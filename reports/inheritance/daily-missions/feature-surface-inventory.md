# Daily Missions feature-surface inventory

Evidence labels: `Verified from source script`, `Verified from CSV`, `Verified from config`, `Verified from asset metadata`, `Inferred from call-site evidence`, and `Needs Studio verification`.

## Source surface

| Surface | Source evidence | SharedLibs result |
|---|---|---|
| Active manager | `StealAPet/Assets/Scripts/Manager/ActivitiesManager.fcg`, active file at source commit `0c1e80fb` | Mission-only `DailyMissionsManager.fcg`; `Verified from source script` |
| Mission config | `StealAPet/Assets/Scripts/Configs/ActivitiesConfigs.fcg` | `DailyMissionsConfigs.fcg`; `Verified from config` |
| Milestone config | `StealAPet/Assets/Scripts/Configs/MilestoneConfig.fcg` | `DailyMissionMilestonesConfigs.fcg`; `Verified from config` |
| Mission data | `StealAPet/Assets/CSV/DailyMissions.csv`, 22 data rows | `Assets/CSV/DailyMissions.csv`, content preserved with normalized line endings; `Verified from CSV` |
| Milestone data | `StealAPet/Assets/CSV/milestone.csv`, milestone catalog including ID 11 | `Assets/CSV/milestone.csv`, content preserved with normalized line endings; `Verified from CSV` |
| Persistence | `pActivities`, `Activity_*` fields in `ActivitiesManager` | Dedicated `DailyMissions` database and `pDailyMissions`; field values preserved under `DailyMission_*` keys |
| Progress call sites | Source Managers/Player/Base call `UpdateDailyMissionsProgress` | Generic action-string API plus explicit value API for provider-backed progress |
| Claim flow | Request → Check → Process for mission, all missions, milestone | Same three-phase public API with reward delivery preflight |
| UI/HUD | `HudActivities.fcg` | Omitted intentionally; consumer adapts returned data |
| Reward/player providers | `RewardManager`, `MailsManager`, `PlayersManager`, `WalletManager`, `RebirthManager`, `PetsManager` | Omitted from shared core; adapters/consumers own delivery and provider lookups |

## Source actions found

`BuyPets`, `ClaimIncome`, `LockBase`, `GetPets`, `Rebirth`, `SaveMoney`, `FusionPets`, `StealPet`, `HitPlayer`, `BuyItem`, `BuyRSItem`, `SpendPetCoins`, `Login`, `LuckySpin`, and `Online` were found in the source generated action definition. Used mission CSV actions are preserved unchanged as strings.

## Source reward values found

Reward type values are carried as the source integer values from CSV. The source milestone-point value `8` is named `REWARD_TYPE_MILESTONE_POINT` in the shared definitions. Delivery-specific types remain opaque to the shared core and are returned to the consumer.

