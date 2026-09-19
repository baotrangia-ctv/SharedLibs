# Folder Architecture Review

**Result:** Retain.

| Responsibility | Current path | Decision |
| --- | --- | --- |
| Manager | `Assets/Scripts/Managers/DailyRewardsManager.fcg` | Retain; matches target plural Managers convention |
| Config | `Assets/Scripts/Configs/DailyRewardsConfigs.fcg` | Retain |
| Feature definitions | `Assets/Scripts/Consts/DailyRewardsDefinitions.fcg` | Retain |
| Generic time utility | `Assets/Scripts/Utils/DailyRewardsTime.fcg` | Retain; source behavior is isolated and reusable |
| Serialized config | `Assets/CSV/DailyRewards.csv` | Retain |
| Inheritance report | `reports/inheritance/daily-rewards/` | Retain |
| Review reports | `reports/reviews/daily-rewards/` | Retain |

No mixed-layer file or feature-subfolder exception was introduced. The target
folder convention is intentionally preserved rather than copying the source's
singular `Manager` directory.

