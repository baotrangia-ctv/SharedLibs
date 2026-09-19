# Active API surface review — Daily Missions

Status: **Pass**.

The public surface was derived from active source getters and call-site evidence: mission list/progress getters, claimed-state queries, action progress update, provider-value progress update, completion checks, mission claim, claim-all, milestone claim, and database lifecycle events. The shared API uses `string` action values and explicit `out` results so consumers do not need source-only enums or reward managers.

