---
name: review-serialized-asset-fidelity
description: Compare readable serialized source and target assets for structural, identity, property, binding, reference, and dependency fidelity. Use for every inheritance or consumer integration involving serialized assets.
---

# Purpose

Detect silent asset simplification, lost serialized data, broken remapping, and
unjustified source-to-target differences.

# Required Inputs

- validated source and target roots
- serialized source asset path and expected target asset path
- dependency inventory and ID-remapping record

# Workflow

1. Read `.codex/references/inheritance/repository-first.md`.
2. Read `.codex/references/inheritance/serialized-assets.md`.
3. Read `.codex/references/inheritance/preserve-first-bindings.md`.
4. Read `.codex/references/inheritance/repository-definition-search.md`.
5. Parse the source and any existing target as structured data without normalizing
   away unknown fields.
6. Search source and shared repositories for custom enum, component, script, utility,
   property, registration, metadata, asset, and import definitions.
7. Compare root type, hierarchy, names, counts, IDs, ordering, components, states,
   transforms, references, text, localization, layouts, controls, scripts, custom
   data, events, enums, tags, layers, and versions where applicable.
8. Trace utility and asset dependencies and every remapped ID or reference.
9. Classify each relevant value:
   - `Preserved unchanged`
   - `Copied with definition`
   - `Path-adjusted`
   - `Adapted`
   - `Isolated`
   - `Unresolved but structurally preserved`
   - `Requires runtime verification`
   - `Structurally invalid`
10. Require evidence for every remap, deletion, adaptation, or invalidity finding.
11. Flag invented simplified replacements and separate fidelity, portability, and
    runtime findings.

# Allowed Changes

Modify only `reports/reviews/[module]/serialized-asset-fidelity-review.md`. Do not
edit assets during this review.

# Required Evidence

Include repository-relative source, target, definition, usage, utility, and asset
paths; identifiers; preservation or remapping evidence; structural-validity decision;
portability impact; and runtime-verification status.

# Stop Conditions

Stop the review only when validated roots or required source evidence are missing.
When the expected target asset is absent, classify it as `Missing`, produce a failed
fidelity report for that asset stage. Report malformed or unreadable structured data
as a finding; do not repair or discard it. An unknown but structurally preserved
binding does not fail clone fidelity. Block only under
`.codex/references/inheritance/explicit-mcp-blockers.md`.
