# Inventory inheritance report

## 1. Module

SharedLibs module `Inventory`, whose source feature is Steal A Pet `Storage`.
It is not Steal A Pet's separate `InventoryManager`.

## 2. Source project

`D:\Craftland\StealAPet`, branch `dev`, active revision `4628e0317`.

## 3. Target project

`D:\Craftland\_Libs\SharedLibs`.

## 4. Repository evidence inspected

Router/index, intake template, all required common inheritance references,
source and target FC workflows, source project conventions, SAP Storage business
logic, active Storage Manager/call sites, source generated definitions, source
Storage UI/trigger/serialized asset references, target SharedLibs managers,
definitions, utilities, and DatabaseController.

## 5. Active implementation selected

`Assets/Scripts/Manager/StorageManager.fcg` from source `dev` was selected from
active database dispatch and call sites. `Assets/Scripts/Manager/InventoryManager.fcg`
was explicitly excluded.

## 6. Deprecated implementations excluded

No separate active Storage implementation was found. Unused helper
`ConvertDataToPetValue`, unused `GetStoragePetIndexBySlot`, and commented passive
serialization code were not copied.

## 7. Source files cloned or adapted

- `Assets/Scripts/Managers/InventoryManager.fcg`: adapted faithful core.
- `Assets/Scripts/Configs/InventoryDefinitions.fcg`: new shared definitions and
  source-compatible storage keys.
- `Assets/Scripts/Utils/BigNumberHandler.fcg`: copied reusable utility because
  SharedLibs had no equivalent.

## 8. Source files omitted

Source UI/HUD, trigger, prefab, material, texture, sprite, localization,
PetsManager, RebirthManager, PetPassiveManager, LevelUpPetManager, WalletManager,
PlayersManager, VisualsManager, DebugLogManager, PetTransactionsManager, and
source InventoryManager were omitted or isolated as consumer dependencies.

## 9. Serialized assets discovered

`Assets/HUDs/PetStorage.ui`, `Assets/Prefabs/Base/Storage.prefab`,
`Assets/Materials/Shops/Storage.mat`, `Assets/Textures/Shops/Storage.png`, and
`Assets/Sprites/Icons/Storage.png` were inspected as source evidence and omitted
because the request is core logic only.

## 10. Serialized asset fidelity

Not applicable to the delivered core module. No serialized target asset was
invented or edited. Source UI/prefab references remain a consumer/editor task.

## 11. Entity or asset ID handling

Not applicable. No entity, UI, scene, prefab, or editor registration was copied.

## 12. Serialized bindings preserved

The persistence field values `Id`, `M`, `W`, `Lv`, `Idx`, and `ST`, and keys
`pStoragePets`/`pStorageBalance`, were preserved in `InventoryDefinitions.fcg`.

## 13. Dependency closure

Target `DatabaseController` and `DataUtils` were reused. `BigNumberHandler` was
copied. Source business Managers were isolated behind explicit setter/payload
hooks. Source UI/asset closure was excluded by scope.

## 14. Missing dependencies

No compile-blocking dependency remains. Consumer-provided pet validation,
capacity, income, time, multiplier, wallet, prompt, and transfer behavior remain
integration obligations.

## 15. Config fidelity

Storage capacity remains a consumer-owned input from the source Rebirth and
Pack Rat systems. The shared core preserves capacity plus current-item overflow
behavior.

## 16. CSV fidelity

No CSV was copied. `rebirth.csv` is source-specific capacity data and is a
consumer integration input, not shared module data.

## 17. Data lifecycle fidelity

Batch load, per-key retry, deserialize, capacity setup, income recalculation,
ready signaling, two-key save, saved signaling, 3-second delay, and cache clear
are preserved.

## 18. Public API fidelity

Store/retrieve, query, balance, lock, capacity, and income surfaces are
preserved with `Inventory` names and generic `Map<string, object>` contracts.
`ExtractPetValueBySlot` is replaced by a consumer-provided pet snapshot.

## 19. Source-specific dependencies

Pets/base transfer, pet config validation, rebirth/passive capacity, level-up
income, wallet credit/multiplier, source time manager, prompt/SFX/visuals,
transactions, and source global pet-index tracking are source-specific.

## 20. Genericization changes

Generated source enums were replaced by string definitions; source Manager
lookups were replaced by input hooks; source UI/error side effects were omitted;
the module uses `InventoryStorage` as its database registration name to avoid
colliding with source `DatabaseType.Inventory`.

## 21. Utilities reused

Shared `DataUtils.fcg` was reused for the exact structured-data delimiters and
`BigNumberHandler.fcg` was copied for list-based large-number arithmetic.

## 22. Interfaces introduced

`SetInventoryCapacityInputs`, `SetPlayerInventoryPetIncome`,
`SetCurrentTimestamp`, `SetPlayerDeltaLastLogTime`, `SetPlayerMultiplyRate`,
payload snapshot/flag fields, and claim-return semantics are the minimal
consumer integration points.

## 23. Adapters introduced and justification

No pass-through adapter was introduced. The Manager directly owns shared state;
only source-only inputs and external side effects are represented as explicit
hooks because SharedLibs has no generic pet/base/wallet contract.

## 24. Files organized by layer

