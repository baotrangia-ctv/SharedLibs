---
name: GlobalTimerSync-shared-to-consumer
description: Integrate SharedLibs GlobalTimerSync into a consumer project using its single wave-state contract and the correct region-adjusted or fixed-epoch anchor.
---

# Purpose

Use this skill when transferring `GlobalTimerSync` from SharedLibs into a
validated consumer project. Treat SharedLibs as read-only for the consumer
workflow and do not reread `StealAPet` as a prerequisite.

## Required policy references

Use `shared-to-consumer-router` with repository-first, preserve-first, dependency
closure, stage completion, standalone portability, runtime-verification, and
MCP-last references. Apply Adapter-Last and Demo-Last. Use the applicable
`review-inherited-module` sections, at minimum Clone Fidelity, Standalone
Portability, Feature Completeness, Folder Architecture, and Utility Reuse; add
Asset Dependency Closure and Static Definitions when the consumer binds scripts
or shared mode/epoch definitions.

## Shared contract

Import the shared utility and call the single API:

```text
GetGlobalWaveState(anchorMode, waveDurations, epochOffset?, out waveIndex, out durationLeftMs)
```

The FC-compatible `epochOffset?` parameter is nullable `object`. Durations and
`durationLeftMs` are milliseconds. Anchor/phase offsets are seconds.

Use the shared definitions rather than duplicating numeric modes or the epoch:

- Weather: `ANCHOR_MODE_REGION_ADJUSTED`, a full weather duration list, `nil`
  phase unless the consumer has a proven phase requirement.
- Global Spawn Pet Mythic/Apex: `ANCHOR_MODE_REGION_ADJUSTED`, a one-element
  interval list, and the existing rarity-specific `START_SECOND` phase.
- Rotation Shop: `ANCHOR_MODE_FIXED_EPOCH`, the full rotation duration list,
  and `GlobalTimerSyncDefinitions.DEFAULT_FIXED_EPOCH_OFFSET` or an explicit
  consumer override.

Do not create separate DailySync, MilestoneSync, WeatherSync, or RotationSync
core functions. Keep consumer-specific Manager state, config readers, events,
UI, persistence, and side effects at the consumer boundary.

## Integration and validation

1. Validate SharedLibs and consumer roots before changing the consumer.
2. Inspect the SharedLibs public contract and dependency closure; preserve
   compatible target utilities and folder conventions.
3. Build duration lists in milliseconds from consumer config getters.
4. Wire the API at the existing countdown entry points only; preserve consumer
   lifecycle and event behavior.
5. Search for duplicate wave arithmetic or hardcoded `1776880800` and replace
   only when repository evidence proves the shared call is equivalent.
6. Run full FC compilation after FC edits; keep runtime Studio verification
   separate and explicit.

Report unresolved clock/region/runtime bindings and consumer obligations under
`reports/consumer-integrations/[consumer-project]/GlobalTimerSync/`. Do not claim
runtime synchronization without live verification.
