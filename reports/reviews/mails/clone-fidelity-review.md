# Mails Clone Fidelity Review

Date: 2026-07-27
Module: `mails`
Stage A result: `Pass, source-compatible`

| Surface | Result | Evidence |
| --- | --- | --- |
| Latest active manager selected | Preserved | `StealAPet/Assets/Scripts/Manager/MailsManager.fcg` is the active manager; deprecated load helpers were identified but not cloned as live shared APIs. |
| Request -> Check -> Process flow | Preserved | `Assets/Scripts/Managers/MailsManager.fcg` keeps `RequestReceiveMail`, `CheckConditionReceiveMail`, `ProcessReceiveMail`, `RequestClaimMail`, `CheckConditionClaimMail`, and `ProcessClaimMail`. |
| Persistence schema | Preserved | Shared manager keeps `CurrentMails`, `PendingMails`, and `OwnGiftCodeHasUse` storage keys. |
| Mail serialization shape | Preserved | Shared manager still uses list-of-key/value JSON strings through `DataUtils.JsonStringToListKeyValueV2` and `ListKeyValueToJsonString`. |
| Readable UI asset | Preserved | `Assets/HUDs/Mail.ui` was copied from source. |
| MailDetails CSV | Preserved | `Assets/CSV/MailDetails.csv` was copied from source. |
| Config reader implementation | Intentionally changed | SharedLibs lacks generated CSV resource enums, so `Assets/Scripts/Configs/MailsConfigs.fcg` bootstraps the copied MailDetails rows directly while leaving consumer gift config as a registration surface. |
| Source-only reward, prompt, analytics, and pet-slot dependencies | Intentionally changed | These integrations were not copied from `RewardManager`, `PetsManager`, `PlayersManager`, `TrackingManager`, `HudMenu`, or prompt events; they were isolated as consumer work. |
| Deprecated source load path | Omitted with evidence | Deprecated helpers remain documented in review outputs and were not promoted into the shared API surface. |

Standalone portability status: `Consumer adaptation required`

Runtime verification status: `Not performed`
