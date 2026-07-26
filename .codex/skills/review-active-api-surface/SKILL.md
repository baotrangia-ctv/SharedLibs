---
name: review-active-api-surface
description: Review versioned, duplicate, legacy, deprecated, compatibility-only, and superseded APIs to identify the latest active implementation and prevent copying every historical version.
---

# Purpose

Identify the active source API surface and prevent inheritance of obsolete or superseded implementations by default.

# Trigger Conditions

- The source contains `V2`, `V3`, `Legacy`, `Old`, `Deprecated`, or `New`
- Multiple similarly named APIs exist
- Commented or disabled alternatives exist
- Feature-flagged implementations exist
- Several implementations appear to support the same user flow

# Required Inputs

- Source Manager, HUD, Config, and integration files
- API inventory draft

# Expected Outputs

- Active API review findings using the shared finding format
- An API inventory with status and inheritance decisions

# Path Validation Requirement

- Respect router-validated source and target roots.
- Do not widen scope to unvalidated repositories.

# Main Workflow

1. Identify duplicate, versioned, legacy, and compatibility APIs.
2. Trace active call sites across HUD, Manager, config, event registration, and runtime entry points.
3. Classify each API as:
   - Active
   - Latest active
   - Compatibility-only
   - Deprecated
   - Unused
   - Demo-only
   - Needs verification
4. Verify whether older APIs are still required for compatibility or migration.
5. Report which APIs should be inherited, isolated, or omitted.

# Code-Tracing Order

```text
Public API names
    ->
Current call sites
    ->
HUD usage
    ->
Manager usage
    ->
Event registration
    ->
Config references
    ->
Feature flags
    ->
Compatibility and migration paths
```

# Reference-Loading Conditions

- Read `references/active-api-inventory-template.md` whenever an API inventory is required.
- Read `references/version-selection-checklist.md` when duplicate or versioned APIs exist.
- Read `references/deprecation-evidence-checklist.md` when deciding whether to omit legacy or deprecated logic.

# Combination Rules

- Combine with a source-to-shared module workflow skill when the source contains duplicate or versioned APIs.
- Combine with `review-feature-completeness` when omitted API versions may affect feature surface completeness.

# Allowed Files to Inspect

- Source Manager, HUD, Config, Utils, and event-registration files
- Inheritance reports and inventories

# Allowed Files to Modify

- Review output files only

# Required Evidence

- Repository-relative file paths
- API names
- Call-site evidence
- Runtime usage evidence
- Compatibility evidence, if retained

# Stop Conditions

- No duplicate, versioned, legacy, or superseded APIs are present
- Required call-site evidence cannot be located in validated repositories

# Report Format and Destination

- Use the shared finding format.
- Write results to `reports/reviews/[module-name]/active-api-review.md`.
