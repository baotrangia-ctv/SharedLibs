# GlobalTimerSync Inheritance Report

## 1. Module / roots

- Module: `GlobalTimerSync`.
- Source: `D:\Craftland\StealAPet` (read-only).
- Target: `D:\Craftland\_Libs\SharedLibs` (read-write).
- Route: `source-to-shared-router`.
- Intake: `reports/inheritance/GlobalTimerSync/00-intake.md`.
- Complexity Gate: `Complex`; approved Phase Plan was followed.

## 2. Repository evidence and active implementation

Inspected the source `AGENTS.md`, `Docs/CODE_CONVENTIONS.md`,
`Docs/BusinessLogic/README.md`, `12-pet-weather.md`, `31-shop-trading.md`,
`92-time-activities-flags.md`, `95-shared-infra.md`, the FC workflow, the
source `TimeManager.fcg`, `WeatherManager.fcg`, `RotationShopManager.fcg`,
`GlobalSpawnPet.fcg`, the two wave config readers, exact call sites, and target
SharedLibs utilities.

The selected active implementations are:

- `WeatherManager.fcg:GetGlobalWeatherWave` at source lines 73-91.
- `RotationShopManager.fcg:GetGlobalRSWave` at source lines 62-78.
- `GlobalSpawnPet.fcg:GetSpawnPetWave` at source lines 70-78.
- `TimeManager.fcg` anchor surface at source lines 9-24 and 92-150.

Git history confirms these are the only named implementations in the validated
source tree; no duplicate `TimeManager`, `WeatherManager`, `RotationShopManager`,
or `GlobalSpawnPet` source path was found.

Adjacent `EventKickBallManager`, `EventMeteoriteManager`, `EventMoleManager`,
and `EventStealABallManager` wave helpers were identified but excluded because
they are not part of the requested module scope.

## 3. Source files cloned / target files created

- `Assets/Scripts/Utils/GlobalTimerSync.fcg`
  - One public `GetGlobalWaveState` API.
  - Shared modulo, wave-index, and remaining-milliseconds resolution.
  - `RegionAdjusted` and `FixedEpoch` switch.
- `Assets/Scripts/Utils/TimeManager.fcg`
  - Preserved `GMTREGION`, `GetCurrentTimestamp`, `GetTimeGMT`, `GetHMS`,
    and compatible day-index/debug anchor behavior.
- `Assets/Scripts/Configs/GlobalTimerSyncDefinitions.fcg`
  - Public anchor mode identifiers and the overridable Rotation Shop example
    epoch `1776880800`.

`Assets/Scripts/Utils/DailyRewardsTime.fcg` is outside the GlobalTimerSync
scope and was not cloned or modified. Its self-contained `GMTREGION`
implementation remains intact for the existing Daily Rewards and Daily
Missions consumers.

## 4. Source files omitted

- Full Weather, Rotation Shop, and Global Spawn Pet Managers: source-specific
  effects, shop/pet business logic, persistence/currency/mail, prompts, UI,
  scene entities, and event side effects remain consumer-owned.
- Weather and Rotation Shop configs/CSV: their wave durations are inputs to the
  shared public contract, not owned by the generic utility.
- Global Spawn Pet HUD and scene assets: no serialized asset is required by the
  timing core.
- Adjacent event wave managers: out of requested scope, not silently deleted.

## 5. Serialized assets and IDs

- No `.eca`, UI, scene, prefab, texture, localization, custom component, or
  asset registration is part of this module.
- The changed files are direct `.fcg` text sources and were validated by the FC
  compiler.
- Entity IDs, asset IDs, generated `ERes*` symbols, and serialized bindings were
  not copied, remapped, or invented.

## 6. Dependency closure

| Dependency | Status | Handling |
| --- | --- | --- |
| FC `List.fcc` | Required | Reused engine library; confirmed by target compiler/source declarations |
| FC `Map.fcc` | Required by `TimeManager` | Reused engine library; confirmed by source declarations |
| FC `StdLibrary.fcc` | Required | Reused engine library; `GetServerTimestamp` and `GetServerRegion` verified |
| `EditorGenLib.fcc` | Required import convention | Reused target project generated library; no generated file edited |
| Source `TimeManager.fcg` Flags/DataUtils/weekend dependencies | Not required | Isolated; only anchor surface copied |
| Source Weather/Rotation/Global Spawn Managers | Optional consumer integration | Not copied; consumers pass duration lists and offsets |
| Target `DailyRewardsTime.fcg` | Existing shipped utility outside scope | Out of scope / untouched; self-contained GMT map and public methods remain unchanged; no dependency on GlobalTimerSync |

