# Daily Missions inheritance report

## 1. Module

Daily Missions core logic, inherited from Steal A Pet into SharedLibs.

## 2–3. Source and target

- Source: `D:\Craftland\StealAPet`
- Target: `D:\Craftland\_Libs\SharedLibs`
- Source remains read-only. Target is the only write scope.

## 4. Repository evidence inspected

`AGENTS.md`, `.agent/INDEX.md`, the routed source-to-shared skill, the Craftland PUGC Steal A Pet references, source and target FC workflow rules, `Docs/CODE_CONVENTIONS.md`, `Docs/BusinessLogic/README.md`, the source `ActivitiesManager.fcg`, `ActivitiesConfigs.fcg`, `MilestoneConfig.fcg`, `DailyMissions.csv`, `milestone.csv`, relevant source call sites, and target Daily Rewards/Mails/Database/DataUtils implementations were inspected. Evidence labels are used in the companion inventory and review reports.

## 5–6. Active and deprecated implementations

The active implementation selected is `StealAPet/Assets/Scripts/Manager/ActivitiesManager.fcg` at source commit `0c1e80fb` (repository HEAD observed as `92fa2287`). The mission logic in that manager is the source of truth. No deprecated Daily Missions implementation was copied; source-only UI and reward orchestration were excluded.

## 7–8. Files cloned and omitted

Cloned/adapted:

- `Assets/Scripts/Managers/DailyMissionsManager.fcg`
- `Assets/Scripts/Configs/DailyMissionsConfigs.fcg`
- `Assets/Scripts/Configs/DailyMissionMilestonesConfigs.fcg`
- `Assets/Scripts/Consts/DailyMissionsDefinitions.fcg`
- `Assets/CSV/DailyMissions.csv` and `.meta`
- `Assets/CSV/milestone.csv` and `.meta`

Omitted by design: `HudActivities`, source Player/Pets/Wallet/Rebirth/Reward/Mails integrations, non-mission Daily Rewards/Event code, scene/UI assets, textures, and demos. This request targets the core logic only.

## 9–12. Serialized assets, fidelity, IDs, and bindings

The two readable CSVs were preserved from source; only CRLF→LF normalization differs in the working copy. Their source file IDs are preserved, and the `platform: server` metadata on `DailyMissions.csv` is preserved. The target registrations were created through Craftland Studio MCP, producing `EResCSV.DailyMissions` and `EResCSV.Milestone` in generated EditorGen output. No opaque `.eca`/scene/UI asset was copied. Existing target registrations were not replaced.

## 13–14. Dependency closure and missing dependencies

The shared implementation depends only on target-available standard FC libraries, `DatabaseController`, `DataUtils`, and `DailyRewardsTime`, plus the two registered CSV resources. Source-specific player, reward, mail, HUD, wallet, rebirth, and pet dependencies are intentionally isolated behind consumer contracts. No required compile-time dependency is missing. Actual consumer availability and reward delivery remain a runtime integration concern.

## 15–18. Config, CSV, lifecycle, and API fidelity

- Config fidelity: all source mission fields, day selection, action, target, condition, reward type/value, and priority are loaded.
- CSV fidelity: all 22 Daily Missions rows and the source milestone catalog are present; milestone config consumes source catalog ID 11 (`20;40;60;80;100` → gifts `10041;10042;10043;10044;10049`).
- Lifecycle fidelity: load/retry, ready state, save, clear, login refresh, day rollover, reset, progress, claimed mission/milestone persistence, and milestone points are implemented.
- API fidelity: mission list/progress/claim/all-claim/milestone query and Request→Check→Process methods are provided. Shared APIs return neutral reward payloads rather than delivering rewards directly.

## 19–23. Source-specific dependencies, genericization, utilities, interfaces, adapters

Source-specific providers are not imported. `SaveMoney` and `Rebirth` progress is supplied through `UpdateDailyMissionProgressValue`; normal action/condition progress uses `UpdateDailyMissionsProgress`. Mission claims accept `canDeliverRewards` as a consumer preflight and return reward payloads/milestone points. The consumer must deliver ordinary rewards and milestone gift/mail rewards. `DataUtils` and `DailyRewardsTime` are reused instead of duplicated.

