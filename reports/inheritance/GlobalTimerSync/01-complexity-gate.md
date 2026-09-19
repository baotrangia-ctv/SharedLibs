# Complexity Gate: GlobalTimerSync

## Result

- Status: `Complex`
- Gate reason: the module contains network/server-time synchronization.
- Approval state: `Pending user approval`
- Implementation state: `Not started`
- Force keyword: not supplied.

Per `.agent/INDEX.md` and `source-to-shared-router`, implementation pauses here
until the user approves this Phase Plan.

## Scope and contract to preserve

The inherited module must preserve one shared countdown algorithm for all three
known consumers:

1. Compute elapsed time from the selected anchor.
2. Apply modulo by the sum of all wave durations.
3. Resolve the current wave index and remaining duration in milliseconds.
4. Restart at wave 1 after the total duration, with the same behavior for
   Weather, Rotation Shop, and Global Spawn Pet Mythic/Apex.

The public contract is one general API, not separate consumer-specific APIs:

```text
GetGlobalWaveState(anchorMode, waveDurations, epochOffset?)
    -> (waveIndex, durationLeftMs)
```

`anchorMode` switches between `RegionAdjusted` and `FixedEpoch`. The
`RegionAdjusted` path must reuse the existing `TimeManager.fcg` logic and
bindings (`GetCurrentTimestamp`, `GetHMS`, `GetTimeGMT`, and `GMTREGION`). The
`FixedEpoch` path must preserve the Rotation Shop reference epoch
`1776880800` as a consumer example/default input that can be overridden; the
core `GlobalTimerSync` implementation must not embed that literal as an
unconfigurable constant.

## Proposed phases

### Phase 1 — Repository-first discovery and dependency closure

- Read the official FC workflow before opening or editing `.fcg`/`.fcc` files.
- Identify the latest active implementations and call sites for:
  - `WeatherManager.fcg:GetGlobalWeatherWave`
  - `RotationShopManager.fcg:GetGlobalRSWave`
  - `GlobalSpawnPet.fcg:GetSpawnPetWave`
  - the `TimeManager.fcg` anchor functions and `GMTREGION` definitions
- Inventory exact signatures, units, wave-duration inputs, index conventions,
  restart behavior, and all transitive script/config/utility dependencies.
- Search source and SharedLibs definitions before considering any adaptation or
  MCP use.

### Phase 2 — Stage A faithful clone

- Clone the active source behavior and dependency closure with no algorithmic
  redesign.
- Preserve the existing `TimeManager.fcg` anchor logic and structurally valid
  bindings; classify source-only and consumer integration points explicitly.
- Verify the three named consumer flows against the source before genericizing.
- Record Stage A as source-compatible and separately track any runtime gap.

### Phase 3 — Stage B shared refactor and public contract

- Extract the common modulo/wave-resolution core behind the single
  `GetGlobalWaveState` API.
- Add an explicit anchor-mode switch for `RegionAdjusted` and `FixedEpoch`.
- Keep epoch selection injectable/overridable; preserve `1776880800` in the
  Rotation Shop consumer/config example rather than hardcoding it in the core.
- Reuse `TimeManager` instead of duplicating `GetCurrentTimestamp`, `GetHMS`,
  `GetTimeGMT`, or `GMTREGION` logic.
- Update the three consumers only at their integration points, preserving their
  observable wave and duration-left behavior.

### Phase 4 — Validation and required reviews

- Run FC compilation validation (`fccompile.exe -i Assets`, or equivalent
  Craftland Studio build validation) for every `.fcg`/`.fcc` change.
- Produce the required `review-inherited-module` sections:
  - Clone Fidelity
  - Standalone Portability
  - Feature Completeness
  - Folder Architecture
  - Utility Reuse
- Also run Asset Dependency Closure because the module reuses `TimeManager` and
  has three consumer integration points; run Static Definitions if the final
  contract introduces shared anchor-mode/state definitions.
- Keep serialized clone fidelity, standalone portability, and live runtime
  verification as separate statuses. Use MCP only for exact unresolved
  editor/runtime blockers after repository evidence is exhausted.

### Phase 5 — Auto-pair skill generation and handoff

- Generate `GlobalTimerSync-source-to-shared` from the completed feature-surface,
  contract, and dependency evidence.
- Generate `GlobalTimerSync-shared-to-consumer` from the same collected evidence,
  without rereading the original source as a prerequisite.
- Record stage statuses, review reports, remaining consumer obligations, and
  runtime verification status.

## Approval checkpoint

No source implementation or target module code has been changed. Proceeding past
this gate requires user approval of the phase plan, or an explicit `force`
keyword.
