# Mails Inheritance Report

Date: 2026-07-27
Module: `mails`
Source: `C:/_Code/craftland/StealAPet`
Target: `C:/_Code/craftland/SharedLibs`

## Path Validation

- Source root exists, is distinct from the target root, and is configured read-only in `.codex/project-paths.json`.
- Target root exists and is configured read-write in `.codex/project-paths.json`.
- Both roots expose Git repository markers.

## Active Source Surface

Latest active filesystem evidence used for Stage A discovery:

- Manager: `Assets/Scripts/Manager/MailsManager.fcg`
- Config reader: `Assets/Scripts/Configs/MailConfigs.fcg`
- HUD: `Assets/Scripts/HUDs/HudMail.fcg`
- Readable UI asset: `Assets/HUDs/Mail.ui`
- CSV: `Assets/CSV/MailDetails.csv`
- Button routing evidence: `Assets/Scripts/Utils/CustomUIUtils.fcg`

Deprecated or compatibility-only logic found and classified separately:

- `LoadOldMails`
- `LoadPlayerMails_Deprecated`
- `ExtractPlayerMails_Deprecated`
- `CleanMails_Deprecated`

## Target Outputs

Implemented or copied into SharedLibs:

- `Assets/Scripts/Configs/MailsDefinitions.fcg`
- `Assets/Scripts/Configs/MailsConfigs.fcg`
- `Assets/Scripts/Managers/MailsManager.fcg`
- `Assets/Scripts/HUDs/MailsHUD.fcg`
- `Assets/Scripts/HUDs/MailsHUDControl.fcg`
- `Assets/HUDs/Mail.ui`
- `Assets/HUDs/Mail.ui.meta`
- `Assets/CSV/MailDetails.csv`
- `Assets/CSV/MailDetails.csv.meta`

## Stage Status

| Stage | Status | Notes |
| --- | --- | --- |
| Source discovery | Complete | Manager, HUD, config, CSV, UI, and button-routing evidence were located from the repository. |
| Active API analysis | Complete | Active Request/Check/Process flow identified; deprecated load path retained only as review evidence. |
| Manager clone | Complete | Persistence, receive, claim, query, and serialization flow were rebuilt in shared form. |
| Config and CSV clone | Partially complete | Readable CSV was copied; runtime config bootstraps the copied rows because SharedLibs lacks generated CSV resource enums. |
| Data lifecycle clone | Complete | Load, save, ready, clear, and pending-mail flush flows were carried over. |
| Serialized asset clone | Complete with unresolved bindings | `Assets/HUDs/Mail.ui` was copied byte-for-byte; editor registration and control bindings still need Studio verification. |
| Dependency closure | Partially complete | Source-only reward, prompt, analytics, and pet-slot integrations were isolated instead of copied. |
| Shared refactor | Complete | Shared definitions, shared payload/data keys, and generic HUD path lookups replaced Steal A Pet-only enums. |
| Runtime verification | Not applicable | No live Studio verification was performed in this task. |

## Faithful Clone Status

`Pass, source-compatible`

The active persistence shape, mail serialization, request flow, copied UI asset, and player-facing open/list/select/claim loop were preserved. The resulting module is not yet fully standalone because reward resolution, prompt dispatch, and exact editor-owned UI registration were intentionally isolated.

## Runtime Verification

Serialized clone completed.
Runtime Studio verification was not performed.
