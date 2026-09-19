# GlobalTimerSync Static Definitions Review

**Result:** `Move to shared definitions` was applied before completion.

| Definition | Declaration | Recommendation | Evidence / compatibility |
| --- | --- | --- | --- |
| `ANCHOR_MODE_REGION_ADJUSTED` | `Assets/Scripts/Configs/GlobalTimerSyncDefinitions.fcg:5` | Move to shared definitions | Used by every RegionAdjusted consumer |
| `ANCHOR_MODE_FIXED_EPOCH` | `Assets/Scripts/Configs/GlobalTimerSyncDefinitions.fcg:6` | Move to shared definitions | Used by every FixedEpoch consumer |
| `DEFAULT_FIXED_EPOCH_OFFSET = 1776880800` | `Assets/Scripts/Configs/GlobalTimerSyncDefinitions.fcg:9` | Move to shared definitions | Rotation Shop example/default remains overrideable and outside the core algorithm |
| `MILLISECONDS_PER_SECOND`, `SECONDS_PER_HOUR`, `SECONDS_PER_MINUTE` | `Assets/Scripts/Utils/GlobalTimerSync.fcg:11-13` | Keep private in utility | Used only by the generic anchor calculation; no cross-module contract needed |

The public mode values and epoch example are cohesive cross-boundary definitions;
they are not duplicated in Weather, Rotation Shop, or Global Spawn consumers. No
persisted or editor-generated numeric value was changed.
