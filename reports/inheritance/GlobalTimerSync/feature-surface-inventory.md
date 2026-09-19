# GlobalTimerSync Feature Surface Inventory

| Source artifact | Responsibility | Active status | Evidence label | Clone classification | Binding classification | Stage status | Portability impact | Target layer | Target handling |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `Assets/Scripts/Manager/WeatherManager.fcg:40-91` | Region-adjusted wall-time wave selection and remaining milliseconds for Weather | Latest active | Verified from source script | Reusable after dependency isolation | Consumer integration point | Complete with unresolved bindings | Consumer supplies wave durations from `WeatherConfigs` | `Assets/Scripts/Utils/GlobalTimerSync.fcg` | Common modulo/wave-resolution behavior extracted behind one public API; Weather manager is not copied |
| `Assets/Scripts/Manager/RotationShopManager.fcg:43-78` | Fixed-epoch wave selection and remaining milliseconds for Rotation Shop | Latest active | Verified from source script | Reusable after dependency isolation | Consumer integration point | Complete with unresolved bindings | Consumer supplies wave durations and epoch override/default | `Assets/Scripts/Utils/GlobalTimerSync.fcg` | FixedEpoch branch preserves the source shape; Rotation Shop epoch is exposed through definitions |
| `Assets/Scripts/Manager/GlobalSpawnPet.fcg:56-78` | Region-adjusted countdown for Mythic/Apex spawn intervals | Latest active | Verified from source script | Reusable after dependency isolation | Consumer integration point | Complete with unresolved bindings | Consumer supplies one interval duration and the existing start phase | `Assets/Scripts/Utils/GlobalTimerSync.fcg` | Normalized as a one-duration wave list with a region anchor phase; spawn UI and pet side effects remain consumer-owned |
| `Assets/Scripts/Manager/TimeManager.fcg:9-24,92-150` | GMT region map and server-time anchor helpers | Active dependency | Verified from source script | Reusable after dependency isolation | Source-specific and isolatable | Complete | Engine server time and region remain runtime-provided | `Assets/Scripts/Utils/TimeManager.fcg` | Preserve the required anchor surface (`GMTREGION`, `GetCurrentTimestamp`, `GetHMS`, `GetTimeGMT`, plus day-index compatibility) without copying unrelated Flags/weekend APIs |
| `Assets/Scripts/Configs/WeatherConfigs.fcg:102-116,255-271` | Weather wave types, durations, total duration | Latest active | Verified from source script | Consumer integration point | Requires remapping | Not applicable | Consumer must pass durations in milliseconds | None cloned | Public API accepts `List<int>`; source config remains outside SharedLibs core |
| `Assets/Scripts/Configs/RotationShopConfigs.fcg:47-59,95-105` | Rotation wave durations and total duration | Latest active | Verified from source script | Consumer integration point | Requires remapping | Not applicable | Consumer must pass durations in milliseconds | None cloned | Public API accepts the complete duration list; source config remains outside SharedLibs core |
| `Assets/Scripts/Manager/WeatherManager.fcg` | Weather change effects, skybox, events, debug weather, player summon | Latest active | Verified from source script | Source-specific dependency | Source-specific and excluded | Not applicable | Consumer-owned integration | None cloned | Only synchronization API is in scope; no simplified Weather manager is invented |
| `Assets/Scripts/Manager/RotationShopManager.fcg` | Stock mutation, purchase flow, prompts, wallet/mail integrations | Latest active | Verified from source script | Source-specific dependency | Source-specific and excluded | Not applicable | Consumer-owned integration | None cloned | Only synchronization API is in scope |
| `Assets/Scripts/Manager/GlobalSpawnPet.fcg` | Spawn pet selection, parade, HUD countdown, scene/UI assets | Latest active | Verified from source script | Source-specific dependency | Source-specific and excluded | Not applicable | Consumer-owned integration | None cloned | No UI, scene, texture, or pet side-effect asset is copied |
| `Assets/Scripts/Manager/EventKickBallManager.fcg`, `EventMeteoriteManager.fcg`, `EventMoleManager.fcg`, `EventStealABallManager.fcg` | Adjacent global-wave implementations using related patterns | Active adjacent | Verified from source script | Source-specific dependency | Compatibility-only / out of scope | Not applicable | Future consumers may reuse the shared API separately | None cloned | User scope names Weather, Rotation Shop, and Global Spawn Pet only; adjacent events are not silently merged |
| `Assets/Scripts/Utils/DailyRewardsTime.fcg` (target) | Existing narrow GMT day-index utility | Latest target utility | Verified from source script | Reusable after dependency isolation | Existing target utility | Complete | Must retain existing day-index API | `Assets/Scripts/Utils/DailyRewardsTime.fcg` | Delegate its time/day-index behavior to the new canonical target `TimeManager` utility to avoid a second GMT map |
| `Assets/Scripts/Configs/GlobalTimerSyncDefinitions.fcg` (target) | Shared anchor modes and overridable Rotation Shop epoch example | Added public contract | Verified from config | Reusable as-is | Shared public definition | Complete | Consumers use shared values instead of duplicated literals | `Assets/Scripts/Configs/GlobalTimerSyncDefinitions.fcg` | Own the cross-consumer mode/epoch definitions under the target Configs layer |

## Public contract

```text
GetGlobalWaveState(anchorMode, waveDurations, epochOffset?, out waveIndex, out durationLeftMs)
```

The FC implementation represents the optional `epochOffset?` as a nullable
`object` parameter because the verified FC function-signature syntax has no
optional/default-parameter form. Values are seconds: for `FixedEpoch`, the
offset is the fixed epoch subtracted from server time; for `RegionAdjusted`, a
consumer may pass a signed phase offset such as Global Spawn Pet's existing
`START_SECOND`. `nil` means no phase offset for RegionAdjusted and the
Rotation Shop example/default epoch for FixedEpoch.

## Boundary decisions

- No persistence, database registration, config CSV, HUD script, serialized UI,
  texture, localization, custom component, or custom enum is part of the core
  closure.
- The source managers' business and presentation behavior stays in consumers.
- The source `GlobalSpawnPet` method has one repeated interval rather than an
  explicit multi-wave config; it is represented as a one-element duration list,
  preserving its modulo countdown and `START_SECOND` phase without creating a
  second synchronization family.
