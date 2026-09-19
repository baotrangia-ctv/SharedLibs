---
name: daily-missions-source-to-shared
description: Inherit the Steal A Pet Daily Missions core into SharedLibs while preserving mission rotation, progress, milestone state, persistence, config rows, and Request-Check-Process claim semantics.
---

# Purpose

Route the active Steal A Pet Daily Missions implementation from
`ActivitiesManager.fcg` and `ActivitiesConfigs.fcg` into SharedLibs. The module
includes daily mission selection, progress tracking, daily reset, milestone
points/claims, persistence, CSV-driven definitions, and the public claim
contract. Daily Rewards, Daily Event, Lucky Spin, HUD/UI, source prompts, and
source-specific reward/player managers are adjacent or consumer-owned surfaces.

# Scope and workflow

1. Validate `D:\Craftland\StealAPet` as read-only and
   `D:\Craftland\_Libs\SharedLibs` as read-write through
   `.agent/project-paths.json`.
2. Read the shared inheritance references required by
   `source-to-shared-router` and the source `AGENTS.md`, code conventions,
   BusinessLogic catalog, and active mission call sites.
3. Use the active `ActivitiesManager` Daily Missions section, not the old
   `DailyRewardManager` or source HUD implementation, as the behavior baseline.
4. Stage A preserves CSV schema/rows, weekly day selection, progress
   clamping, daily reset, mission/milestone cache state, persistence lifecycle,
   and Request -> Check -> Process semantics.
5. Stage B uses SharedLibs folder conventions and isolates source-only reward
   dispatch, player/rebirth/wallet/pet checks, HUD updates, prompts, and
   effects behind explicit consumer-facing return values and setters.
6. Register readable CSV assets through Craftland Studio MCP after copying them;
   never edit generated EditorGen files. Run full FC compilation and Studio
   build/log validation after FC edits and registration.

# Target surface

- `Assets/Scripts/Managers/DailyMissionsManager.fcg`: authoritative player
  state, load/save, reset, progress, milestone state, query APIs, and claims.
- `Assets/Scripts/Configs/DailyMissionsConfigs.fcg`: DailyMissions CSV reader
  and lookup APIs.
- `Assets/Scripts/Configs/DailyMissionMilestonesConfigs.fcg`: feature-local
  milestone CSV reader and threshold -> reward-id lookup.
- `Assets/Scripts/Consts/DailyMissionsDefinitions.fcg`: database keys,
  persistence field keys, CSV columns, action/status/contract literals.
- `Assets/CSV/DailyMissions.csv`: source mission schema and rows preserved.
- `Assets/CSV/DailyMissionMilestones.csv`: source milestone catalog rows for
  milestone ID 11 extracted into a feature-local schema.

# Required reviews

Always run Clone Fidelity, Standalone Portability, Feature Completeness, and
Folder Architecture. Also run Serialized Asset Fidelity for CSV/meta files,
Asset Dependency Closure, Active API Surface, Utility Reuse, Static Definitions,
Request-Check-Process, and Data Lifecycle. Reports belong under
`reports/inheritance/daily-missions/` and `reports/reviews/daily-missions/`.

# Portability boundary

The source imports `PlayersManager`, `RebirthManager`, `PetsManager`,
`WalletManager`, `RewardManager`, `MailsManager`, and `HudActivities`. SharedLibs
must not invent these source APIs. Shared code returns normalized reward bundles
and milestone reward IDs from claims; consumers own reward delivery, capacity
checks, UI prompts/effects, and provider-driven absolute progress updates.

# Evidence and stop rules

Record repository-relative paths, symbols, persistence keys, CSV hashes/rows,
call sites, preserved/remapped values, and each source-specific dependency.
Unknown but structurally safe IDs/values are preserved and reported. MCP may
block only an exact mandatory dependency satisfying all six conditions in
`explicit-mcp-blockers.md`; missing runtime/UI verification does not block
serialized code/config inheritance.
