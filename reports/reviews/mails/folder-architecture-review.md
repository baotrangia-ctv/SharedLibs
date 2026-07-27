# Mails Folder Architecture Review

Date: 2026-07-27
Module: `mails`

| Misplaced File | Current Responsibility | Correct Target Folder | Decision | Evidence |
| --- | --- | --- | --- | --- |
| `Assets/Scripts/Mails/` | Mixed feature-folder remnant | Layer-owned folders only | Remove | The directory was previously identified as the forbidden mixed-layer target for Mails. |
| `Assets/Scripts/Configs/MailsDefinitions.fcg` | Shared feature definitions | `Assets/Scripts/Configs/` | Retain | Shared payload keys, storage keys, tab ids, and UI asset id are feature definitions. |
| `Assets/Scripts/Configs/MailsConfigs.fcg` | Config and registry surface | `Assets/Scripts/Configs/` | Retain | Mail detail and gift config ownership belongs to Configs. |
| `Assets/Scripts/Managers/MailsManager.fcg` | Authoritative runtime and persistence | `Assets/Scripts/Managers/` | Retain | Manager owns load/save/request/process flow. |
| `Assets/Scripts/HUDs/MailsHUD.fcg` | UI behavior | `Assets/Scripts/HUDs/` | Retain | HUD owns open/list/select/render behavior. |
| `Assets/Scripts/HUDs/MailsHUDControl.fcg` | UI input routing | `Assets/Scripts/HUDs/` | Retain | Control flow stays layer-local with the HUD. |
| `Assets/HUDs/Mail.ui` | UI asset | `Assets/HUDs/` | Retain | Readable UI asset was copied without relocation. |
| `Assets/CSV/MailDetails.csv` | CSV data | `Assets/CSV/` | Retain | CSV belongs to the data/config layer. |
