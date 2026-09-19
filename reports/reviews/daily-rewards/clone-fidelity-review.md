# Clone Fidelity Review

**Result:** Pass with runtime verification pending.

Evidence: source `ActivitiesManager.fcg:380-526`, `ActivitiesConfigs.fcg:65-226`,
and `DailyRewards.csv` were compared with target `DailyRewardsManager.fcg`,
`DailyRewardsConfigs.fcg`, and the imported CSV. The 35-row CSV hash matches
byte-for-byte. Seven-day streak refresh, can-claim/claimed derivation, mail
check/receive, load retry, readiness, save, and cache clear are present.

The source-only PlayersManager/RebirthManager/HudActivities bindings are
explicitly isolated behind `SetUserType`, `ResetRevivalRewardCycle`, the
`rebirthLevel` parameter, `SetLastLoginDeltaSeconds`, and returned status
strings. The separate Lucky Spin `DailyRewardManager` is classified as adjacent,
not silently omitted from this core scope. No unknown serialized values were
discarded.

**Corrective finding resolved:** source `ActivitiesManager.fcg:289-305` resets
`_LoginStreaks`/`_CanClaimDates`/`_ClaimedDates` on day-change when the user is
`Revival` and the previous-login delta is greater than
`REVIVAL_REWARD_RESET_SECONDS` (1209600 seconds). Target
`DailyRewardsManager.fcg:252-276` now performs the same branch using the
consumer-provided transient `SetLastLoginDeltaSeconds` hook, without importing
`PlayersManager`. The hook is consumed after the day-change decision and reset
to zero, then `UpdateLoginStreak` runs exactly as in source. The existing
`DailyRewardsDefinitions.REVIVAL_REWARD_RESET_SECONDS` is now live code.

**Portability:** Pass with consumer adapters. **Runtime:** Studio build passed;
live player claim/reconnect verification remains pending.
