---
name: source-to-shared-router
description: Route source-project to SharedLibs inheritance through repository definition search, preserve-first faithful cloning, safe stage completion, clone and portability reviews, and exact MCP-last blockers.
---

# Purpose

Route every source-to-shared inheritance to one module workflow and the smallest
sufficient common review set. Keep module behavior out of the router.

# Required Inputs

- user request and module name
- `.codex/project-paths.json`

# Path Validation

Before source inspection or target modification:

1. Resolve and normalize configured source and SharedLibs paths.
2. Verify both roots and repository markers.
3. Verify the roots differ.
4. Verify the source is read-only and SharedLibs is read-write.
5. Stop before modification when validation fails.

# Workflow

```text
Validate configured source and target paths
    ->
Select [module]-source-to-shared
    ->
Apply repository-first discovery
    ->
Identify the latest active implementation
    ->
Build the complete dependency closure
    ->
Search repository definitions
    ->
Choose preserve, copy, adapt, or isolate handling
    ->
Complete every safe independent stage
    ->
Create a Faithful Clone Mode result
    ->
Run serialized, dependency, and clone-fidelity reviews
    ->
Assess standalone portability
    ->
Apply module-specific, architecture, and quality reviews
    ->
Use MCP only for exact unresolved blockers
    ->
Generate stage-based reports
```

If the module skill is absent and skill creation is in scope, create both module
workflow skills from the common templates. Otherwise stop and identify the missing
workflow.

# Required Common References

Load these before routing implementation work:

- `.codex/references/inheritance/repository-first.md`
- `.codex/references/inheritance/clone-first-workflow.md`
- `.codex/references/inheritance/mcp-last.md`
- `.codex/references/inheritance/runtime-verification.md`
- `.codex/references/inheritance/preserve-first-bindings.md`
- `.codex/references/inheritance/repository-definition-search.md`
- `.codex/references/inheritance/faithful-clone-mode.md`
- `.codex/references/inheritance/stage-based-completion.md`
- `.codex/references/inheritance/standalone-portability.md`
- `.codex/references/inheritance/explicit-mcp-blockers.md`

Load `serialized-assets.md`, `dependency-closure.md`, and `clone-fidelity.md` when
their corresponding stage or review begins. Module skills load only their own
feature-specific references.

# Review Routing

- Always use `review-clone-fidelity`.
- Always use `review-standalone-portability`.
- Always use `review-feature-completeness`.
- Always use `review-folder-architecture`.
- Use `review-serialized-asset-fidelity` for readable serialized assets.
- Use `review-asset-dependency-closure` for referenced files or assets.
- Use `review-active-api-surface` for duplicate, versioned, legacy, deprecated, or
  compatibility APIs.
- Use `review-utility-reuse` for structured-data processing.
- Use `review-static-definitions` for repeated or cross-layer definitions.
- Use `review-request-check-process` for public Manager actions.
- Use `review-data-lifecycle` for persistence, cache, readiness, reconnect, quit,
  shutdown, or persistent rewards.
- Use `review-production-readiness` only for release-facing work.
- Select no demo skill by default.

# Required Evidence

Record validated roots and modes, repository markers, selected module skill and
reviews, repository paths inspected, active implementation evidence, artifact
classifications, definition searches, dependency closure, preserve/remap decisions,
stage statuses, faithful clone status, clone fidelity, standalone portability, Stage
B changes, safe files, utility and texture analysis, exact MCP blockers, runtime
status, and Studio-only gaps.

# Allowed Scope

Inspect validated source evidence, SharedLibs files, rules, skills, references, and
reports. Modify only the validated SharedLibs target after path validation.

# Stop Conditions

Stop routing for invalid paths, same source and target, incorrect access modes, or a
missing module workflow outside creation scope.

A missing root, authoritative artifact, or transitive dependency blocks only its
affected stage by default. Search validated roots, preserve or isolate when safe,
report it, and continue independent stages.

Block the whole inheritance because MCP is unavailable only when all six conditions
in `.codex/references/inheritance/explicit-mcp-blockers.md` are true. Otherwise block
only the affected stage. Unknown custom values, partial standalone portability,
local files, complex dependencies, closed Studio, and pending runtime verification
are not full-task blockers.

# Reports

Write inheritance evidence under `reports/inheritance/[module]/` and reviews under
`reports/reviews/[module]/`, including:

- `serialized-asset-fidelity-review.md` when applicable
- `asset-dependency-closure-review.md` when applicable
- `clone-fidelity-review.md`
- `standalone-portability-review.md`
- `feature-completeness-review.md`
- architecture and selected quality reviews

Use `references/inheritance-report-template.md`.
