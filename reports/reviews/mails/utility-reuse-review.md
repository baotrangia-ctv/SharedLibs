# Mails Utility Reuse Review

Date: 2026-07-27
Module: `mails`

Recommendation: `Reuse existing utility`

- `Assets/Scripts/Managers/MailsManager.fcg` reuses `Assets/Scripts/Utils/DataUtils.fcg` for:
  - `JsonStringToListKeyValueV2`
  - `ListKeyValueToJsonString`
  - `StringToListIntV2`
  - `StringToListStringV2`
  - `ListStringToStringUseComma`
  - `ListIntToString`
- No duplicate `MailsDataUtils` file was introduced.
- Reward-shape cleanup remains feature-local inside `MailsManager.fcg` because it reflects Mails business rules rather than shared serialization behavior.
