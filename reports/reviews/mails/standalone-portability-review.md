# Mails Standalone Portability Review

Date: 2026-07-27
Module: `mails`
Portability status: `Consumer adaptation required`

| Dependency | Required | Handling | Evidence |
| --- | --- | --- | --- |
| `Assets/Scripts/CoreLib/DatabaseController.fcg` | Required | Reuse target equivalent | SharedLibs already contains the same database controller pattern. |
| `Assets/Scripts/Utils/DataUtils.fcg` | Required | Reuse target equivalent | Shared manager uses existing JSON/list helpers instead of cloning Steal A Pet utilities. |
| `RewardManager.ClaimReward` | Required for reward granting | Abstract as integration point | Shared claim flow now returns claimed mail data and leaves reward application to the consumer. |
| Pet-slot checks from `PetsManager` | Optional for generic mail | Source-specific and excluded | Claim gating was isolated because SharedLibs has no generic pet inventory contract yet. |
| Prompt and analytics dispatch | Optional | Source-specific and excluded | `OnShowPrompt`, `OnReadMail`, and tracking calls were not copied into the shared manager. |
| Generated UI enums and resource maps | Required for exact source HUD code | Replaced with path-based UI lookup | Shared HUD uses `CreateCustomUI(... as CustomUIAssetID)` and `GetWidgetByPath` instead of Steal A Pet `EResKey*` enums. |
| Editor-owned UI registration and bindings | Required for live runtime parity | Runtime verification pending | Readable UI asset was copied, but Studio/editor validation was not performed in this task. |

Stage summary:

- Shared refactor: `Complete`
- Runtime verification: `Not applicable`
