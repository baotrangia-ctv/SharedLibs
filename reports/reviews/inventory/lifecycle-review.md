# Inventory data-lifecycle review

## Lifecycle order

1. `OnAwake` initializes maps and registers `InventoryStorage`.
2. `OnDatabaseLoad` receives the controller dispatch and initializes player
   state.
3. Two persistence keys are batch-read; each failed key is retried.
4. Pet records are parsed and balance is converted. The load marks inventory
   data as loaded, then refreshes capacity only if the consumer has supplied
   authoritative capacity inputs, and recalculates income.
5. `SetInventoryCapacityInputs` is the non-blocking consumer handoff: it marks
   capacity ready, refreshes `MaxSlot`, recalculates income, and finalizes the
   database ready signal only after both data and capacity are ready.
6. Runtime balance updates use consumer-provided time delta and multiplier.
7. `OnDatabaseSave` writes both keys, marks saved, waits 3 seconds, and clears
   UUID-keyed runtime cache.

## Findings

- Readiness ordering is preserved: no ready signal precedes required extraction
  and setup.
- Resolved capacity race: `LoadInventoryDatabase` no longer treats
  `petsCount` as provisional capacity and no longer calls `SetDatabaseReady`
  directly. Before the consumer supplies capacity, `MaxSlot` is not
  authoritative and no balance loop is started; after the callback, the
  existing `baseSlots + bonusSlots`, clamped to at least `petsCount`, logic is
  preserved.
- Requests during the handoff return `InventoryNotReady` while persistence is
  still loading or `InventoryCapacityNotReady` while capacity is still
  missing; they cannot return `PlayerFullStorage` from the default zero inputs.
- Resolved direct-capacity API gap: `SetPlayerInventoryMaxSlot` now marks
  capacity ready and finalizes through the same flow, so direct-capacity
  consumers can store/retrieve and save normally. If both capacity APIs are
  used in one session, a warning is logged and the latest call determines
  `MaxSlot`.
- Cache initialization is guarded and player-scoped.
- Reconnect requires the consumer to re-provide capacity, income, time, and
  multiplier inputs after a new load; this is documented as an integration
  contract rather than hidden source state.
- Persistence rollback must not run the shared module and source StorageManager
  as simultaneous writers for the same keys.

Result: `Complete with consumer lifecycle obligations; capacity race resolved`;
runtime reconnect and quit behavior were not live-verified.
