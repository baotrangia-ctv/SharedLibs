---
name: review-inherited-module
description: Review đa năng cho module vừa inherit (source→shared hoặc shared→consumer). Chọn section theo tình huống thay vì chọn skill riêng.
---

# Purpose

Review an inherited module through the applicable sections below. This skill
replaces the separate review skills without changing their review boundaries,
evidence requirements, report destinations, or safety constraints.

# How to choose sections

Always run:

- Clone Fidelity
- Standalone Portability
- Feature Completeness
- Folder Architecture

Add sections when the module has the corresponding surface:

- Readable serialized assets → Serialized Asset Fidelity.
- References to other scripts, assets, configs, CSV, localization, components,
  events, services, or engine resources → Asset Dependency Closure.
- Duplicate, versioned, legacy, deprecated, compatibility-only, or superseded
  APIs → Active API Surface.
- Parsing, serialization, conversion, migration, or structured-data storage →
  Utility Reuse.
- Repeated fields, statuses, actions, result codes, config keys, or state
  identifiers → Static Definitions.
- Public Manager actions or user-triggered operations → Request-Check-Process.
- Persistence, cache, readiness, reconnect, quit, shutdown, or persistent
  rewards → Data Lifecycle.
- Real production integration, release rollout, or replacement of demo systems →
  Production Readiness.

The selected sections must be recorded in the applicable inheritance or review
report. Each section keeps clone fidelity, standalone portability, and runtime
verification as separate statuses.

# Common review rules

- Respect router-validated source, target, and consumer roots; do not widen
  scope to unvalidated repositories.
- Use repository-relative paths, symbols, call sites, and explicit evidence.
- Inspect repository evidence before MCP. Use
  `.agent/references/inheritance/explicit-mcp-blockers.md` before claiming an
  MCP blocker.
- Review-only sections modify review output files only. Do not edit source,
  target implementation, serialized assets, or dependencies during review.
- Preserve unknown but structurally valid serialized values and bindings; unknown
  meaning is not structural invalidity.
- Do not invent simplified replacements when readable source assets exist.
- Keep reports under `reports/inheritance/[module]/` and
  `reports/reviews/[module]/` or the applicable existing consumer/bootstrap
  destination.
- Use the shared finding format and report severity, confidence, category,
  impact, evidence, and validation where applicable.

## Section: Clone Fidelity

### Apply when

Run for every inherited module. It verifies that the Stage A clone captured the
latest active behavior before Stage B genericization.

### Required inputs

- Source feature-surface and active-API inventories.
- Stage A clone inventory.
- Serialized-asset and dependency reviews when applicable.
- Behavior-change and omission records.

### Review

1. Read `.agent/references/inheritance/repository-first.md`,
   `clone-first-workflow.md`, `clone-fidelity.md`, `faithful-clone-mode.md`,
   and `standalone-portability.md`.
2. Verify latest-active selection and compatibility evidence.
3. Compare source and clone behavior, APIs, config, CSV, lifecycle, Manager
   actions, HUD, serialized assets, events, integrations, and dependencies.
4. Confirm unknown serialized values and source-specific dependencies were
   preserved and classified before refactoring.
5. Require evidence for removals, abstractions, remapping, and simplified
   replacements.
6. Report clone fidelity separately from portability and runtime validation.

### Stage A result

Assign one result: `Pass`, `Pass, source-compatible`, `Pass with runtime
verification pending`, or `Fail`. Do not begin Stage B on `Fail`; resolve the
finding or document an explicit scope decision with compatibility and rollback
consequences.

### Report

Write `reports/reviews/[module]/clone-fidelity-review.md` with paths and symbols,
active call sites, preserved unknowns, omission reasons, dependency and
serialized review results, clone status, portability status, and runtime status.

## Section: Standalone Portability

### Apply when

Run for every inherited module after clone fidelity and when preparing a module
for consumer reuse. Report portability independently from clone fidelity.

### Review

