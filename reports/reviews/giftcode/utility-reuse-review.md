# Giftcode Utility Reuse Review

| Concern | Existing utility/API | Decision |
| --- | --- | --- |
| Gift CSV parsing | `CSVData.ReadCSV` plus `DataUtils.JsonStringToListKeyValueV2` in target `MailConfigs` | Reuse existing utility. |
| Reward value normalization | Target `MailConfigs` and `MailsManager.CleanMailData` | Keep feature-local because it is tied to mail/gift schema. |
| Mail persistence serialization | Target `DataUtils.ListKeyValueToJsonString`, list conversion helpers | Reuse existing utility. |
| Time-window calculation | Target `MailsManager.IsValidStartTime/IsValidEndTime` | Keep feature-local; it expresses Giftcode business rules. |
| Source `StringToListIntV2` reward IDs | No direct target equivalent needed | Not copied; target stores structured reward objects. |

No duplicate generic parser or conversion wrapper was introduced.

