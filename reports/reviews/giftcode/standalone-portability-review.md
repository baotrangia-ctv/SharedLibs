# Giftcode Standalone Portability Review

Status: `Standalone with optional integrations`.

| Dependency | Required? | Handling |
| --- | --- | --- |
| `DatabaseController` | Required | Reused from target CoreLib. |
| `DataUtils` | Required | Reused from target Utils; no duplicate parser added. |
| `MailsDefinitions` / `StatusCodes` | Required | Reused target definitions. |
| Registered target `Gifts.csv` | Required | Existing target registration and `EResCSV.Gifts` preserved. |
| `RebirthManager` | Optional/source-specific | Consumer-provided eligibility adapter; not copied. |
| `PetsManager` | Optional/source-specific | Consumer reward-slot check; not copied. |
| `HudGiftCode` / `GiftCode.ui` | Optional | Consumer-owned UI integration. |
| Source localization and prompt events | Optional | Consumer feedback layer. |
| Source accumulation quota service | Unresolved/optional | No active source validation call-site; deferred rather than invented. |

No strict MCP blocker applies. Repository evidence was sufficient for the core
clone; live editor state is only needed for a consumer UI/registration stage.

