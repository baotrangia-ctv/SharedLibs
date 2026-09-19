# Inventory asset-dependency-closure review

## Smallest complete core closure

| Dependency | Source evidence | Target handling | Required | Stage |
|---|---|---|---|---|
| `StorageManager.fcg` | Imports DataUtils, BigNumber, DatabaseController and source Managers | Adapted `InventoryManager` | Yes | Complete |
| `DataUtils.fcg` | JSON/list encoding calls | Reuse target equivalent | Yes | Complete |
| `BigNumberHandler.fcg` | balance add/multiply/min/convert calls | Copy to target Utils | Yes | Complete |
| `DatabaseController.fcg` | registration/retry/ready/saved calls | Reuse target equivalent | Yes | Complete |
| Rebirth/PetPassive/LevelUp/Wallet/Pets/Time Managers | active Storage call sites | Isolate as hooks | Gameplay integration | Complete with unresolved bindings |
| `HudPetStorage.fcg` / `StorageTrigger.fcg` | active UI/trigger calls | Omit from core | No | Not applicable |
| `PetStorage.ui` / `Storage.prefab` | serialized UI/world references | Omit from core | No | Not applicable |
| Storage textures/materials/sprites | visual references | Omit from core | No | Not applicable |
| Source `InventoryManager.fcg` | separate keys and callers | Exclude | No | Not applicable |

## Texture and file analysis

Source texture/material/prefab references were located and existence-checked.
They are optional visual assets for the omitted surface, not required for the
text-only Manager to compile or load its persistence schema. No texture was
copied or replaced.

## Conclusion

The closure is complete for the requested core. Consumer gameplay and editor
asset closure remain explicit, bounded integration work.
