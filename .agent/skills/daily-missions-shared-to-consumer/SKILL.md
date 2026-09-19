---
name: daily-missions-shared-to-consumer
description: Integrate the SharedLibs Daily Missions core into a consumer project while preserving its persistence and claim contract.
---

# Purpose

Integrate `DailyMissionsManager` and its CSV/config surface into a consumer
without changing the inherited mission rules. The consumer supplies reward
delivery, player/pet/wallet/rebirth providers, UI, prompts/effects, and any
optional progress event routing.

# Consumer contract

- Register and wait for the `DailyMissions` database before querying or claiming.
- Call `UpdateDailyMissionsProgress(playerUID, action, conditions)` for count-
  based events and `SetDailyMissionProgress` for provider-owned absolute values
  such as money rank or rebirth level.
- Use `GetDailyMissions`, `GetDailyMissionIds`, `CanClaimDailyMissionReward`,
  and `GetMilestonePoints` for presentation.
- Call `RequestClaimDailyMission` or `RequestClaimDailyMilestone`; consume the
  returned reward bundle/reward id only after `NoError`, and surface the
  returned status through consumer UI.
- Provide idempotent reward dispatch and capacity validation before marking a
  consumer-side delivery complete. The shared manager owns claimed-state
  mutation and persistence; consumers own actual reward application.

# Required workflow and reviews

Read `.agent/references/inheritance/standalone-portability.md`,
`runtime-verification.md`, `preserve-first-bindings.md`, and
`repository-definition-search.md` before adapting. Validate database lifecycle,
reconnect/save behavior, action idempotency, CSV registration, reward contract,
and UI/event call sites. Report consumer work under the consumer integration
report location and do not edit inherited shared implementation during a
consumer-only review.

# Known integration points

The core does not depend on SAP `ActivitiesManager`, `ActivitiesConfigs`,
`PlayersManager`, `RebirthManager`, `PetsManager`, `WalletManager`,
`RewardManager`, `MailsManager`, or `HudActivities`. Adapters are justified only
when they translate those provider contracts or attach UI/effects; pass-through
wrappers should not be introduced.
