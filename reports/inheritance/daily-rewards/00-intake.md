# Daily Rewards — Source-to-Shared Intake

1. **Module covered:** Daily Rewards core logic.

2. **Confirmed route:** `source-to-shared-router` (Steal A Pet source project -> SharedLibs).

3. **Validated source root and access mode:** `D:\Craftland\StealAPet`; configured access mode `read-only`. The root exists, is a directory, and contains a `.git` repository marker. No source files will be modified.

4. **Validated SharedLibs root and access mode:** `D:\Craftland\_Libs\SharedLibs`; configured access mode `read-write`. The root exists, is a directory, and contains both `.git` and `.agent` repository markers.

5. **Selected module skill:** `.agent/skills/daily-rewards-source-to-shared/SKILL.md` and the paired `.agent/skills/daily-rewards-shared-to-consumer/SKILL.md` were created from the router templates after discovery, with the required Daily Rewards-specific scope and portability boundary.

6. **Required Common References actually opened:**
   - `.agent/references/inheritance/repository-first.md`
   - `.agent/references/inheritance/clone-first-workflow.md`
   - `.agent/references/inheritance/mcp-last.md`
   - `.agent/references/inheritance/runtime-verification.md`
   - `.agent/references/inheritance/preserve-first-bindings.md`
   - `.agent/references/inheritance/repository-definition-search.md`
   - `.agent/references/inheritance/faithful-clone-mode.md`
   - `.agent/references/inheritance/stage-based-completion.md`
   - `.agent/references/inheritance/standalone-portability.md`
   - `.agent/references/inheritance/explicit-mcp-blockers.md`

7. **User-specified exclusions:** none. The request covers the core logic of Daily Rewards without naming a sub-feature to exclude. Repository evidence later identified `DailyRewardManager` as the source's separately named Lucky Spin/Milestone flow; it is recorded as an adjacent scope boundary, not a user-specified exclusion.

8. **Dependency-closure check for exclusions:** not applicable because no exclusion was specified. During discovery, any source-only or non-core Daily Rewards feature found outside the requested scope will be checked for shared Manager, config, utility, and serialized-asset touch points before isolation.

9. **Stop conditions:** the router-mentioned template path `.agent/references/inheritance/intake-record-template.md` is absent. The same required template is available at `.agent/skills/source-to-shared-router/references/intake-record-template.md` and was used. This is recorded as a resolved repository-layout discrepancy; no path-validation stop condition remains.

10. **Evidence collected before implementation:** source `ActivitiesManager.fcg` lines 115, 289, 326, 380–526; `ActivitiesConfigs.fcg` lines 65–226; `DailyRewards.csv` (35 data rows); `HudActivities.fcg` lines 417–552; target mail/config/database utilities; and target generated `EResCSV.DailyRewards` registration.

11. **Implementation boundary:** Manager/config/definitions/time utility/persistence/mail config and CSV are in scope. Source HUD widgets, prompts, reward presentation, source PlayersManager/RebirthManager classification, unrelated missions/events, and Lucky Spin/Milestone code remain consumer integration or adjacent scope.

12. **Corrective request:** restore the source Revival stale-cycle reset in `RefreshDailyRewards` without importing `PlayersManager`; preserve existing APIs through a consumer-supplied transient last-login-delta hook. This turn re-runs the source-to-shared router and `review-inherited-module` Clone Fidelity + Feature Completeness sections.

13. **User-specified exclusions for this corrective task:** do not modify config lookup, GMT day-index, mail claim flow, `Gifts.csv`, or `MailConfigs.fcg`. Dependency-closure check: the fix is confined to `DailyRewardsManager.fcg` and its existing `DailyRewardsDefinitions.REVIVAL_REWARD_RESET_SECONDS`; no excluded config/time/mail artifact needs to change.

14. **Corrective evidence opened:** source `ActivitiesManager.fcg:289-305`; target `DailyRewardsManager.fcg:238-253`; target `DailyRewardsDefinitions.fcg:13`; existing inheritance/clone-fidelity/feature-completeness reports; router, module skill, review skill, and inheritance references including `clone-fidelity.md`.
