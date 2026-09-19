# GlobalTimerSync Clone Fidelity Review

**Result:** `Pass, source-compatible`  
**Portability:** `Standalone with optional integrations`  
**Runtime:** `Not performed`

## Evidence comparison

| Source behavior | Evidence | Target handling | Status |
| --- | --- | --- | --- |
| Weather uses local region-adjusted wall time, modulo total wave duration, then resolves the current wave and remaining milliseconds | `Assets/Scripts/Manager/WeatherManager.fcg:73-91` | `GlobalTimerSync.GetGlobalWaveState` with RegionAdjusted and a millisecond duration list | Preserved |
| Rotation Shop subtracts `1776880800`, modulo total duration, then resolves wave and remaining milliseconds | `Assets/Scripts/Manager/RotationShopManager.fcg:62-78` | FixedEpoch branch; default epoch moved to `GlobalTimerSyncDefinitions` and remains overrideable | Preserved with explicit configuration |
| Global Spawn Pet uses region-adjusted local time plus `START_SECOND`, modulo one repeated interval, and returns time to the next boundary | `Assets/Scripts/Manager/GlobalSpawnPet.fcg:70-78` | One-duration `waveDurations` list plus signed RegionAdjusted phase offset | Preserved as a specialization |
| Region map and time helpers | `Assets/Scripts/Manager/TimeManager.fcg:9-24,92-150` | Required anchor surface copied to target `Utils/TimeManager.fcg`; unrelated Flags/weekend APIs excluded | Preserved after dependency isolation |

## Boundary finding

The source Weather and Rotation helpers expose a zero-duration transient at an
exact wave boundary (`wave = 0`/current wave with `durationLeft = 0`), after which
their processing loops advance to wave 1 or the next wave. The shared public
contract intentionally returns a one-based current wave and its full remaining
duration at that boundary. This is an explicit Stage B contract normalization,
not a new Daily/Milestone synchronization model, and does not change the
observable restart schedule.

## Omission and preservation review

- Preserved: anchor modes, modulo cycle, duration units, wave ordering, restart
  behavior, `GMTREGION`, `GetCurrentTimestamp`, `GetTimeGMT`, and `GetHMS`.
- Out-of-scope target utility: `Assets/Scripts/Utils/DailyRewardsTime.fcg` was
  not cloned, modified, or made dependent on `GlobalTimerSync`; its original
  self-contained `GMTREGION` implementation remains intact for
  `DailyRewardsManager` and `DailyMissionsManager`.
- Intentionally omitted: source manager side effects, source configs/CSV, UI,
  scene assets, pet/shop/weather business flows, persistence, and unrelated
  TimeManager Flags/weekend features.
- Unknown serialized values: none.
- Remapped IDs: none.
- Deprecated/duplicate named implementation: none found.

The target FC source compiled successfully with the configured external compiler.
