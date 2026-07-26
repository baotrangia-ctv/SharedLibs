---
name: review-clone-fidelity
description: Verify that a source-to-shared Stage A clone faithfully captures the latest active behavior, contracts, assets, lifecycle, events, and dependency closure before Stage B genericization. Use for every source-to-shared inheritance.
---

# Purpose

Make faithful capture an explicit gate before shared-module refactoring.

# Required Inputs

- source feature-surface and active API inventories
- Stage A clone inventory
- serialized-asset and dependency reviews when applicable
- behavior-change and omission records

# Workflow

1. Read `.codex/references/inheritance/repository-first.md`.
2. Read `.codex/references/inheritance/clone-first-workflow.md`.
3. Read `.codex/references/inheritance/clone-fidelity.md`.
4. Read `.codex/references/inheritance/faithful-clone-mode.md`.
5. Read `.codex/references/inheritance/standalone-portability.md`.
6. Verify latest-active selection and compatibility evidence.
7. Compare source and clone behavior, APIs, config, CSV, lifecycle, Manager actions,
   HUD, serialized assets, events, integrations, and dependencies.
8. Confirm unknown serialized values were preserved safely and dependencies were
   inventoried.
9. Confirm source-specific dependencies were preserved and classified before
   refactoring.
10. Confirm removals, abstractions, remapping, and simplified replacements have
   evidence and compatibility notes.
11. Report clone fidelity separately from standalone portability and runtime
    validation.

# Stage B Gate

Assign one Stage A result:

- `Pass`: active source behavior and required artifacts are captured, unknowns are
  structurally preserved, dependencies are inventoried, and no behavior is silently
  discarded.
- `Pass, source-compatible`: clone fidelity passes while standalone portability is
  partial or consumer adaptation remains.
- `Pass with runtime verification pending`: clone fidelity passes while only live
  runtime checks remain.
- `Fail`: required behavior, contracts, assets, lifecycle, events, dependencies, or
  evidence were discarded or are structurally invalid for the faithful clone; or an
  unjustified simplified replacement exists.

Do not begin Stage B on `Fail`. Resolve the finding or obtain an explicit,
documented scope decision that includes compatibility and rollback consequences.

# Allowed Changes

Modify only `reports/reviews/[module]/clone-fidelity-review.md`. Do not edit source,
clone, or shared implementation files during this review.

# Required Evidence

Include repository-relative paths and symbols, active-version call sites, preserved
unknowns, omitted-artifact reasons, dependency and serialized review results, faithful
clone status, standalone-portability status, and runtime-verification status.

# Stop Conditions

Stop the review only when source evidence or the Stage A inventory is unavailable.
When the inventory exists but the clone omits an artifact, report `Fail` rather than
stopping the review. Partial standalone portability and a pending live Studio run do
not fail a structurally valid faithful clone.