1. Read `.agent/references/inheritance/standalone-portability.md`,
   `stage-based-completion.md`, and `repository-definition-search.md`.
2. Inventory remaining source utilities, services, components, enums, bindings,
   assets, consumer integration points, and runtime-only dependencies.
3. Mark every dependency required or optional.
4. Decide copy, reuse, extract, adapt, isolate, defer, MCP, or runtime
   verification handling.
5. Assign the reference-defined portability and stage statuses.
6. Report exact blockers without changing clone-fidelity status.

### Report

Write `reports/reviews/[module]/standalone-portability-review.md` with definitions
and usages, required/optional status, handling decision, consumer responsibility,
exact blockers, portability status, stage statuses, and runtime status.

## Section: Feature Completeness

### Apply when

Run for every source-to-shared inheritance and corrective inheritance task where
UI, config, CSV, persistence, or other layers may be omitted.

### Review

1. Confirm the feature-surface inventory exists.
2. Confirm repository scripts, readable serialized assets, dependencies, reports,
   and documentation were inspected before MCP.
3. Compare the target against these surfaces independently: Manager, Config, CSV,
   Persistence, Actions, Events, HUD script, serialized HUD asset, Textures,
   Utilities, custom components, custom enums, standalone portability, and
   runtime verification.
4. Verify architectural layers, smallest complete dependency closure, utility
   reuse, static-definition ownership, adapters, and unnecessary demo artifacts.
5. Compare inventory entries with generated target files and record missing or
   silently omitted behavioral or serialized surfaces.
6. Assign Manager-through-Custom-enums statuses from the source workflow and keep
   faithful clone, portability, and runtime statuses separate.

### Evidence and Studio policy

Read `.agent/references/inheritance/repository-first.md`,
`clone-first-workflow.md`, `runtime-verification.md`,
`preserve-first-bindings.md`, `stage-based-completion.md`, and
`standalone-portability.md`. Read the local feature, config/CSV, HUD/UI, or
Manager checklists when their conditions apply.

Do not fail completeness solely because Studio/MCP is unavailable. Treat live
rendering, registration, and runtime-only bindings as verification gaps unless
all strict MCP-blocker conditions apply. Serialized hierarchy, properties,
bindings, references, and unknown structurally preserved values remain repository
evidence.

### Report

Write `reports/reviews/[module]/feature-completeness-review.md` with surface
coverage, target-file evidence, omissions, demo-artifact findings, utility and
adapter decisions, evidence labels, serialized/runtime status, MCP gaps, stage
summary, and portability status.

## Section: Folder Architecture

### Review

1. Inventory module source, asset, report, and skill-reference files.
2. Assign one responsibility to each file.
3. Read `references/folder-mapping.md` and map each responsibility.
4. Detect mixed feature folders, misplaced reports, unclear filenames, and
   layer-crossing files.
5. Evaluate feature-subfolder exceptions for layer locality, convention,
   justification, and grouping need.
6. Recommend exactly `Move`, `Split`, `Remove`, or `Retain with documented
   exception`.

Do not move files during a review-only task. Do not recommend a folder solely
because the source project used it. Use `rg --files`, `Get-ChildItem -Force`, and
`rg -n` as appropriate.

### Report

Write `reports/reviews/[module]/folder-architecture-review.md` or the relevant
consumer integration report with current responsibility, current folder, target
folder, decision, and evidence for every finding.

## Section: Serialized Asset Fidelity

### Apply when

Run when readable serialized assets are part of the inheritance or consumer
integration.

### Review

1. Read `.agent/references/inheritance/repository-first.md`,
   `serialized-assets.md`, `preserve-first-bindings.md`, and
   `repository-definition-search.md`.
2. Parse source and target as structured data without dropping unknown fields.
3. Search definitions for custom enums, components, scripts, utilities,
   properties, registrations, metadata, assets, and imports.
4. Compare root type, hierarchy, names, counts, IDs, ordering, components,
   states, transforms, references, text, localization, layouts, controls,
   scripts, custom data, events, enums, tags, layers, and versions where
   applicable.
