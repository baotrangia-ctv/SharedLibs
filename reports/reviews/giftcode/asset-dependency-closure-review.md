# Giftcode Asset Dependency Closure Review

| Dependency | Source evidence | Target handling | Classification |
| --- | --- | --- | --- |
| Giftcode config CSV | `Assets/Scripts/Configs/MailConfigs.fcg`, `Assets/CSV/giftcode.csv` | Reuse target `Assets/CSV/Mails/Gifts.csv` and registered `EResCSV.Gifts`. | Reuse target equivalent; schema adapted. |
| Mails database | `MailsManager.fcg:109-165,331-403` | Reuse target `DatabaseController` and `MailsDefinitions`. | Already exists in target. |
| Structured-data parsing | Source `DataUtils` call-sites | Reuse target `Assets/Scripts/Utils/DataUtils.fcg`. | Already exists in target. |
| Rebirth eligibility | `PlayerGiftCode.fcg:30`, `MailsManager.fcg:780-795` | Consumer adapter only. | Source-specific and isolated. |
| Pet slot validation | `PlayerGiftCode.fcg:72-91` | Consumer reward/UI layer only. | Source-specific and excluded. |
| Prompt/read-mail events | `MailsManager.fcg:488-497` | Consumer feedback adapter. | Source-specific and isolated. |
| Giftcode UI and menu route | `HudGiftCode.fcg`, `CustomUIUtils.fcg:560-572`, `GiftCode.ui` | Not copied for core request. | Consumer integration point. |
| Icon/localization | `GiftcodeIconTemp.png`, `Localization/key.csv` | Not copied for core request. | Optional visual/presentation asset. |
| Engine FC libraries | `Map.fcc`, `List.fcc`, `Database.fcc`, `StdLibrary.fcc` | Resolved by target toolchain. | Engine/library reference. |

The closure is complete for the target core Manager/config/persistence path. No
required missing filesystem dependency or strict MCP blocker was found.

