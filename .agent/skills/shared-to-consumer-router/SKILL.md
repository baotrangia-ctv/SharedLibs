---
name: shared-to-consumer-router
description: Route SharedLibs to consumer integration with preserve-first inspection, consumer portability assessment, exact MCP-last blockers, and a mandatory Complexity Gate + Phase Plan unless explicitly forced.
---

# Purpose

Route every completed shared module to one consumer workflow without requiring access
to the original source project.

# Required Inputs

- user request and module name
- `.agent/project-paths.json`
- module portability manifest and consumer package when available

# Path Validation

Before SharedLibs inspection or consumer modification:

1. Resolve and normalize configured SharedLibs and consumer paths.
2. Verify both roots and repository markers.
3. Verify the roots differ.
4. Treat SharedLibs as read-only for this workflow and verify the consumer is
   read-write. Do not require the configured SharedLibs permission to be read-only.
5. Stop before modification when validation fails.

# Intake Gate (Mandatory First Action)

Before inspecting SharedLibs implementation files or writing any file outside
`reports/`, create
`reports/consumer-integrations/[consumer-project]/[module]/00-intake.md` using
`references/intake-record-template.md`. It must record:

- The validated SharedLibs and consumer roots and access modes from Path
  Validation.
- Confirmation this request routes through `shared-to-consumer-router`, not
  `source-to-shared-router`.
- The selected `[module]-shared-to-consumer` skill, or a note that it is
  missing and blocks routing.
- Every file actually opened from `# Required Common References` below,
  listed by path.
- The Complexity Gate result computed in the next section.

Do not modify any consumer file, and do not print a Phase Plan, until
`00-intake.md` exists and lists every required reference actually loaded. A
missing or incomplete intake record is a Stop Condition, identical to an
invalid path. Complete the Complexity Gate assessment as part of building this
same intake record, before proposing a Phase Plan or starting Stage A.

# Complexity Gate and Phase Plan

Apply this gate before changing code for every SharedLibs-to-consumer request
unless the user explicitly uses a force keyword. The gate still runs and its
result must be recorded when force is used.

## Complexity assessment

Mark the module **complex — mandatory phase plan** when either condition is true:

- **A — component count:** the module has at least four component types from
  {Manager, HUD/UI script, Config/CSV, Persistence, Event, Public API/contract,
  independent serialized asset}.
- **B — sensitive state:** the module uses persistence, reconnect, runtime cache,
  or network/server synchronization, regardless of file count.

If neither condition is true, mark the module **simple**. Before implementing a
simple module, list the short sequence of work; a formal phase plan is not
required.

## Required plan for complex modules

Before any file change, print:

```md
## Đề xuất Phase Plan — Inherit [module] vào [consumer_project]

Lý do chia phase: [điều kiện A/B + bằng chứng cụ thể]

- **Phase 1 — [tên]:** [thành phần/tính năng cụ thể]
- **Phase 2 — [tên]:** [thành phần/tính năng cụ thể]
- **Phase 3 — [tên]:** [thành phần/tính năng cụ thể]

Mỗi phase sẽ dừng lại để bạn review trước khi sang phase tiếp theo.
Gõ "force" hoặc "làm luôn" nếu muốn bỏ qua plan và chạy thẳng toàn bộ.
```

Adapt the phase sequence to the actual module. Use these layers when applicable:

1. Core data/model and config, without UI or persistence.
2. Manager/logic and public contract, including Request-Check-Process when
   applicable.
3. HUD/UI, navigation, and loading/empty/error state.
4. Persistence/reconnect/lifecycle when condition B is true.
5. Production readiness and polish only when release work is in scope.

After printing the plan, stop and wait for explicit user approval before any
file change. In Claude Code this maps to `ExitPlanMode`; in Codex, stop after
the plan and require explicit go-ahead.

## Force keywords

Treat `force`, `làm luôn`, `không cần plan`, `just do it`, and `skip plan` as
explicit force keywords. With force, skip the approval stop and run the full
workflow (Stage A → Stage B → applicable reviews → report), but still record
the Complexity Gate result for audit.