- Logic: `Assets/Scripts/Managers/InventoryManager.fcg`
- Definitions: `Assets/Scripts/Configs/InventoryDefinitions.fcg`
- Utility: `Assets/Scripts/Utils/BigNumberHandler.fcg`
- Reports: `reports/inheritance/inventory/`, `reports/reviews/inventory/`
- Skills: `.agent/skills/inventory-source-to-shared/`,
  `.agent/skills/inventory-shared-to-consumer/`

## 25. Demo artifacts omitted

No demo Manager, mock UI, placeholder asset, or sample consumer was added.

## 26. Serialized clone status

`Complete with documented unresolved runtime gaps` for the core persistence and
structured-data surface; serialized UI/scene stages are out of scope.

## 27. Runtime verification status

`Not performed`. Full local FC compilation passed; no live Studio session was
used.

## 28. MCP usage

None. Repository evidence was sufficient for the core FC implementation; no
editor-owned asset was changed.

## 29. Remaining Studio-only verification gaps

None for the delivered text-only core. A consumer that adds HUD, trigger,
prefab, scene, or script attachments must perform Studio registration/build.

## 30. Remaining consumer integration work

Connect pet snapshot/removal/addition, capacity, income resolver, current time,
offline delta, wallet multiplier/credit, feature/base-slot flags, UI/prompts,
transactions, and a single persistence owner.

## 31. Stage completion summary

| Stage | Status |
|---|---|
| Source discovery | Complete |
| Active API analysis | Complete |
| Manager clone | Complete with unresolved bindings |
| Config and CSV clone | Complete with unresolved bindings; no CSV required |
| Data lifecycle clone | Complete |
| Serialized asset clone | Not applicable to core scope |
| Dependency closure | Complete with consumer integrations |
| Shared refactor | Complete |
| Runtime verification | Runtime verification pending |

## 32. Safe files created

The three FC files, paired module skills, intake, feature inventory, API
inventory, inheritance report, and focused review reports listed in the review
directory.

## 33. Safe files modified

No pre-existing source or SharedLibs implementation file was modified. Only new
files were created.

## 34. Faithful clone status

`Pass, source-compatible` for Storage persistence, data schema, balance math,
capacity overflow behavior, lock, and Request-Check-Process core. Source-only
effects are explicitly isolated.

## 35. Clone fidelity status

`Preserved` for keys, serialized fields, lifecycle order, lock duration, income
multiplier, cache boundaries, and core actions; `Intentionally changed` for
source enum types and external Manager/UI calls; `Missing by scope` for UI/assets.

## 36. Standalone portability status

`Standalone with optional integrations`. The FC core compiles without source
Managers; consumer hooks are required for full gameplay behavior.

## 37. Runtime verification evidence and pending checks

Command: project `fccompile_external.exe -i Assets`; exit code `0`. Warnings
are pre-existing deprecated APIs in `Assets/Scripts/HUDs/HudControls.fcg`.
Pending: consumer runtime load/save/reconnect and real pet/wallet integration.

## 38. Utility dependency analysis

`DataUtils` was reused because target signatures match the source encoding.
`BigNumberHandler` was copied because the target had no equivalent and the
Storage balance depends on its arbitrary-size list arithmetic.

## 39. Texture dependency analysis

Storage textures/icons/materials are optional visual dependencies for the omitted
HUD/world surface and were not copied into the core module.

## 40. Custom enum inventory

Source `DataType`, `PetValue`, `DataKey`, `RequestParameter`, `CustomStatusCode`,
and `DatabaseType` values were searched in the source generated library.
Target code preserves required persistence values as feature definitions and
uses strings for public generic payloads. No target generated enum was edited.

## 41. Custom component inventory

None in the delivered core. UI/scene custom components belong to the omitted
consumer surface.

## 42. Definitions found in repository

Source generated definitions were found in
`Temp/UGCLanguage/editorGen/EditorGenLib.fcc`; target equivalents for
`DatabaseController` and `DataUtils` were found in SharedLibs.

## 43. Values preserved unchanged

`pStoragePets`, `pStorageBalance`, `PlayerSave`, `Id`, `M`, `W`, `Lv`, `Idx`,
`ST`, `LOCK_DURATION = 28800`, and `INCOME_PERCENT = 0.04`.

## 44. Values remapped

Source `DatabaseType.Storage` is registered as `InventoryStorage`; source enum
payloads/status codes are represented by `InventoryDefinitions` string keys.

## 45. Values unresolved but preserved

Consumer pet IDs, mutation/weather validity meanings, editor bindings, and
consumer-specific status presentation remain unresolved at the shared layer and
are preserved as generic payload/status contracts.

## 46. Exact MCP blockers

None. The six strict MCP blocker conditions are not met because no editor-owned
asset or unknown mandatory binding must be written for this core request.

## 47. Work completed without MCP

Repository discovery, active-version selection, dependency closure, FC code,
utility reuse/copy, compile validation, paired skills, and reports.

## 48. Work remaining with Studio

Only consumer-side UI/scene/trigger registration and live runtime verification,
if a consumer chooses to add those surfaces.

## 49. Consumer adaptation requirements

See `inventory-shared-to-consumer/SKILL.md` and the standalone portability
review. Do not run this module alongside a second authoritative writer for the
same two persistence keys.