5. Trace dependencies and every remapped ID/reference.
6. Classify values as preserved, copied with definition, path-adjusted, adapted,
   isolated, unresolved-but-preserved, runtime verification required, or
   structurally invalid.
7. Require evidence for every remap, deletion, adaptation, or invalidity finding.

If the expected target asset is absent, report the asset stage as `Missing` and
failed fidelity. Do not repair or discard malformed data in this review.

### Report

Write `reports/reviews/[module]/serialized-asset-fidelity-review.md` with source,
target, definition, usage, utility, asset paths, identifiers, preservation or
remapping evidence, structural validity, portability impact, and runtime status.

## Section: Asset Dependency Closure

### Apply when

Run whenever inherited files or assets reference other artifacts.

### Review

1. Read `.agent/references/inheritance/repository-first.md`,
   `dependency-closure.md`, `repository-definition-search.md`, and
   `stage-based-completion.md`.
2. Parse paths, asset IDs, scripts, components, config/CSV, localization, events,
   services, and engine-library references.
3. Follow local references transitively and inspect utility API usage.
4. Validate relative textures and file paths; distinguish local from engine-owned
   dependencies.
5. Search source, shared, and applicable consumer repositories for definitions
   and equivalents.
6. Classify dependencies as existing/copyable, existing/reusable,
   source-specific, extractable definition, engine-owned, missing, MCP-required,
   or runtime-verification-required.
7. Flag incomplete closure, unrelated bulk copying, affected stages, and safe
   independent work.

Do not copy or edit dependencies during this review. Do not block an entire asset
for one optional unresolved dependency; require exact MCP-blocker evidence.

### Report

Write `reports/reviews/[module]/asset-dependency-closure-review.md` with all
referencing, definition, and referenced paths; dependency type; required/optional
status; classification; target handling; texture/utility analysis; affected
stage; and the smallest-complete-set conclusion.

## Section: Active API Surface

### Apply when

Run when duplicate, versioned, legacy, deprecated, compatibility-only, or
superseded APIs may exist.

### Review

1. Identify `V2`, `V3`, `Legacy`, `Old`, `Deprecated`, `New`, feature-flagged,
   commented, disabled, or similarly named alternatives.
2. Trace active call sites through HUD, Manager, config, event registration,
   runtime entry points, flags, compatibility, and migration paths.
3. Classify each API as Active, Latest active, Compatibility-only, Deprecated,
   Unused, Demo-only, or Needs verification.
4. Verify whether older APIs remain required and report which APIs to inherit,
   isolate, or omit.

Load the active-API inventory, version-selection, and deprecation checklists when
their conditions apply. Combine with Feature Completeness when omitted versions
may affect the feature surface.

### Report

Write `reports/reviews/[module]/active-api-review.md` using repository-relative
paths, API names, call-site and runtime evidence, and compatibility evidence when
an API is retained.

## Section: Utility Reuse

### Apply when

Run when the module parses, serializes, converts, migrates, or stores structured
data.

### Review

1. Inventory parsing, serialization, list/map, JSON-like, split/join, conversion,
   defaults, and migration logic.
2. Inspect the current `Assets/Scripts/Utils/DataUtils.fcg` and other relevant
   SharedLibs utilities; do not rely on stale reports or memory.
3. Compare signatures, behavior, delimiters, defaults, mutation, encoding, and
   compatibility requirements.
4. Choose one decision from `references/utility-decision-checklist.md`.
5. Flag generic Manager helpers, duplicate wrappers, copied source utilities,
   and missed existing APIs.

Use only: `Reuse existing utility`, `Extend existing utility`, `Keep
feature-local`, `Remove duplicate`, or `Needs compatibility wrapper`. Do not
change canonical encoding or add feature-specific behavior to a generic utility.

### Report

Write `reports/reviews/[module]/utility-reuse-review.md` with helper paths,
existing API paths and signatures, behavioral comparison, call sites,
compatibility requirement, decision, and rationale.

## Section: Static Definitions

