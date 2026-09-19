---
name: source-to-shared-router
description: Route source-project to SharedLibs inheritance through repository definition search, preserve-first faithful cloning, safe stage completion, clone and portability reviews, exact MCP-last blockers, and mandatory paired module-skill generation.
---

# Purpose

Route every source-to-shared inheritance to one module workflow and the smallest
sufficient common review set. Keep module behavior out of the router.

# Required Inputs

- user request and module name
- `.agent/project-paths.json`

# Path Validation

Before source inspection or target modification:

1. Resolve and normalize configured source and SharedLibs paths.
2. Verify both roots and repository markers.
3. Verify the roots differ.
4. Verify the source is read-only and SharedLibs is read-write.
5. Stop before modification when validation fails.

# Intake Gate (Mandatory First Action)

Before reading source implementation files or writing any file outside
`reports/`, create `reports/inheritance/[module]/00-intake.md` using
`references/intake-record-template.md`. It must record:

- The validated source and SharedLibs roots and access modes from Path
  Validation.
- Confirmation this request routes through `source-to-shared-router`, not
  `shared-to-consumer-router`.
- The selected `[module]-source-to-shared` skill, or a note that it is
  missing and must be created from templates.
- Every file actually opened from `# Required Common References` below,
  listed by path.
- Every user-specified exclusion (a named sub-feature to leave out) and the
  dependency-closure check confirming whether the excluded feature shares a
  Manager, config, utility, or serialized asset with the included scope.

Do not modify any file outside `reports/` until `00-intake.md` exists and
lists every required reference actually loaded. A missing or incomplete
intake record is a Stop Condition, identical to an invalid path.

# Workflow

```text
Validate configured source and target paths
    ->
Write the mandatory 00-intake.md intake record
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

# Auto-pair Skill Generation

After every completed source-to-shared inheritance, always generate both module
workflow skills:

- `[module]-source-to-shared`
- `[module]-shared-to-consumer`

The shared-to-consumer skill must be generated from the evidence already collected
during source-to-shared work: feature surface, public contract, and complete
dependency closure. Do not require reading the original source project again to
generate the paired consumer skill. This pair is mandatory and is not optional
when only one direction was explicitly requested.

# Required Common References

Load these before routing implementation work:

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

Load `serialized-assets.md`, `dependency-closure.md`, and `clone-fidelity.md` when
their corresponding stage or review begins. Module skills load only their own
feature-specific references.

# Review Routing

- Always use `review-inherited-module` sections: Clone Fidelity, Standalone
  Portability, Feature Completeness, and Folder Architecture.
- Use the Serialized Asset Fidelity section for readable serialized assets.
- Use the Asset Dependency Closure section for referenced files or assets.
- Use the Active API Surface section for duplicate, versioned, legacy, deprecated,
  or compatibility APIs.
- Use the Utility Reuse section for structured-data processing.
- Use the Static Definitions section for repeated or cross-layer definitions.
- Use the Request-Check-Process section for public Manager actions.
- Use the Data Lifecycle section for persistence, cache, readiness, reconnect, quit,
  shutdown, or persistent rewards.
- Use the Production Readiness section only for release-facing work.
- Select no demo skill by default.

# Required Evidence

Record the `00-intake.md` path and completeness, validated roots and modes, repository markers, selected module skill and
reviews, repository paths inspected, active implementation evidence, artifact
classifications, definition searches, dependency closure, preserve/remap decisions,
stage statuses, faithful clone status, clone fidelity, standalone portability, Stage
B changes, safe files, utility and texture analysis, exact MCP blockers, runtime
status, and Studio-only gaps.

# Allowed Scope

Inspect validated source evidence, SharedLibs files, rules, skills, references, and
reports. Modify only the validated SharedLibs target after path validation.

# Stop Conditions

Stop routing for invalid paths, same source and target, incorrect access modes, a
missing or incomplete `00-intake.md` record, or a missing module workflow outside
creation scope.

A missing root, authoritative artifact, or transitive dependency blocks only its
affected stage by default. Search validated roots, preserve or isolate when safe,
report it, and continue independent stages.

Block the whole inheritance because MCP is unavailable only when all six conditions
in `.agent/references/inheritance/explicit-mcp-blockers.md` are true. Otherwise block
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
