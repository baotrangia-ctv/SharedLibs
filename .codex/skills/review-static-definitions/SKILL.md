---
name: review-static-definitions
description: Review repeated fields, statuses, result codes, action identifiers, config keys, and state constants for correct local, Manager-private, Config, feature-definition, or shared placement without over-fragmentation.
---

# Purpose

Centralize reusable feature contracts while keeping local implementation details local and avoiding one-file-per-constant sprawl.

# Required Inputs

- Module Manager, Config, HUD, model, status, constants, and event files
- Public contract and call-site inventory
- Target folder architecture

# Expected Outputs

- Findings for duplicated, misplaced, inline, or fragmented definitions
- One placement recommendation per definition group
- Consolidation plan for excessive tiny definition files

# Main Workflow

1. Inventory `FIELD_*`, `STATUS_*`, action, result, config-key, state, and duplicated string or numeric definitions.
2. Trace every definition's call sites across Manager, Config, HUD, events, analytics, and other modules.
3. Apply `references/definition-decision-tree.md`.
4. Detect constants that should remain local or private.
5. Detect reused definitions that should move to a cohesive Config or feature definition file.
6. Detect feature-specific constants misplaced in Utils.
7. Detect and merge over-fragmented definition files.
8. Report exact moves without editing source during a review-only task.

# Reference-Loading Conditions

- Read `references/definition-decision-tree.md` for every review.

# Combination Rules

- Combine with source-to-shared workflows that introduce repeated fields, statuses, actions, config keys, states, or result codes.
- Combine with shared-to-consumer workflows when shared definitions must map to consumer definitions.
- Combine with `review-folder-architecture` when definition files are misplaced.

# Allowed Files to Inspect

- Module Manager, Config, HUD, model, constants, status, action, event, and utility files
- Public API and persistence schemas
- Consumer definition files when integration is in scope

# Allowed Files to Modify

- Review output files only

# Commands

- Use `rg -n` for declaration patterns, repeated literals, imports, and cross-layer call sites.
- Search by both symbolic name and literal value before classifying a definition as shared or duplicate.

# Safety Constraints

- Do not centralize a constant solely because its name is uppercase.
- Do not expose private implementation details as public contracts.
- Do not create one file per constant.
- Do not place feature-specific definitions in generic Utils.
- Place feature Config and public feature definition files under `Assets/Scripts/Configs/` unless an established target-project convention documents another responsibility-equivalent layer.
- Do not change persisted field keys or public status values without compatibility analysis.

# Required Evidence

- Definition name or literal
- Declaration and call-site paths
- Current scope
- Required scope
- Compatibility impact
- Recommended placement

# Stop Conditions

- Definition call sites cannot be located
- Persisted or public values cannot be changed safely
- Ownership between feature and shared contracts is unresolved

# Report Format and Destination

Use only these recommendations:

- `Keep local`
- `Keep private in Manager`
- `Move to Config definitions`
- `Move to feature definitions`
- `Move to shared definitions`
- `Merge fragmented definition files`

Write results to `reports/reviews/[module-name]/static-definitions-review.md` or the relevant consumer integration report directory.
