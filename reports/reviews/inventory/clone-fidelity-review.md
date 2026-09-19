# Inventory clone-fidelity review

## Result

`Pass, source-compatible` for the requested Storage core. Portability and
runtime verification are reported separately.

## Active implementation evidence

- Source `dev` revision `4628e0317` is the selected active implementation.
- `StorageManager.fcg` is registered through `DatabaseController` and called by
  active HUD, trigger, Rebirth, passive, base, tracking, and visuals paths.
- Source `InventoryManager.fcg` has separate persistence keys and no active
  Storage dependency; it is excluded.

## Comparison

| Surface | Result | Evidence / target |
|---|---|---|
| Player-keyed pet state | Preserved | `InventoryManager.fcg` maps keyed by `UUID` |
| Storage persistence keys | Preserved | `InventoryDefinitions.fcg`: `pStoragePets`, `pStorageBalance` |
| Batch load and per-key retry | Preserved | `LoadInventoryDatabase`, `LoadPlayerInventoryValue` |
| Ready signaling | Preserved | Ready set only after extraction, balance, capacity, and income |
| Save and delayed cache clear | Preserved | `SaveInventoryDatabase`, `ClearData` |
| Pet serialized fields | Preserved | `Id`, `M`, `W`, `Lv`, `Idx`, `ST` |
| Capacity overflow | Preserved | max capacity is never lowered below loaded pet count |
| Retrieve lock | Preserved | `LOCK_DURATION = 28800` |
| Storage income multiplier | Preserved | `INCOME_PERCENT = 0.04` |
| Request -> Check -> Process | Preserved | store/retrieve public actions |
| Source enum types | Intentionally changed | generic string definitions avoid target enum collision |
| Pet/base/wallet/UI side effects | Intentionally isolated | explicit consumer hooks |
| Source UI/scene assets | Omitted by request scope | core logic request; no replacement asset invented |

## Behavior changes and compatibility impact

The target manager accepts a generic pet snapshot rather than reading a source
`PetsManager` slot. It accepts runtime pet income rather than calling
`LevelUpPetManager`, and returns claimed balance rather than crediting a source
`WalletManager`. These changes preserve the Storage state machine while making
source-only systems explicit consumer obligations.

The target uses database registration name `InventoryStorage` to avoid confusing
it with source `DatabaseType.Inventory`; it intentionally keeps the source
storage keys for persistence compatibility.

## Runtime and portability

- Serialized clone: `Complete with documented unresolved runtime gaps`.
- Runtime verification: `Not performed`.
- Standalone portability: `Standalone with optional integrations`.
