---
name: daily-rewards-source-to-shared
description: Inherit the source Daily Rewards login-streak flow into SharedLibs while preserving configuration, persistence, Request-Check-Process claims, mail delivery, and lifecycle behavior.
---

# Purpose

This module skill routes the source `ActivitiesManager` Daily Rewards surface,
not the separately named `DailyRewardManager` Lucky Spin/Milestone surface.

# Required workflow

1. Read the source `ActivitiesManager` Daily Rewards section, its daily config
   and CSV, mail/config contracts, persistence fields, and active call sites.
2. Inventory source-specific dependencies and classify each as cloned, adapted,
   consumer integration, or out of scope.
3. Preserve the source seven-day streak, day-index refresh, user-type/rebirth
   reward lookup, mail-backed claim, and load/save lifecycle in Stage A.
4. Keep `Request -> Check -> Process` explicit. Checks must remain read-only;
   claim state changes belong to Process.
5. Use the target MailsManager contract and target folder conventions. Reuse
   target `DataUtils` and `DatabaseController` instead of creating duplicates.
6. Import/register readable CSV assets through Craftland Studio MCP and never edit
   generated EditorGen files.
7. Compile the full target `Assets` tree after FC edits, then run the editor build
   and inspect console logs when runtime/build verification is available.
8. Write inheritance and review reports under the Daily Rewards report folders.

# Required evidence

- Source and target roots, route/intake record, active call sites, exact CSV
  schema/rows, public APIs, persistence keys, dependency classifications,
  preserve/remap decisions, stage statuses, portability and runtime status.
- Apply Clone Fidelity, Standalone Portability, Feature Completeness, Folder
  Architecture, Serialized Asset Fidelity, Asset Dependency Closure, Utility
  Reuse, Static Definitions, Request-Check-Process, and Data Lifecycle reviews.

# Portability boundary

The source derives user type and rebirth level from game-specific Managers and
drives HUD effects/prompts from `HudActivities`. SharedLibs exposes explicit
setters/parameters for those values and leaves UI feedback to the consumer.
This keeps the core logic usable without inventing source-only managers.

