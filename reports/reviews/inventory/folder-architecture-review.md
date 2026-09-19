# Inventory folder-architecture review

| File | Responsibility | Folder | Decision | Evidence |
|---|---|---|---|---|
| `Assets/Scripts/Managers/InventoryManager.fcg` | Authoritative state, lifecycle, actions | Managers | Retain | Manager owns persistence and Request/Check/Process |
| `Assets/Scripts/Configs/InventoryDefinitions.fcg` | Feature keys, statuses, schema, constants | Configs | Retain | Shared by Manager and consumers |
| `Assets/Scripts/Utils/BigNumberHandler.fcg` | Generic big-number utility | Utils | Retain | Reused by balance and other future modules |
| `reports/inheritance/inventory/*` | Execution evidence | reports | Retain | Router-required evidence |
| `reports/reviews/inventory/*` | Review evidence | reports | Retain | Review-required outputs |
| `.agent/skills/inventory-source-to-shared/SKILL.md` | Source-to-shared workflow | skill layer | Retain | Paired module skill |
| `.agent/skills/inventory-shared-to-consumer/SKILL.md` | Shared-to-consumer workflow | skill layer | Retain | Paired module skill |

No mixed `Assets/Scripts/Inventory/` feature folder was created. No HUD, asset,
config reader, and utility responsibilities are mixed in one directory.
