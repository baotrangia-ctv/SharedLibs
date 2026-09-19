---
name: GlobalTimerSync-source-to-shared
description: Inherit the Steal A Pet global countdown synchronization core into SharedLibs while preserving region-adjusted and fixed-epoch anchors behind one public wave-state API.
---

# Purpose

Use this skill when inheriting `GlobalTimerSync` from `D:\Craftland\StealAPet`
into `D:\Craftland\_Libs\SharedLibs`.

## Required policy references

Load the source-to-shared router and the shared inheritance references before
implementation. Always apply repository-first discovery, Faithful Clone Mode,
preserve-first bindings, stage-based completion, standalone portability, and
runtime-verification separation. Load dependency-closure and clone-fidelity
references when those stages begin. Use `review-inherited-module` sections:

- Clone Fidelity
- Standalone Portability
- Feature Completeness
- Folder Architecture
- Utility Reuse

Also use Asset Dependency Closure and Static Definitions for this module.

## Module surface

The active source surface is:

- `Assets/Scripts/Manager/WeatherManager.fcg:GetGlobalWeatherWave`
- `Assets/Scripts/Manager/RotationShopManager.fcg:GetGlobalRSWave`
- `Assets/Scripts/Manager/GlobalSpawnPet.fcg:GetSpawnPetWave`
- `Assets/Scripts/Manager/TimeManager.fcg` anchor helpers and `GMTREGION`

Weather and Global Spawn Pet use the RegionAdjusted wall-time anchor. Rotation
Shop uses FixedEpoch. The wave-resolution algorithm is shared: calculate elapsed
time, modulo the sum of durations, resolve the current wave, and return the
remaining milliseconds. Do not split this into DailySync and MilestoneSync APIs.

## Public contract

Expose exactly one general API:

```text
GetGlobalWaveState(anchorMode, waveDurations, epochOffset?, out waveIndex, out durationLeftMs)
```

The FC implementation uses a nullable `object` for `epochOffset?` because the
verified FC grammar has no optional/default-parameter syntax. Durations and the
result are milliseconds; anchor/phase offsets are seconds. `RegionAdjusted`
reuses `TimeManager.GetHMS`, which preserves `GetTimeGMT` and `GMTREGION`.
`FixedEpoch` subtracts `TimeManager.GetCurrentTimestamp()` from the supplied
epoch. Keep `1776880800` in a shared definition as the Rotation Shop example or
default input; never embed it as an unoverrideable literal in the core.

## Faithful clone and portability rules

- Preserve the required `TimeManager` anchor surface; isolate unrelated source
  Flags, weekend, date-formatting, and business APIs.
- Represent Global Spawn Pet's repeated interval as a one-element duration list
  and pass its existing `START_SECOND` as a RegionAdjusted phase offset.
- Keep Weather, Rotation Shop, and Global Spawn Pet Managers, configs, events,
  persistence, UI, scene assets, textures, and pet/shop/weather side effects as
  consumer integration points.
- Reuse existing target time utilities where compatible. Do not duplicate GMT
  maps or add DataUtils-style conversion helpers.
- Preserve target folder layers: generic timing in `Assets/Scripts/Utils/`,
  public definitions in `Assets/Scripts/Configs/`, and evidence in `reports/`.
- Do not claim runtime success from serialized/source fidelity. Run full FC
  compile after `.fcg`/`.fcc` edits and report live Studio verification separately.

## Completion evidence

Record the feature-surface inventory, dependency closure, source/target mapping,
preserved values, intentional boundary normalization, consumer obligations, FC
compiler result, runtime status, and the required review reports under:

- `reports/inheritance/GlobalTimerSync/`
- `reports/reviews/GlobalTimerSync/`

After a completed source-to-shared inheritance, generate the paired
`GlobalTimerSync-shared-to-consumer` skill from this contract and dependency
evidence without requiring a new source-project read.
