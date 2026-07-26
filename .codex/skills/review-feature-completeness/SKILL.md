---
name: review-feature-completeness
description: Review every applicable feature surface after clone-first inheritance, including scripts, serialized assets, config, data, events, localization, dependencies, and consumer integration points. Use for every source-to-shared inheritance.
---

# Purpose

Verify that a source-to-shared inheritance considered all required feature layers instead of inheriting only the primary Manager logic.

# Trigger Conditions

- Every source-to-shared inheritance
- Any corrective inheritance task where required UI, config, CSV, or persistence layers may have been omitted

# Required Inputs

- Source feature-surface inventory
- Inheritance report draft
- Target SharedLibs module files

# Expected Outputs

- Completeness findings using the shared finding format
- A status for every applicable feature surface
- A separate faithful-clone, standalone-portability, and runtime status
- `Unnecessary Demo Artifacts` findings
- Evidence labels and a non-blocking Studio-verification gap list

# Path Validation Requirement

- Respect router-validated source and target roots.
- Do not widen scope to unvalidated repositories.

# Main Workflow

1. Confirm the feature-surface inventory exists.
2. Confirm repository scripts, readable serialized assets, dependencies, reports,
   and documentation were inspected before MCP.
3. Verify and report these surfaces independently:
   - Manager
   - Config
   - CSV
   - Persistence
   - Actions
   - Events
   - HUD script
   - Serialized HUD asset
   - Textures
   - Utilities
   - Custom components
   - Custom enums
   - Standalone portability
   - Runtime verification
4. Verify files map to architectural layers and no mixed feature folder exists.
5. Verify the generated source set is the smallest complete dependency closure.
6. Verify existing utilities and static-definition ownership were considered.
7. Identify `Unnecessary Demo Artifacts`.
8. Verify every adapter has concrete justification.
9. Compare the inventory with generated target files.
10. Verify every important finding uses an evidence label from the repository-first
    reference.
11. Assign Manager through Custom enums exactly one stage status:
    - `Complete`
    - `Complete with unresolved bindings`
    - `Partially complete`
    - `Blocked`
    - `Not applicable`
    - `Runtime verification pending`
12. Assign Standalone portability one status from
    `.codex/references/inheritance/standalone-portability.md`.
13. Assign Runtime verification one status from
    `.codex/references/inheritance/runtime-verification.md`.
14. Reject an invented simplified replacement when a readable source asset exists.
15. Report missing or silently omitted required behavioral or serialized surfaces.
16. Do not mark the entire feature incomplete because one presentation or portability
    surface is unresolved.
17. Record faithful clone fidelity, standalone portability, and runtime verification
    separately.

# Studio and MCP Review Policy

- Do not fail completeness solely because Studio or MCP was unavailable.
- Do not require Studio to inspect CSV files or parsing code available on disk.
- Treat live rendering, registration, and runtime-only bindings as Studio-verification
  gaps unless they meet all six strict conditions in
  `.codex/references/inheritance/explicit-mcp-blockers.md`.
- Treat serialized hierarchy, properties, bindings, and references as repository
  evidence, not Studio-only details.
- Treat unknown but structurally preserved custom values as a complete clone surface
  with unresolved bindings, not automatic invalidity.
- Do not accept runtime claims without the corresponding live validation.

# Code-Tracing Order

```text
Repository feature surface
    ->
Latest active implementation
    ->
Serialized assets and dependency closure
    ->
Manager, Load Data, Save Data, and Actions
    ->
HUD and UI assets
    ->
Config readers and CSV
    ->
Utils and dependencies
    ->
Events and callbacks
    ->
Primary flow validation
    ->
Portability artifacts
```

# Reference-Loading Conditions

- Read `.codex/rules/studio-mcp-inheritance-policy.md` before evaluating Studio availability, evidence labels, fallback behavior, or Studio-related stop conditions.
- Read `.codex/references/inheritance/repository-first.md` for every review.
- Read `.codex/references/inheritance/clone-first-workflow.md` for every review.
- Read `.codex/references/inheritance/runtime-verification.md` for every review.
- Read `.codex/references/inheritance/preserve-first-bindings.md` for serialized
  custom values.
- Read `.codex/references/inheritance/stage-based-completion.md` for every review.
- Read `.codex/references/inheritance/standalone-portability.md` for every review.
- Read `references/feature-surface-checklist.md` for every source-to-shared inheritance.
- Read `references/config-and-csv-checklist.md` when the source feature uses config readers or CSV data.
- Read `references/hud-and-ui-checklist.md` when the source feature has any user-facing HUD or UI flow.
- Read `references/manager-organization-checklist.md` when the feature has a primary Manager or persistent runtime state.

# Combination Rules

- Always combine with a source-to-shared module workflow skill.
- Always combine with `review-folder-architecture`.
- Always combine with `review-clone-fidelity`.
- Always combine with `review-standalone-portability`.
- Combine with `review-serialized-asset-fidelity` when readable serialized assets
  exist.
- Combine with `review-asset-dependency-closure` when files or assets reference other
  artifacts.
- Combine with `review-utility-reuse` when structured data is processed.
- Combine with `review-static-definitions` when repeated or cross-layer definitions exist.
- Usually combine with `review-request-check-process`.
- Combine with `review-data-lifecycle` when persistence, cache, readiness, or reconnect behavior exists.
- Combine with `review-active-api-surface` when versioned or legacy APIs exist.

# Allowed Files to Inspect

- Source Manager, HUD, Config, Utils, and CSV files
- Source and target readable serialized assets, localization, components, and
  dependency inventories
- Target SharedLibs module files
- Inheritance reports
- Portability manifests

# Allowed Files to Modify

- Review output files only

# Required Evidence

- Repository-relative file paths
- Feature-surface inventory entries
- Target file coverage evidence
- Missing-layer comparisons
- Final source file set and intentionally omitted files
- Unnecessary demo-artifact findings
- Utility reuse, static-definition, and adapter decisions
- Evidence labels for important findings
- Serialized clone status, runtime-verification status, MCP usage, and remaining
  Studio-only gaps
- Stage completion summary and standalone-portability status

# Stop Conditions

- Feature-surface inventory is missing
- Source feature files cannot be located after repository-accessible evidence is exhausted
- Missing evidence blocks the review itself; individual surfaces may remain blocked
  with exact evidence while other surfaces complete

Do not stop solely because a custom meaning is unknown, standalone portability is
partial, or runtime Studio verification was not performed.

# Report Format and Destination

- Use the shared finding format.
- Write results to `reports/reviews/[module-name]/feature-completeness-review.md`.