## Between approved phases

After each phase, report the work completed, the applicable
`review-inherited-module` sections run, stage statuses, and remaining work. Stop
and wait for user approval before continuing to the next phase. Do not chain
phases automatically unless the user explicitly approved all remaining phases.

# Workflow

```text
Validate configured SharedLibs and consumer paths
    ->
Write the mandatory 00-intake.md intake record and Complexity Gate result
    ->
Select [module]-shared-to-consumer
    ->
Inspect SharedLibs repository evidence
    ->
Select latest active public contract
    ->
Inventory serialized assets and references
    ->
Build the smallest complete dependency closure
    ->
Search SharedLibs and consumer definitions
    ->
Preserve compatible values and copy required dependencies
    ->
Adapt only proven incompatibilities
    ->
Isolate unresolved consumer-specific behavior
    ->
Complete every safe independent stage
    ->
Assess consumer portability separately from fidelity
    ->
Run focused reviews with Adapter-Last and Demo-Last
    ->
Use MCP only for exact unresolved blockers
    ->
Generate stage-based integration and rollback reports
```

Do not read the original source project. Stop routing if the module workflow is
missing. If portability artifacts are missing, inspect available shared contracts,
complete safe analysis stages, and block only the stage that cannot proceed safely.

# Required Common References

Load:

- `.agent/references/inheritance/repository-first.md`
- `.agent/references/inheritance/serialized-assets.md` when serialized assets exist
- `.agent/references/inheritance/dependency-closure.md` when references exist
- `.agent/references/inheritance/mcp-last.md`
- `.agent/references/inheritance/runtime-verification.md`
- `.agent/references/inheritance/preserve-first-bindings.md`
- `.agent/references/inheritance/repository-definition-search.md`
- `.agent/references/inheritance/stage-based-completion.md`
- `.agent/references/inheritance/standalone-portability.md`
- `.agent/references/inheritance/explicit-mcp-blockers.md`

# Review Routing

- Use `review-inherited-module` — Serialized Asset Fidelity — for serialized assets.
- Use `review-inherited-module` — Asset Dependency Closure — for referenced files or assets.
- Use `review-inherited-module` — Standalone Portability — to report remaining
  shared or consumer dependencies separately from transfer fidelity.
- Use `review-inherited-module` — Folder Architecture — when files are created,
  copied, moved, or adapted.
- Use `review-inherited-module` — Utility Reuse — for structured-data adaptation.
- Use `review-inherited-module` — Static Definitions — for cross-boundary definitions.
- Use `review-inherited-module` — Request-Check-Process — for public actions.
- Use `review-inherited-module` — Data Lifecycle — for persistence or runtime state.
- Use `review-inherited-module` — Production Readiness — for real or release-facing integrations.

# Required Evidence

Record the `00-intake.md` path and completeness, validated roots and modes, selected module skill and reviews, SharedLibs
artifacts and active APIs, serialized identity and binding handling, dependency
closure, repository definitions, preserve/remap decisions, copied/adapted/omitted
files, stage statuses, consumer portability, utility and texture handling, exact MCP
blockers, runtime status, and rollback.

# Allowed Scope

Inspect SharedLibs and the validated consumer. Modify only the validated consumer
target after path validation.

# Stop Conditions

Stop for invalid paths, a non-writable consumer, same source and target, a missing or
incomplete `00-intake.md` record, or a missing module workflow. A read-write SharedLibs configuration is allowed but this workflow
must not modify it. Missing portability artifacts or consumer integration points
block only their affected stage unless all full-task blocker conditions apply.

Block the whole integration because MCP is unavailable only when all six conditions
in `.agent/references/inheritance/explicit-mcp-blockers.md` are true. Otherwise block
only the affected stage and continue safe filesystem integration.

# Reports

Write results under `reports/consumer-integrations/[consumer-project]/[module]/` and
use `references/consumer-integration-report-template.md`.
