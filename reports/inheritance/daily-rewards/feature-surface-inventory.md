# Daily Rewards Feature Surface Inventory

| Source artifact | Responsibility | Active status | Evidence label | Clone classification | Binding classification | Stage status | Portability impact | Target layer | Target handling |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `Assets/Scripts/Manager/ActivitiesManager.fcg:115,289,326,380-526` | Load/save, day refresh, streak state, daily reward list, claim action | Latest active | Direct repository evidence; active `HudActivities` call sites | Reusable after dependency isolation | Source manager + consumer integration | Complete with unresolved bindings | User type/rebirth/UI must be supplied by consumer | `Assets/Scripts/Managers/DailyRewardsManager.fcg` | Core state and Request-Check-Process flow cloned; source-only providers isolated |
| `Assets/Scripts/Configs/ActivitiesConfigs.fcg:65-226` | CSV parsing and user-type/rebirth/day -> gift lookup | Latest active | Direct repository evidence | Reusable after path adjustment | Generated enum remapped to target registration | Complete | Target must register `EResCSV.DailyRewards` | `Assets/Scripts/Configs/DailyRewardsConfigs.fcg` | Daily-only config extracted; target static column definitions used |
| `Assets/CSV/DailyRewards.csv` | 35-row daily reward matrix | Latest active | Byte/hash verified against source | Reusable as-is | CSV asset registration | Complete | None for file; consumer must keep registration | `Assets/CSV/DailyRewards.csv` | Imported through Studio; SHA-256 matches source |
| `Assets/Scripts/Manager/TimeManager.fcg` | GMT day index | Active dependency | Direct repository evidence | Reusable after dependency isolation | Source Flags/debug time omitted | Complete | Uses engine server time/region | `Assets/Scripts/Utils/DailyRewardsTime.fcg` | GMT offsets and day-index logic preserved; debug controls excluded |
| `Assets/Scripts/Manager/MailsManager.fcg` | Mail capacity, config-gift validation, receive | Active dependency | Direct target/source repository evidence | Consumer integration point | Existing target public API | Complete | Consumer must initialize Mails DB before claims | Existing `Assets/Scripts/Managers/MailsManager.fcg` | Reused; Daily manager calls target contract |
| `Assets/Scripts/Configs/MailConfigs.fcg` + target `Gifts.csv` | Gift windows and reward payloads | Active dependency | Direct target repository evidence | Reusable after schema adaptation | Target `Gifts` schema differs from source `giftcode.csv` | Complete with adaptation | Reward consumer must understand target reward fields | Existing MailConfigs/Gifts | Added required gift rows, canonical reward keys, unbounded-window support |
| `Assets/Scripts/Utils/DataUtils.fcg` | JSON-like persistence/list conversion | Active dependency | Direct target repository evidence | Reuse existing utility | No new serializer | Complete | Shared encoding remains target-defined | Existing DataUtils | Reused for load/save and lists |
| `Assets/Scripts/HUDs/HudActivities.fcg:417-552` + related UI assets | Display, prompt, reward effect, button payload | Latest active | Direct source call-site evidence | Consumer integration point | Source UI/IDs not portable to SharedLibs | Not applicable | Consumer must adapt UI and pass rebirth/user type | None cloned | Omitted by core-logic scope; no simplified HUD invented |
| `Assets/Scripts/Manager/DailyRewardManager.fcg` | Lucky Spin/milestone activity | Active adjacent surface | Source comments and HudActivities call sites | Source-specific dependency | Explicit scope boundary | Not applicable | Separate future inheritance task | None | Not mixed into Daily Rewards clone |

## Definitions and bindings

- Persisted field names `Activity_LoginDate`, `Activity_LoginStreaks`,
  `Activity_CanClaimDates`, and `Activity_UserType` are preserved.
- Source `DatabaseType.Activities`/`pActivities` was isolated to
  `DailyRewards`/`pDailyRewards` because SharedLibs does not own the source's
  combined Activities database. This is an explicit portability adaptation.
- No custom enum, component, texture, or serialized UI binding is required by
  the core logic package.