No missing mandatory dependency or strict MCP blocker exists.

## 7. Public API fidelity

The target exposes one general API:

```text
GetGlobalWaveState(anchorMode, waveDurations, epochOffset?, out waveIndex, out durationLeftMs)
```

FC has no verified optional-parameter syntax, so `epochOffset?` is represented
as nullable `object`: pass `nil` for the default/no-offset case, or pass an
integer number of seconds. For `FixedEpoch`, the value is subtracted from the
current timestamp. For `RegionAdjusted`, it is a signed phase offset, preserving
Global Spawn Pet's existing `START_SECOND` without creating another sync family.

The fixed-epoch default is defined outside the core in
`GlobalTimerSyncDefinitions.DEFAULT_FIXED_EPOCH_OFFSET`; consumers may override
it by passing another value. The literal `1776880800` is not embedded in the
wave algorithm.

## 8. Faithful clone and Stage B changes

- Source modulo behavior and millisecond unit conversion are preserved.
- Weather and Rotation duration resolution is generalized from config getters to
  a consumer-supplied `List<int>`.
- Global Spawn Pet is represented as a one-duration wave list plus its existing
  region phase offset; its pet selection, HUD countdown, and effects are not
  moved into SharedLibs.
- The public boundary is normalized to one-based `waveIndex` with a full first
  wave duration at an exact cycle boundary. This removes the source managers'
  zero-duration transient return while preserving the observable restart at
  wave 1 requested by the contract.
- `DailyRewardsTime` is outside this module's scope and was not changed; its
  original self-contained GMT implementation remains independent.

## 9. Lifecycle, config, CSV, events, and presentation

- Persistence: Not applicable.
- Database registration/readiness/reconnect/save: Not applicable.
- Request/Check/Process actions: Not applicable.
- Config/CSV loading: Not applicable to the core; consumers own wave data.
- Events/callbacks: Not applicable to the core.
- HUD/serialized UI/textures/localization: Not applicable.
- Runtime clock and region remain engine-provided integrations.

## 10. Validation and MCP

- Full local FC compile: passed with exit code `0`.
- Compiler: `C:\Users\giabao.tran\AppData\Local\Programs\Craftland Studio\resources\LocalData\Utilities\UGCLanguage\release\fccompile_external.exe`.
- The compiler is an older version and rejected `-agent`/`-session`; the required
  fallback command without those flags passed.
- Only pre-existing deprecated-symbol warnings in
  `Assets/Scripts/HUDs/HudControls.fcg` remain.
- Craftland Studio MCP was not used. No editor-owned asset, UI, scene, or script
  attachment changed, so local FC compilation is sufficient for this text-only
  change.
- Runtime verification: Not performed; live Studio clock/region behavior remains
  a separate verification status.

## 11. Reviews

Completed under `review-inherited-module`:

- `reports/reviews/GlobalTimerSync/clone-fidelity-review.md`
- `reports/reviews/GlobalTimerSync/standalone-portability-review.md`
- `reports/reviews/GlobalTimerSync/feature-completeness-review.md`
- `reports/reviews/GlobalTimerSync/folder-architecture-review.md`
- `reports/reviews/GlobalTimerSync/utility-reuse-review.md`
- `reports/reviews/GlobalTimerSync/asset-dependency-closure-review.md`
- `reports/reviews/GlobalTimerSync/static-definitions-review.md`

## 12. Stage summary

| Stage | Result |
| --- | --- |
| Intake/router/reference gate | Complete |
| Path validation | Complete |
| Source discovery / active implementation | Complete |
| Feature-surface inventory | Complete |
| Stage A faithful algorithm/anchor clone | Complete with documented consumer bindings |
| Dependency closure | Complete |
| Stage B shared refactor | Complete |
| FC full compile | Complete |
| Runtime Studio verification | Not performed |
| Auto-pair skill generation | Complete |

## 13. Final independent statuses

- Faithful clone: `Source-compatible`.
- Clone fidelity: `Pass, source-compatible`.
- Standalone portability: `Standalone with optional integrations`.
- Runtime verification: `Not performed`.
- Exact MCP blockers: none.

## 14. Remaining consumer work

Consumers must import `GlobalTimerSync`, build their duration list in
milliseconds, pass `GlobalTimerSyncDefinitions.ANCHOR_MODE_REGION_ADJUSTED` for
Weather and Global Spawn Pet, pass `ANCHOR_MODE_FIXED_EPOCH` for Rotation Shop,
and pass the Rotation Shop default or an explicit override. They retain all
business logic, events, UI, persistence, and source-specific debug behavior.
