# Mails Static Definitions Review

Date: 2026-07-27
Module: `mails`

| Definition Group | Recommendation | Evidence |
| --- | --- | --- |
| Storage keys, payload keys, mail field keys, tab ids, and shared UI asset id | Move to feature definitions | Centralized in `Assets/Scripts/Configs/MailsDefinitions.fcg` because they are used across Manager and HUD. |
| Config lookup maps and gift registration state | Move to Config definitions | Owned by `Assets/Scripts/Configs/MailsConfigs.fcg`. |
| Temporary control-flow variables inside manager methods | Keep local | These are not reused across files and remain inside `MailsManager.fcg`. |

Compatibility note:

- Persisted mail field names and storage keys match the source active persistence shape and were not renamed.
