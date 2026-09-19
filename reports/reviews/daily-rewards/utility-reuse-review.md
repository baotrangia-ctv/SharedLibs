# Utility Reuse Review

**Result:** Reuse existing utility.

- Persistence/list encoding uses `Assets/Scripts/Utils/DataUtils.fcg` APIs
  `JsonStringToListKeyValueV2`, `ListKeyValueToJsonString`,
  `StringToListIntV2`, and `ListIntToString`.
- Integer parsing uses engine `Convert.fcc` via the existing `StringToInt`
  contract; no feature parser was duplicated.
- Source `TimeManager` was not copied wholesale. Only the required GMT offsets,
  server timestamp, and day-index behavior were isolated in
  `DailyRewardsTime.fcg`, because the target has no equivalent time manager and
  the source debug/weekend/event APIs are outside this feature.
- Reward value brace handling is feature-local in `MailConfigs` because it is
  target CSV schema compatibility, not a generic DataUtils concern.