## 24–25. Placement and demo artifacts

Files are organized under `Consts`, `Configs`, `Managers`, and `CSV`. No demo, HUD, or scene artifact was added.

## 26–30. Clone, runtime, MCP, and Studio status

- Serialized clone: complete for readable CSV assets and metadata.
- FC compile: passed with the installed target compiler using its supported `-i Assets -e Temp/UGCLanguage/editorGen` form; this installed compiler rejected the newer `-agent`/`-session` flags before compilation, so the supported equivalent was used. Only pre-existing deprecation warnings in `HudControls.fcg` were emitted.
- Studio build: `game-build(release)` returned `success: true` and produced `Temp/Build/FEUserLevelData.bytes`.
- Studio logs: existing unrelated missing sprite errors remain for `AlertIconNotice`, `AlertIconSystem`, `MailDetails`, `AlertMenuIcon`, and `AlertMailIcon`; they do not reference the Daily Missions files.
- Gameplay/runtime verification: not performed; consumer reward delivery and live player persistence need a Studio playtest.
- MCP: used for CSV registration and release build after reading the required Craftland instructions. No MCP blocker remains for the shared core.

## 31. Stage completion summary

Stage A (faithful mission core and data) is complete. Stage B (provider isolation and shared-layer organization) is complete. Consumer integration and gameplay verification remain intentionally outside this source-to-shared change.

## 32–33. Safe files created and modified

Safe files created are listed in sections 7 and the companion inventory. The only tracked project setting changed is the Studio-managed CSV registration in `ProjectSettings/ResourceRegisteration.asset`. Generated EditorGen output was refreshed by Studio and not hand-edited. No existing business-logic file was modified.

## 34–37. Faithful clone, fidelity, portability, and runtime evidence

- Faithful clone: `Pass with explicit adapter boundary`; mission state, rotation, progress, reset, persistence, and claim state are preserved.
- Clone fidelity: `Pass` for source-readable CSV/config semantics and compile-time symbols; reward delivery side effects are deliberately moved to the consumer.
- Standalone portability: `Pass for compile-time portability`; the module has no source-project imports. Runtime portability depends on the target consumer implementing the documented contract.
- Runtime verification: `Studio build passed`; actual claim/load/save gameplay remains pending.

## 38–41. Utility, texture, enum, and component analysis

- Utility dependency: reused target `DataUtils` and `DailyRewardsTime`.
- Texture dependency: none; no UI/HUD assets were included.
- Custom enum: source action/reward enums were discovered in generated source symbols. Shared code preserves actions as strings and reward kinds as CSV integer values; milestone point `8` is named in definitions.
- Custom component: none discovered or required.

## 42–45. Definitions and value handling

Definitions found: `DailyMissionsDefinitions`, `DailyMissionsConfigs`, and `DailyMissionMilestonesConfigs`. CSV column positions, actions, mission IDs, targets, conditions, reward values, priorities, milestone thresholds, gift IDs, persistence field intent, and source resource file IDs are preserved. Values remapped only where needed for shared naming (`Activity_*` → `DailyMission_*`, `pActivities` → `pDailyMissions`); source reward integers remain unchanged. No unknown value was discarded.

## 46–48. Blockers and remaining work

Exact blockers: none for Stage A/B or FC/build validation. Remaining Studio work is a consumer-backed playtest covering database load/save, day rollover, action progress, ordinary reward delivery, milestone mail delivery, disconnect/failed-delivery behavior, and UI integration.

## 49. Consumer adaptation requirements

Consumers must register/use the `DailyMissions` database lifecycle, forward source-equivalent action events, call `UpdateDailyMissionProgressValue` for provider-backed `SaveMoney`/`Rebirth` progress, localize `Description`, and implement reward delivery around `RequestClaimDailyMission`, `RequestClaimAllCompletedDailyMissions`, and `RequestClaimDailyMilestone`. They should persist/retry through the shared database lifecycle and surface returned status codes to UI.
