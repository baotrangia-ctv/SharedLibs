---
name: shared-to-consumer-router
description: Route SharedLibs to consumer integration through preserve-first repository inspection, definition search, complete safe stages, consumer portability assessment, and exact MCP-last blockers.
---

# Purpose

Route every completed shared module to one consumer workflow without requiring access
to the original source project.

# Required Inputs

- user request and module name
- `.codex/project-paths.json`
- module portability manifest and consumer package when available

# Path Validation

Before SharedLibs inspection or consumer modification:

1. Resolve and normalize configured SharedLibs and consumer paths.
2. Verify both roots and repository markers.
3. Verify the roots differ.
4. Treat SharedLibs as read-only for this workflow and verify the consumer is
   read-write. Do not require the configured SharedLibs permission to be read-only.
5. Stop before modification when validation fails.

# Workflow

```text
Validate configured SharedLibs and consumer paths
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

- `.codex/references/inheritance/repository-first.md`
- `.codex/references/inheritance/serialized-assets.md` when serialized assets exist
- `.codex/references/inheritance/dependency-closure.md` when references exist
- `.codex/references/inheritance/mcp-last.md`
- `.codex/references/inheritance/runtime-verification.md`
- `.codex/references/inheritance/preserve-first-bindings.md`
- `.codex/references/inheritance/repository-definition-search.md`
- `.codex/references/inheritance/stage-based-completion.md`
- `.codex/references/inheritance/standalone-portability.md`
- `.codex/references/inheritance/explicit-mcp-blockers.md`

# Review Routing

- Use `review-serialized-asset-fidelity` for serialized assets.
- Use `review-asset-dependency-closure` for referenced files or assets.
- Use `review-standalone-portability` to report remaining shared or consumer
  dependencies separately from transfer fidelity.
- Use `review-folder-architecture` when files are created, copied, moved, or adapted.
- Use `review-utility-reuse` for structured-data adaptation.
- Use `review-static-definitions` for cross-boundary definitions.
- Use `review-request-check-process` for public actions.
- Use `review-data-lifecycle` for persistence or runtime state.
- Use `review-production-readiness` for real or release-facing integrations.

# Required Evidence

Record validated roots and modes, selected module skill and reviews, SharedLibs
artifacts and active APIs, serialized identity and binding handling, dependency
closure, repository definitions, preserve/remap decisions, copied/adapted/omitted
files, stage statuses, consumer portability, utility and texture handling, exact MCP
blockers, runtime status, and rollback.

# Allowed Scope

Inspect SharedLibs and the validated consumer. Modify only the validated consumer
target after path validation.

# Stop Conditions

Stop for invalid paths, a non-writable consumer, same source and target, or a missing
module workflow. A read-write SharedLibs configuration is allowed but this workflow
must not modify it. Missing portability artifacts or consumer integration points
block only their affected stage unless all full-task blocker conditions apply.

Block the whole integration because MCP is unavailable only when all six conditions
in `.codex/references/inheritance/explicit-mcp-blockers.md` are true. Otherwise block
only the affected stage and continue safe filesystem integration.

# Reports

Write results under `reports/consumer-integrations/[consumer-project]/[module]/` and
use `references/consumer-integration-report-template.md`.