### Apply when

Run when the module introduces or reuses fields, statuses, action identifiers,
result codes, config keys, state constants, or duplicated literals.

### Review

1. Inventory `FIELD_*`, `STATUS_*`, action, result, config-key, state, and
   duplicated string or numeric definitions.
2. Trace declarations across Manager, Config, HUD, events, analytics, and other
   modules.
3. Read `references/definition-decision-tree.md`.
4. Detect definitions that should remain local/private, move to Config or feature
   definitions, move to shared definitions, or merge fragmented files.
5. Report exact moves without editing source during review.

Use only these recommendations: `Keep local`, `Keep private in Manager`, `Move
to Config definitions`, `Move to feature definitions`, `Move to shared
definitions`, or `Merge fragmented definition files`. Do not centralize solely
because a name is uppercase, expose private implementation details, create one
file per constant, or change persisted/public values without compatibility
analysis.

### Report

Write `reports/reviews/[module]/static-definitions-review.md` or the relevant
consumer report with definition/literal, declaration and call sites, current and
required scope, compatibility impact, and placement recommendation.

## Section: Request-Check-Process

### Apply when

Run when the module exposes user actions, public Manager operations, rewards,
state mutations, or persistence through public APIs.

### Review

1. Identify every public action or user-triggered operation.
2. Trace HUD or external caller to Manager `Request`.
3. Verify `Request` calls `Check`, `Check` is read-only, and `Process` owns
   authoritative mutation and persistence.
4. Verify failure does not partially mutate state.
5. Verify one-time actions are idempotent or protected from duplicate execution.

Read `references/action-flow-checklist.md` for public actions and
`references/idempotency-cases.md` for rewards, purchases, progression, or
duplicate-call risks.

### Report

Write `reports/reviews/[module]/request-check-process-review.md` or the applicable
bootstrap report with entry points, Request/Check/Process call sites, mutation,
persistence, and required validation evidence.

## Section: Data Lifecycle

### Apply when

Run when the module loads/saves player data, maintains runtime cache, registers
readiness, handles reconnect, quit, shutdown, persistent rewards, or progression.

### Review

Trace in order: player join → database load → default-data creation → cache
initialization → database-ready signal → feature initialization → runtime updates
→ save → disconnect → reconnect → player quit → server shutdown.

Load only the lifecycle references required by observed behavior:
`references/load-save-lifecycle.md`, `cache-invariants.md`, `reconnect-cases.md`,
`rollback-cases.md`, and `known-incidents.md`. Classify findings with severity,
confidence, category, impact, and validation.

Combine with Request-Check-Process for public actions and Production Readiness
when real systems replace demos. A module with no persistence, cache, readiness,
reconnect, or shutdown behavior is `Not applicable`, not a blocked review.

### Report

Write `reports/reviews/[module]/lifecycle-review.md` or
`reports/bootstrap/validation-report.md` for bootstrap tasks with lifecycle
order, relevant callbacks, readiness, cache, and save/load call-site evidence.

## Section: Production Readiness

### Apply when

Run when demo persistence or rewards are replaced, real persistence/rewards are
connected, consumer business logic is introduced, or the feature is intended for
release.

### Review

1. Confirm the task moved beyond demo-only behavior.
2. Identify remaining mocks, demo handlers, and placeholder integrations.
3. Verify real system connections and justify retained adapters under
   Adapter-Last.
4. Review config completeness, persistence integration, failure handling,
   logging, rollback instructions, and known limitations.
5. Record release blockers and required validation steps.

Load `references/demo-replacement-checklist.md`, `release-readiness.md`, and
`rollback-readiness.md` when their conditions apply. Combine with Data Lifecycle
for persistence/cache and Request-Check-Process for public actions. A task that
is still purely demo-only is `Not applicable`, not a production failure.

### Report

Write `reports/reviews/[module]/production-readiness-review.md` or the existing
consumer integration validation report with remaining demo behavior, real adapter
and persistence call sites, rollback evidence, release limitations, and blockers.
