# Inventory static-definitions review

| Definition | Placement | Decision | Evidence |
|---|---|---|---|
| `pStoragePets`, `pStorageBalance`, `PlayerSave` | `InventoryDefinitions.fcg` | Move to feature definitions | Shared by load/save and consumers |
| `Id`, `M`, `W`, `Lv`, `Idx`, `ST` | `InventoryDefinitions.fcg` | Move to feature definitions | Persistence schema contract |
| `LOCK_DURATION`, `INCOME_PERCENT`, one-hour seconds | `InventoryDefinitions.fcg` | Move to feature definitions | Shared formula contract |
| payload field names | `InventoryDefinitions.fcg` | Move to feature definitions | Shared Manager/consumer boundary |
| status strings | `InventoryDefinitions.fcg` | Move to feature definitions | Public action result contract |
| default pet values | `InventoryManager.fcg` | Keep private in Manager | Internal normalization only |
| runtime cache field names | `InventoryManager.fcg` | Keep private in Manager | Not a consumer contract |

No target `StatusCodes` or generated source enum was modified; the module-owned
definitions avoid collision with the source Inventory feature.
