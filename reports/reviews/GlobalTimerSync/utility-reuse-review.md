# GlobalTimerSync Utility Reuse Review

**Result:** `Remove duplicate` + `Extend existing utility`

## Decisions

| Helper / behavior | Existing evidence | Decision | Rationale |
| --- | --- | --- | --- |
| GMT region map and server-time anchor | Existing `Assets/Scripts/Utils/DailyRewardsTime.fcg`; source `TimeManager.fcg:9-24,92-150` | Remove duplicate; extend canonical target time utility | `DailyRewardsTime` had only a subset; `GlobalTimerSync` needs `GetHMS`/`GetTimeGMT`. One target `TimeManager` now owns the shared anchor surface. |
| Wave list arithmetic | No compatible target helper | Keep feature-local in `GlobalTimerSync.fcg` | Modulo over duration lists is the feature's public behavior, not JSON/list encoding. |
| Structured-data parsing/serialization | `Assets/Scripts/Utils/DataUtils.fcg` | Reuse existing utility not applicable | The module does not parse, serialize, migrate, split, or join data. |

The existing `DailyRewardsTime.GetCurrentTimestamp` and
`GetDayIndexGMT` signatures remain intact. No DataUtils wrapper or duplicate
conversion helper was added.
