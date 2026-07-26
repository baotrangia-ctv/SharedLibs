---
name: review-utility-reuse
description: Review modules that parse, serialize, convert, migrate, or store structured data for missed DataUtils reuse, copied utilities, generic feature-local helpers, unnecessary wrappers, and encoding compatibility needs.
---

# Purpose

Prevent duplicated data-format logic and ensure modules reuse existing SharedLibs utilities before adding helpers.

# Required Inputs

- Generated or proposed module files
- `Assets/Scripts/Utils/DataUtils.fcg`
- Other relevant files under `Assets/Scripts/Utils/`
- Source encoding and compatibility requirements

# Expected Outputs

- Utility findings with exact existing APIs and call sites
- One decision per helper: reuse, extend, keep feature-local, remove, or add compatibility wrapper
- Documented canonical and legacy encoding boundaries

# Main Workflow

1. Inventory parsing, serialization, list, map, JSON-like, split, join, conversion, default-value, and migration logic in the module.
2. Inspect `DataUtils.fcg` before evaluating new helpers.
3. Inspect other relevant SharedLibs utilities.
4. Compare signatures, behavior, delimiters, defaults, mutation behavior, and compatibility requirements.
5. Select one decision from `references/utility-decision-checklist.md`.
6. Flag generic helpers inside Managers, duplicate wrappers, copied source utilities, and missed existing APIs.
7. Record any justified extension or compatibility wrapper.

# Reference-Loading Conditions

- Read `references/utility-decision-checklist.md` for every review.
- Read the current `Assets/Scripts/Utils/DataUtils.fcg`; do not rely on a stale API list in reports or memory.

# Combination Rules

- Combine with source-to-shared workflows when structured data is parsed, serialized, converted, migrated, or stored.
- Combine with shared-to-consumer workflows when data formats or utilities are adapted.
- Combine with `review-data-lifecycle` when encoding affects persisted state.

# Allowed Files to Inspect

- `Assets/Scripts/Utils/DataUtils.fcg`
- Other SharedLibs or consumer utility files
- Module Manager, Config, model, status, and helper files
- Persistence schemas and migration documentation

# Allowed Files to Modify

- Review output files only

# Commands

- Use `rg -n` for helper declarations, imports, and call sites.
- Search `DataUtils` and other Utils by behavior and candidate function name before concluding an API is missing.

# Safety Constraints

- Do not change canonical encoding during a review.
- Do not recommend `DataUtils` reuse without comparing behavior and compatibility.
- Do not extend `DataUtils` with feature-specific behavior.
- Do not add an adapter or wrapper without a concrete representation or compatibility need.

# Required Evidence

- Generated helper or duplicated logic path
- Existing utility path and exact API, when available
- Behavioral comparison
- Call-site evidence
- Compatibility requirement
- Decision and rationale

# Stop Conditions

- `DataUtils.fcg` or the relevant utility root cannot be inspected
- Required encoding behavior cannot be determined safely
- Persistence compatibility is unresolved and a recommendation could corrupt data

# Report Format and Destination

Use only these recommendations:

- `Reuse existing utility`
- `Extend existing utility`
- `Keep feature-local`
- `Remove duplicate`
- `Needs compatibility wrapper`

Write results to `reports/reviews/[module-name]/utility-reuse-review.md` or the relevant consumer integration report directory.
