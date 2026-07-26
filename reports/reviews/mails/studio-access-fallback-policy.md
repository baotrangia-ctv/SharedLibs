# Mails Studio Access Fallback Policy Review

Date: 2026-07-26
Module: `mails`
Scope: SharedLibs inheritance rules and skills only

## Summary

The previous Mails inheritance attempt was blocked after project-path validation because the inheritance workflow treated Craftland Studio or MCP access as required for HUD/UI and CSV inspection. That gate was broader than the behavior actually required: repository-accessible Manager scripts, HUD scripts, config readers, CSV files, metadata, event registrations, public APIs, reports, and documentation can establish much of the feature safely.

This update makes inheritance filesystem-first and Studio-conditional. It does not re-inherit Mails and does not modify Steal A Pet.

## Evidence

| Finding | Evidence | Evidence Status |
| --- | --- | --- |
| The prior task was blocked after path validation because Studio access was required for HUD/UI and CSV inspection. | User-provided task history for this policy correction. | `Inferred` |
| The prior `mails-source-to-shared` stop conditions allowed a broad stop when the feature surface or active API could not be resolved. | `.codex/skills/mails-source-to-shared/SKILL.md` before this update. | `Verified from source files` |
| The prior router did not require filesystem-first inspection or define a Studio-unavailable fallback. | `.codex/skills/source-to-shared-router/SKILL.md` before this update. | `Verified from source files` |
| Repository rules already required a minimal runnable HUD but did not distinguish behavioral completeness from exact visual parity. | `.codex/rules/ui-completeness.md` before this update. | `Verified from source files` |
| Repository-accessible CSV and config readers were not explicitly exempted from Studio requirements. | `.codex/rules/config-preservation.md` before this update. | `Verified from source files` |

No independent execution log for the blocked inheritance was present in SharedLibs, so the exact runtime MCP failure is not claimed as `Verified from source files`.

## Policy Change

The updated workflow now:

1. Validates configured source and target paths.
2. Inspects all repository-accessible feature evidence.
3. Reads on-disk CSV files and parsing code directly.
4. Preserves verified Manager, config, CSV, persistence, event, API, and HUD-script behavior.
5. Uses a minimal generic HUD when exact source UI hierarchy cannot be inspected safely.
6. Records opaque editor bindings and visual details as `Needs Studio verification`.
7. Stops only when missing evidence prevents identification of the public Manager API, determination of the CSV schema or authoritative state changes, construction of a safe executable or testable primary flow, or avoidance of destructive or invalid target changes.

The fallback does not authorize direct editing or registration of opaque editor-owned assets.

## Mails Fallback Result

For the prompt `Inherit Mails system from Steal A Pet.` with Studio MCP unavailable, the expected routing is:

```text
source-to-shared-router
    ->
mails-source-to-shared
    ->
inspect filesystem evidence
    ->
review-feature-completeness
    ->
review-request-check-process
    ->
review-data-lifecycle
    ->
review-active-api-surface when versioned or legacy APIs are found
```

The task must continue through filesystem discovery and behavioral inheritance. Its generic HUD must support opening Mails, listing mail, selecting mail, claiming through the Manager request flow, refreshing claimed state, and displaying success or failure feedback.

Exact layout, styling, asset hierarchy, registration, and editor bindings remain `Needs Studio verification` unless verified through Studio MCP.

## Remaining Studio-Only Checklist

- Confirm opaque Mails UI asset hierarchy.
- Confirm editor-only control bindings.
- Confirm runtime asset registration when it cannot be proven from metadata.
- Compare layout and styling if exact visual parity is later required.
- Validate any editor-owned asset creation or attachment through Craftland Studio.

## Validation Boundary

This report validates policy and routing expectations only. It does not assert that the current SharedLibs repository contains an inherited Mails implementation, and it does not authorize re-inheritance during this task.
