---
name: mails-source-to-shared
description: Inherit the active source Mails feature through preserve-first repository discovery, Faithful Clone Mode, safe stage completion, separate standalone-portability assessment, and exact MCP-last blockers.
---

# Purpose

Apply the common source-to-shared framework while tracing the feature-specific
Manager, HUD, config, CSV, persistence, event, and action flows.

# Required Inputs

- router-validated source read-only and SharedLibs read-write roots
- `.codex/project-paths.json`
- existing target outputs and reports, if present

# Workflow

```text
Discover complete feature surface and latest active implementation
    ->
Inventory Manager, HUD scripts, serialized UI/assets, Config, CSV, persistence,
events, Utils, localization, public APIs, reports, and dependencies
    ->
Trace initialization, list/detail queries, claim actions, state refresh, load, save,
and callbacks
    ->
Build the complete dependency closure
    ->
Search source and shared repository definitions
    ->
Preserve, copy, adapt, or isolate every custom binding and dependency
    ->
Complete every safe independent stage
    ->
Create a faithful source-compatible clone
    ->
Run serialized, dependency, and clone-fidelity reviews
    ->
Assess standalone portability and consumer adaptation
    ->
Refactor safe Stage B work with utility reuse, Adapter-Last, Demo-Last, and layers
    ->
Use MCP only for enumerated structurally invalid blockers
    ->
Generate stage-based reports and optionally verify runtime
```

Stage A must preserve the active open, list, select, claim, refresh, feedback, config,
CSV, persistence, and event flows before Stage B changes their dependencies.

# Common References

Read from `.codex/references/inheritance/`:

- `repository-first.md`, `clone-first-workflow.md`, and `clone-fidelity.md` always
- `serialized-assets.md` when readable serialized assets exist
- `dependency-closure.md` when references exist
- `mcp-last.md` before an MCP request or MCP-related stop
- `runtime-verification.md` when reporting completion
- `preserve-first-bindings.md`, `faithful-clone-mode.md`,
  `stage-based-completion.md`, and `standalone-portability.md` always
- `repository-definition-search.md` for custom or unresolved definitions
- `explicit-mcp-blockers.md` before an MCP-related stage block

Read module references progressively:

- `references/feature-surface-template.md` for discovery
- `references/dependency-analysis.md` for feature-specific integrations
- `references/business-abstraction.md` during Stage B
- `references/primary-flow-validation.md` for executable behavior
- `references/module-contract-template.md` for public contracts
- `references/consumer-kit-template.md` after clone fidelity and Stage B validation

# Reviews

- Always use `review-clone-fidelity`, `review-standalone-portability`,
  `review-feature-completeness`, and `review-folder-architecture`.
- Use `review-serialized-asset-fidelity` for readable serialized assets.
- Use `review-asset-dependency-closure` for referenced files or assets.
- Use `review-active-api-surface` when duplicate or versioned APIs exist.
- Use `review-utility-reuse` for structured data.
- Use `review-static-definitions` for reused fields, statuses, actions, or results.
- Use `review-request-check-process` for claim and other public actions.
- Use `review-data-lifecycle` for persisted state, cache, readiness, reconnect, quit,
  shutdown, or rewards.

# Architecture and Behavior Constraints

- Place Manager, HUD script, config/definitions, UI assets, and generic utilities in
  their established architectural layers.
- Inspect `DataUtils` and existing Utils before adding data helpers.
- Preserve Request -> Check -> Process, with Check read-only and Process
  Manager-owned.
- Preserve available readable UI assets; do not replace them with a simplified HUD.
- Preserve unknown custom enums, components, IDs, and bindings when structurally
  safe; do not remap merely because their display meaning is unknown.
- Resolve repository utilities and local textures through dependency closure before
  considering MCP.
- If no serialized UI asset exists, a minimal fallback is allowed only after
  repository evidence is exhausted and exact parity is reported unavailable.
- Preserve source-specific behavior during Stage A. During Stage B, isolate it behind
  the smallest necessary interface or justified adapter without deleting behavior
  before a replacement path exists.
- Do not generate demo providers, fake persistence, or placeholder rewards by
  default.

# Allowed Scope

Inspect only validated source evidence and SharedLibs. Modify only SharedLibs target
files when implementation is requested.

# Required Evidence

Record repository-relative paths, active-version call sites, artifact and dependency
classifications, definition searches, preserve/remap decisions, stage statuses,
config and CSV schemas, lifecycle and action flow, faithful clone status, standalone
portability, utility and texture analysis, exact MCP blockers, runtime status, and
remaining consumer work.

# Stop Conditions

Stop for router validation failure or unlocatable authoritative source artifacts.
Block the whole task for unavailable MCP only when all six conditions in
`.codex/references/inheritance/explicit-mcp-blockers.md` are true. Otherwise block
only the affected stage and continue safe work.

# Reports

Write inheritance reports under `reports/inheritance/mails/` and reviews under
`reports/reviews/mails/`, including clone fidelity and applicable serialized-asset
and dependency-closure reviews plus standalone portability.
