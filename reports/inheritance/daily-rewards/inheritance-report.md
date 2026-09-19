# Daily Rewards Inheritance Report

## 1. Module / roots

- Module: Daily Rewards core login-streak flow.
- Source: `D:\Craftland\StealAPet` (read-only).
- Target: `D:\Craftland\_Libs\SharedLibs` (read-write).
- Route: `source-to-shared-router`; intake: `reports/inheritance/daily-rewards/00-intake.md`.

## 2. Repository evidence and active implementation

Inspected source `AGENTS.md`, `Docs/CODE_CONVENTIONS.md`,
`Docs/BusinessLogic/README.md`, `Docs/BusinessLogic/41-daily-reward-mail.md`,
`ActivitiesManager.fcg`, `ActivitiesConfigs.fcg`, `TimeManager.fcg`,
`MailsManager.fcg`, `MailConfigs.fcg`, `DailyRewards.csv`, `giftcode.csv`,
`reward.csv`, and active `HudActivities.fcg` call sites. The selected active
implementation is the `ActivitiesManager` Daily Rewards section at lines
380–526, not the separately named Lucky Spin/Milestone `DailyRewardManager`.

## 3. Files and surfaces

### Created safely in SharedLibs

- `Assets/Scripts/Managers/DailyRewardsManager.fcg`
- `Assets/Scripts/Configs/DailyRewardsConfigs.fcg`
- `Assets/Scripts/Consts/DailyRewardsDefinitions.fcg`
- `Assets/Scripts/Utils/DailyRewardsTime.fcg`
- `Assets/CSV/DailyRewards.csv` and `.meta` (Studio import, source fileId preserved)
- paired module skills under `.agent/skills/daily-rewards-*`
- feature inventory and all applicable review reports.

### Modified safely in SharedLibs

- `Assets/CSV/Mails/Gifts.csv`: added the 28 gift IDs referenced by the source
  daily matrix, with source code/reuse/value/amount fidelity mapped to target
  reward fields.
- `Assets/Scripts/Configs/MailConfigs.fcg`: support open-ended `-1/-1` gift
  windows and brace-preserved composite reward values.
- Studio-managed `ProjectSettings/ResourceRegisteration.asset` and generated
  `Temp/UGCLanguage/editorGen/EditorGenLib.fcc`: DailyRewards CSV registration.

### Omitted deliberately

- Source `HudActivities` scripts/assets, prompts, reward effects, and textures:
  they are consumer UI, not core logic, and target UI assets have different
  bindings.
- Source combined daily missions/events/milestones and `DailyRewardManager`
  Lucky Spin: adjacent surfaces with separate APIs and persistence.
- Source PlayersManager/RebirthManager/FlagsManager/DebugLogManager: handled as
  integration providers or non-core dependencies, not invented in SharedLibs.

## 4. Fidelity

- Config fidelity: source 5-column schema and 35 data rows preserved exactly.
- CSV fidelity: SHA-256 source and target `DailyRewards.csv` both
  `B78AE7C79B866F79F75ED6FEFA4FC199AF705BCF454778D7500C335B5EC075CF`.
- Gift closure: every gift ID referenced by the daily matrix exists in target
  `Gifts.csv`; source reward type/value/quantity and reuse behavior were mapped.
- Persistence fidelity: login date, streak, can-claim dates, user type, default
  handling, load retry, readiness, save, clear, day refresh, and the Revival
  stale-cycle reset after a previous-login delta greater than 1209600 seconds
  are preserved.
- Action fidelity: claim remains `RequestClaimDailyReward` -> `Check...` ->
  `Process...`; Process alone mutates can-claim/claimed state and receives mail.
- Serialized bindings: CSV fileId `umxlisep0im-mpxjymwo-ge4mpccujzk` preserved;
  no UI/entity IDs were copied or remapped.

## 5. Portability changes and interfaces

- `GetDailyRewards(playerUID, rebirthLevel)` receives rebirth level explicitly;
  the source obtains it from `RebirthManager`.
- `SetUserType` and `ResetRevivalRewardCycle` expose source classification and
  revival-cycle decisions without depending on source PlayersManager.
- `SetLastLoginDeltaSeconds(playerUID, deltaSeconds)` is a transient consumer
  hook equivalent to `PlayersManager.GetPlayerDeltaLastLogTime`. It preserves
  the existing `RefreshDailyRewards`/`GetDailyRewards` APIs and is consumed once
  on the next day-change refresh.
- UI prompts/effects are omitted; consumer calls the public status-returning
  claim API and presents feedback.
- SharedLibs uses a dedicated `DailyRewards` database key (`pDailyRewards`) to
  avoid silently colliding with a consumer's combined Activities record.

## 6. Validation and MCP

- FC compiler: passed full `fccompile_external.exe -i Assets`; only existing
  deprecated `HudControls` warnings remain.
- Corrective validation rerun after the Revival branch: full compiler exit code
  `0`; Craftland Studio `game_build(release)` returned `success: true` again.
- Craftland Studio `game_build(release)`: returned success and
  `Temp/Build/FEUserLevelData.bytes`.
- EditorGen: `EResCSV.DailyRewards` is present.
- Build console has five pre-existing missing-icon errors under existing mail/
  alert UI assets; none references Daily Rewards files and they do not block the
  successful build result.
- MCP was used only for the required CSV import, CSV registration, build, and
  build-log inspection. No MCP blocker remains.

## 7. Stage summary

| Stage | Result |
| --- | --- |
| Intake/router/reference gate | Complete |
| Source feature inventory | Complete |
| Stage A faithful code/config/CSV clone | Complete with source-specific bindings isolated |
| Corrective Revival stale-cycle branch | Complete; source gate and reset ordering restored |
| Asset registration and generated symbols | Complete |
| Full FC compile | Complete |
| Studio build | Complete; unrelated pre-existing UI asset errors logged |
| Standalone portability assessment | Complete with consumer adapters documented |
| Live player claim/reconnect runtime | Pending consumer runtime session |

## 8. Remaining consumer work

Initialize target Mails DB before claim, provide user type/rebirth integration,
wire UI buttons to `RequestClaimDailyReward`, surface status strings, and decide
whether consumer persistence should merge `pDailyRewards` into a broader player
record during downstream integration.
