# Asset dependency closure review — Daily Missions

Status: **Pass for the requested core**.

The dependency closure is: `DailyMissionsManager` → `DailyMissionsConfigs` / `DailyMissionMilestonesConfigs` → registered CSV resources, plus target `DatabaseController`, `DataUtils`, and `DailyRewardsTime`. The module has no texture or scene dependency. Reward and mail assets are consumer-owned because the shared core returns neutral reward data and milestone gift IDs.

