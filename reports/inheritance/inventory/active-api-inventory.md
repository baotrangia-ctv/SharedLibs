# Inventory active API inventory

| Source API | Version | Active call sites | Status | SharedLibs decision |
|---|---|---|---|---|
| `StorageManager.OnDatabaseLoad` / `LoadStorageDatabase` | current | `DatabaseController` dispatch | Latest active | Inherit as `InventoryManager` with `InventoryStorage` database type |
| `StorageManager.OnDatabaseSave` / `SaveStorageDatabase` | current | `DatabaseController` dispatch | Latest active | Inherit with same two persistence keys and delayed clear |
| `RequestStorePet` -> `CheckConditionStorePet` -> `ProcessStorePet` | current | `HudPetStorage.fcg` | Latest active | Inherit with generic pet snapshot and consumer flags |
| `RequestRetrievePetBySlot` -> `CheckConditionRetrievePetBySlot` -> `ProcessRetrievePetBySlot` | current | `HudPetStorage.fcg` | Latest active | Inherit with generic base-slot flag and returned pet snapshot |
| `HandleClaimBalance` | current | `StorageTrigger.fcg` | Latest active | Inherit as claim-and-return; wallet/UI effects are consumer hooks |
| `SetUpPlayerStorageMaxSlot` | current | `PetPassiveManager`, `RebirthManager`, `StorageManager` | Latest active | Replace source Manager reads with `SetInventoryCapacityInputs` |
| `UpdatePlayerStorageBalanceLoop` / offline update | current | `BasesManager`, `StorageManager` | Latest active | Inherit as `UpdatePlayerInventoryBalanceLoop` with setter inputs |
| `ExtractPetValueBySlot` | current | only `StorageManager` | Active source helper | Omit; consumer passes pet snapshot in payload |
| `GetStoragePetIndexBySlot` | current | no active call site found | Unused by active Storage flow | Omit; generic value query covers the same field |
| `ConvertDataToPetValue` | current | no active call site found | Unused by active Storage flow | Omit |
| commented passive serialization/deserialization lines | legacy/commented | none | Compatibility-only / inactive | Omit; passive remains runtime field but source persistence remains unchanged |
| source `InventoryManager` APIs | separate feature | mutagen/event-pet callers only | Explicitly excluded | Do not inherit or reuse |

Evidence: `Verified from source script` at
`Assets/Scripts/Manager/StorageManager.fcg` and active call sites listed in
`Assets/Scripts/HUDs/HudPetStorage.fcg`, `Assets/Scripts/Base/StorageTrigger.fcg`,
and Manager files.
