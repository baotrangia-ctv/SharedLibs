# Active API Surface Review

**Result:** Latest active surface selected; adjacent APIs isolated.

| API/surface | Classification | Evidence |
| --- | --- | --- |
| `ActivitiesManager.GetDailyRewardsV2` | Latest active source lookup | Source `ActivitiesManager.fcg:394` and `HudActivities` daily tab |
| `ActivitiesManager.GetDailyRewards` | Active wrapper | Source `ActivitiesManager.fcg:380`; requires source RebirthManager |
| `ActivitiesManager.Request/Check/ProcessClaimDailyReward` | Active claim contract | Source lines 456, 483, 526 |
| `DailyRewardManager` spin/milestone APIs | Active adjacent, not Daily Rewards | Source `HudActivities` lines 418, 1045 and separate manager file |
| target `DailyRewardsManager` APIs | Shared contract | New portable surface with explicit rebirth/status parameters |

No deprecated or commented Daily Rewards version was selected. The source
wrapper/V2 distinction is represented by one explicit target API rather than
inventing a source-only provider call.

