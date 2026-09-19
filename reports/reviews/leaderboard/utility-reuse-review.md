# Utility reuse review

No structured parsing, serialization, conversion, or migration helper was introduced.
The target uses confirmed standard `List.Clone`, `List.Length`, and Map access
semantics. `Assets/Scripts/Utils/DataUtils.fcg` does not provide behavior needed by the
leaderboard row/query contract, so adding a wrapper or extending `DataUtils` would be
unnecessary.

Decision: `Keep feature-local` for mock row construction and money-score formatting
when the HUD stage is completed.
