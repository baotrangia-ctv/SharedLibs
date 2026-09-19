# Giftcode Folder Architecture Review

| Responsibility | Current location | Decision |
| --- | --- | --- |
| Authoritative redeem/mail logic | `Assets/Scripts/Managers/MailsManager.fcg` | Retain; matches Manager convention. |
| Gift/mail config reader | `Assets/Scripts/Configs/MailConfigs.fcg` | Retain; shared with mail consumers. |
| Field/status/persistence definitions | `Assets/Scripts/Consts/MailsDefinitions.fcg`, `StatusCodes.fcg` | Retain; definitions are already shared by Manager and HUD. |
| Structured-data helpers | `Assets/Scripts/Utils/DataUtils.fcg` | Reuse; no feature-local duplicate. |
| Giftcode CSV | `Assets/CSV/Mails/Gifts.csv` | Retain under the existing Mails asset grouping. |
| Reports | `reports/inheritance/giftcode/`, `reports/reviews/giftcode/` | Retain; outside source/target code layers. |
| Source Giftcode HUD | Source `Assets/HUDs/` and `Assets/Scripts/HUDs/` | Omit from core; consumer may add it under the target HUD layer. |

No file mixes Manager, HUD, Config, and Utils responsibilities in the target
changes.

