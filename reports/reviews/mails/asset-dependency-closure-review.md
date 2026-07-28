# Mails Asset Dependency Closure Review

Date: 2026-07-27
Module: `mails`

| Dependency | Required | Classification | Target handling | Evidence |
| --- | --- | --- | --- | --- |
| `Assets/HUDs/Mail.ui` | Required | Exists and can be copied | Copied from source | Readable UI asset drives the mail interaction surface. |
| `Assets/CSV/MailDetails.csv` | Required | Exists and can be copied | Copied from source | Shared config bootstraps these mail-detail rows. |
| `Assets/Scripts/Utils/DataUtils.fcg` | Required | Exists and can be reused | Reuse target equivalent | Shared manager relies on existing JSON/list helpers. |
| Source texture references inside `Mail.ui` | Required for visual parity | Runtime verification required | Preserve serialized references | The copied UI still points at the source asset paths recorded in the UI JSON. |
| `RewardManager`, `PetsManager`, `PlayersManager`, `TrackingManager`, `HudMenu` | Source-specific | Exists but source-specific | Excluded and documented | SharedLibs does not currently contain those game-specific integrations. |

Smallest complete set conclusion:

- The copied UI asset, copied MailDetails CSV, shared definitions/configs, shared manager, shared HUD, and shared HUD control form the smallest useful inheritance set completed in this task.
