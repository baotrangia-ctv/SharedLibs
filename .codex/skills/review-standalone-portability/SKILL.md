---
name: review-standalone-portability
description: Evaluate whether a faithfully cloned shared module can operate without source-project infrastructure, and classify remaining utilities, components, enums, integrations, target equivalents, and runtime dependencies. Use for every source-to-shared inheritance after clone fidelity and when preparing a module for consumer reuse.
---

# Purpose

Report standalone portability independently from clone fidelity.

# Required Inputs

- faithful clone and clone-fidelity report
- dependency and repository-definition inventories
- source-specific and consumer integration decisions

# Workflow

1. Read `.codex/references/inheritance/standalone-portability.md`.
2. Read `.codex/references/inheritance/stage-based-completion.md`.
3. Read `.codex/references/inheritance/repository-definition-search.md`.
4. Inventory remaining source-project utilities, services, components, enums,
   bindings, assets, consumer integration points, and runtime-only dependencies.
5. Mark every dependency required or optional.
6. Determine copy, reuse, extract, adapt, isolate, defer, MCP, or runtime-verification
   handling.
7. Assign one portability status and exact stage statuses from the shared references.
8. Report exact blockers without changing clone-fidelity status.

# Allowed Changes

Modify only `reports/reviews/[module]/standalone-portability-review.md`. Do not edit
source or implementation files during this review.

# Required Evidence

Include repository-relative definitions and usages, required or optional status,
handling decision, consumer responsibility, exact blockers, portability status,
stage statuses using only the shared vocabulary, and runtime-verification status.

# Stop Conditions

Stop the review only when the faithful clone or dependency inventory is unavailable.
Unknown but structurally preserved values, partial portability, and pending runtime
verification are reportable results, not review blockers.
