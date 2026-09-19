---
name: inventory-shared-to-consumer
description: Integrate the SharedLibs Inventory module, which is Storage-derived, into a consumer without confusing it with Steal A Pet's separate InventoryManager.
---

# Module identity

The shared module is `Inventory` and its implementation is
`Assets/Scripts/Managers/InventoryManager.fcg`. It is a pet Storage-derived
inventory. It is not the Steal A Pet source `InventoryManager` for mutagens,
weather generators, or event pets.

# Consumer contract

The consumer must:

- load `InventoryDefinitions.DATABASE_TYPE` and avoid registering a second
  manager against the same `pStoragePets`/`pStorageBalance` keys
- provide capacity through exactly one API: use
  `SetInventoryCapacityInputs` for base/bonus inputs, or
  `SetPlayerInventoryMaxSlot` for one authoritative direct slot count
- call the selected capacity API after the consumer has authoritative inputs;
  both APIs finalize the same readiness flow, while mixing them in one session
  logs a warning and lets the latest capacity call determine `MaxSlot`
- until capacity is supplied, Inventory keeps its capacity provisional, does
  not mark its database ready, and returns `InventoryCapacityNotReady` instead
  of treating the pet count as a full inventory
- provide runtime pet income via `SetPlayerInventoryPetIncome`
- provide current time, offline delta, and multiplier via the corresponding
  setters before balance updates
- pass a pet snapshot to `RequestStorePet` and remove it from the consumer pet
  store only after success
- pass base-slot and feature flags to `RequestRetrievePetBySlot`, then add the
  returned pet to the consumer pet store only after success
- claim through `HandleClaimBalance` and credit the returned amount in the
  consumer wallet
- own HUD, prompt, SFX, localization, analytics, and editor-owned assets

# Required common references

Load the shared-to-consumer router references under
`.agent/references/inheritance/`:

- `repository-first.md`
- `serialized-assets.md` when the consumer transfers serialized assets
- `dependency-closure.md` when references exist
- `mcp-last.md`
- `runtime-verification.md`
- `preserve-first-bindings.md`
- `repository-definition-search.md`
- `stage-based-completion.md`
- `standalone-portability.md`
- `explicit-mcp-blockers.md`

Use the `review-inherited-module` sections Serialized Asset Fidelity and Asset
Dependency Closure only when the consumer actually transfers those assets, and
always use Standalone Portability, Folder Architecture, Utility Reuse, Static
Definitions, Request-Check-Process, and Data Lifecycle for this persistent
module.

# Workflow

1. Validate SharedLibs and consumer roots and create the consumer intake before
   any consumer write.
2. Read the shared contract directly; do not re-read or depend on the original
   Steal A Pet project.
3. Inspect consumer pet, capacity, wallet, time, persistence, and UI contracts.
4. Map the hooks above to existing consumer APIs. Adapt only proven type or
   lifecycle incompatibilities.
5. Ensure one authoritative writer for `pStoragePets` and `pStorageBalance`.
6. Run the consumer compiler/build and separate serialized fidelity,
   portability, and live runtime results.

# Reports and rollback

Write integration and rollback evidence under
`reports/consumer-integrations/[consumer-project]/inventory/`. Rollback must
disable the consumer registration and remove the consumer's Inventory entry
point without deleting the persisted Storage keys until migration ownership is
confirmed.

# Stop conditions

Do not block for missing UI or runtime-only verification. Block only the exact
consumer stage that cannot be made structurally safe, or the whole integration
when all six strict MCP blocker conditions are proven.
