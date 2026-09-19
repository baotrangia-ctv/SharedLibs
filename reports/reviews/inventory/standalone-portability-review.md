# Inventory standalone-portability review

## Status

`Standalone with optional integrations`.

| Dependency | Required | Handling | Consumer responsibility |
|---|---|---|---|
| `DatabaseController.fcg` | Yes | Reuse target equivalent | Register one authoritative InventoryStorage writer |
| `DataUtils.fcg` | Yes | Reuse target equivalent | Preserve target serialization utility |
| `BigNumberHandler.fcg` | Yes | Copy reusable source utility | Keep list-based balance representation |
| Source `PetsManager` | For store/retrieve gameplay | Abstracted | Pass snapshot; remove/add pet after success |
| Source `PetConfigs` | For source-valid pet IDs | Abstracted | Validate pet contract before request or strengthen consumer check |
| Source `RebirthManager`/`PetPassiveManager` | For capacity | Abstracted | Call `SetInventoryCapacityInputs` |
| Source `LevelUpPetManager` | For income | Abstracted | Call `SetPlayerInventoryPetIncome` and recalculate |
| Source `WalletManager` | For multiplier/claim | Abstracted | Set multiplier; credit `HandleClaimBalance` result |
| Source `TimeManager`/`PlayersManager` | For lock/offline time | Abstracted | Set current timestamp and delta |
| Source `PetIndexManager` | Cross-store uniqueness | Partially isolated | Validate collisions outside SharedLibs; local duplicates are guarded |
| HUD, prompt, SFX, visuals, analytics | Optional | Omitted | Consumer owns presentation and tracking |
| Source UI/prefab/material/texture | Optional | Omitted | Consumer owns editor assets |

No exact blocker remains. Full gameplay portability depends on consumer hooks,
but the module itself compiles without source Managers.
