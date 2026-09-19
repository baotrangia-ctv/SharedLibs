# Inventory feature-surface inventory

Source feature: `Storage` from `D:\Craftland\StealAPet`
Target module: `Inventory` in `D:\Craftland\_Libs\SharedLibs`
Active source revision: `dev`, `4628e0317` (`chore: texture no tiles`)

| Source artifact | Responsibility | Active status | Evidence label | Clone classification | Binding classification | Stage status | Portability impact | Target layer | Target handling |
|---|---|---|---|---|---|---|---|---|---|
| `Assets/Scripts/Manager/StorageManager.fcg` | Storage persistence, pet list, capacity, income, lock, actions | Latest active | Verified from source script | Reusable after dependency isolation | Source-specific and isolatable | Complete with unresolved bindings | Consumer must provide pet/capacity/time/wallet inputs | `Assets/Scripts/Managers/` | `InventoryManager.fcg` |
| `Assets/Scripts/Manager/InventoryManager.fcg` | Mutagen, weather-generator, event-pet inventory | Explicitly excluded | Verified from source script | Source-specific dependency | Excluded by user scope | Not applicable | Must not be copied or conflated | None | No target file |
| `Assets/Scripts/Configs/RebirthConfigs.fcg` | Storage slot capacity source | Latest active dependency | Verified from source script | Consumer integration point | Source-specific and isolatable | Complete with unresolved bindings | Consumer calls `SetInventoryCapacityInputs` | `Assets/Scripts/Configs/` | No copy; hook documented |
| `Assets/CSV/rebirth.csv` | Rebirth-to-storage capacity data | Latest active dependency | Verified from CSV | Consumer integration point | Source-specific and isolatable | Complete with unresolved bindings | Consumer owns capacity config | `Assets/CSV/` | No copy |
| `Assets/Scripts/Manager/PetPassiveManager.fcg` | Pack Rat slot bonus, passive refresh | Latest active dependency | Verified from source script | Consumer integration point | Source-specific and isolatable | Complete with unresolved bindings | Consumer passes bonus slots and refreshes pet state | None | No copy |
| `Assets/Scripts/Manager/LevelUpPetManager.fcg` | Pet income calculation | Latest active dependency | Verified from source script | Consumer integration point | Source-specific and isolatable | Complete with unresolved bindings | Consumer passes runtime income per stored pet | None | No copy |
| `Assets/Scripts/Manager/WalletManager.fcg` | Wallet earn and multiplier | Latest active dependency | Verified from source script | Consumer integration point | Source-specific and isolatable | Complete with unresolved bindings | Consumer sets multiplier and credits claim result | None | No copy |
| `Assets/Scripts/Manager/PetsManager.fcg` | Base-pet transfer, validation, base capacity | Latest active dependency | Verified from source script | Consumer integration point | Source-specific and isolatable | Complete with unresolved bindings | Consumer passes pet snapshot and handles transfer | None | No copy |
| `Assets/Scripts/Manager/PetIndexManager.fcg` | Global pet-index uniqueness | Latest active dependency | Verified from source script | Reusable after dependency isolation | Source-specific and isolatable | Complete with unresolved bindings | Shared module protects local duplicates; consumer checks cross-store collisions | `Assets/Scripts/Managers/` | Local per-player index guard |
| `Assets/Scripts/Utils/DataUtils.fcg` | Structured storage parsing/serialization | Latest active dependency | Verified from source script | Reusable as-is | Meaning known and valid | Complete | None; target equivalent exists | `Assets/Scripts/Utils/` | Reused target utility |
| `Assets/Scripts/Utils/BigNumberHandler.fcg` | Large-number balance arithmetic | Latest active dependency | Verified from source script | Reusable as-is | Meaning known and valid | Complete | None | `Assets/Scripts/Utils/` | Copied source utility |
| `Assets/Scripts/SharedLibs/CoreLib/DatabaseController.fcg` | Database registration/readiness/retry/save dispatch | Latest active dependency | Verified from source script | Reuse target equivalent | Meaning known and valid | Complete | Consumer must register only one authoritative writer | `Assets/Scripts/CoreLib/` | Reused target equivalent |
| `Assets/Scripts/Base/StorageTrigger.fcg` | Storage trigger and claim/UI entry point | Latest active | Verified from source script | Consumer integration point | Source-specific and isolatable | Not applicable to core | Consumer owns trigger/UI | `Assets/Scripts/` | Omitted |
| `Assets/Scripts/HUDs/HudPetStorage.fcg` | Storage HUD and button routing | Latest active | Verified from source script | Consumer integration point | Source-specific and isolatable | Not applicable to core | Consumer owns HUD and prompts | `Assets/Scripts/HUDs/` | Omitted |
| `Assets/HUDs/PetStorage.ui` | Serialized storage HUD | Latest active | Verified from serialized asset | Source-specific dependency | Runtime/editor binding required | Not applicable to core | Consumer must register its own UI | `Assets/HUDs/` | Omitted |
| `Assets/Prefabs/Base/Storage.prefab` | Serialized storage world object | Latest active | Verified from serialized asset | Source-specific dependency | Runtime/editor binding required | Not applicable to core | Consumer owns world asset | `Assets/` | Omitted |
| `Assets/Materials/Shops/Storage.mat`, `Assets/Textures/Shops/Storage.png`, `Assets/Sprites/Icons/Storage.png` | Storage visuals | Latest active | Verified from asset metadata | Source-specific dependency | Source-specific and isolatable | Not applicable to core | No visual asset is required by the shared core | `Assets/` | Omitted |
| `Assets/Localization/key.csv` Storage keys | Prompts/title strings | Latest active | Verified from CSV | Consumer integration point | Source-specific and isolatable | Not applicable to core | Consumer owns localization | `Assets/Localization/` | Omitted |
| Generated `DataType`, `PetValue`, `DataKey`, `CustomStatusCode` | Source enums and serialized keys | Latest active | Verified through source generated symbol table | Reusable after dependency isolation | Requires remapping | Complete with unresolved bindings | String definitions preserve keys without target enum collision | `Assets/Scripts/Configs/` | `InventoryDefinitions.fcg` |

## Exclusion closure: StealAPet `Inventory`

The excluded source `Assets/Scripts/Manager/InventoryManager.fcg` has no active
import or call-site dependency from `StorageManager.fcg`. It uses separate keys
`pMutagens`, `pWeatherGens`, and `pEventPets`; Storage uses `pStoragePets` and
`pStorageBalance`. The only shared touch points are generic infrastructure
(`DataUtils`, `BigNumberHandler`, `DatabaseController`) and generated enum
definitions. No shared Manager, feature config, or serialized asset was found.

Evidence: `Verified from source script` (`StorageManager.fcg` imports/call sites
and `InventoryManager.fcg` persistence keys); `Verified through source generated
symbol table` (`Temp/UGCLanguage/editorGen/EditorGenLib.fcc`).
