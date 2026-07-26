# Mails First Inheritance Gap Review

Date: 2026-07-26
Module: `mails`
Review scope: SharedLibs reusable inheritance system and current SharedLibs Mails output

## Summary

The current SharedLibs Mails inheritance is incomplete. The repository contains bootstrap-era Mails workflow skill folders, but no completed Mails runtime, HUD, config, or CSV feature output under `Assets/`. The first inheritance also appears to have skipped required feature-surface discovery, config inheritance, HUD inheritance, Manager organization enforcement, and active API review.

This report records the gaps and the corrective expectations for a future dedicated Mails correction task. It does not claim the Mails implementation is fixed.

## Current SharedLibs Evidence

### Mails workflow skills

- `.codex/skills/mails-source-to-shared/` existed previously but had no `SKILL.md`
- `.codex/skills/mails-shared-to-consumer/` existed previously but had no `SKILL.md`

### Current SharedLibs feature files

Observed feature files under SharedLibs currently include `Collection` artifacts and shared utilities, but no Mails runtime or HUD files were found under:

- `Assets/Scripts/Managers/`
- `Assets/Scripts/HUDs/`
- `Assets/Scripts/Configs/`
- `Assets/Scripts/Utils/`
- `Assets/HUDs/`

Relevant repository checks found:

- `Assets/Scripts/Managers/CollectionManager.fcg`
- `Assets/Scripts/HUDs/Collection/HudCollection.fcg`
- `Assets/HUDs/Collection.ui`
- no Mails counterparts in these target directories

## Gap Findings

### 1. Missing Config

- Severity: High
- Confidence: Confirmed
- Category: Config
- Evidence: No Mails config reader or Mails config files were found under `Assets/Scripts/Configs/`.
- Affected repository-relative paths:
  - `Assets/Scripts/Configs/`
- Affected flow: Config loading
- Expected behavior: A reusable Mails inheritance should preserve the active config-reading mechanism and provide minimal demo config data when the source module is config-driven.
- Actual or possible behavior: The current SharedLibs output has no visible Mails config layer.
- Impact: Future Mails runtime cannot preserve reusable CSV-driven behavior.
- Recommended fix: Re-inherit Mails with explicit config-reader and minimal example CSV inheritance.
- Required validation: Verify source Mails config reader, CSV schema, parsing logic, and runtime consumers.

### 2. Missing CSV Reader

- Severity: High
- Confidence: Confirmed
- Category: Missing CSV Reader
- Evidence: No Mails CSV reader or example CSV file was found in `Assets/Scripts/Configs/` or `Assets/CSV/`.
- Affected repository-relative paths:
  - `Assets/Scripts/Configs/`
  - `Assets/CSV/`
- Affected flow: Config-driven runtime behavior
- Expected behavior: Preserve reusable CSV loading and include only the minimal example rows required for validation.
- Actual or possible behavior: The current output has no Mails CSV loading path.
- Impact: Any inherited Mails demo would be forced toward hardcoded data or remain incomplete.
- Recommended fix: Re-inherit active Mails config and CSV flow using the updated rules.
- Required validation: Trace source CSV files, schema, parsing, defaults, and lookup methods.

### 3. Missing HUD

- Severity: High
- Confidence: Confirmed
- Category: Missing HUD
- Evidence: No Mails HUD script was found under `Assets/Scripts/HUDs/`.
- Affected repository-relative paths:
  - `Assets/Scripts/HUDs/`
- Affected flow: User-facing mail interaction
- Expected behavior: A generic Mails inheritance should include a runnable minimal HUD when the source feature has UI.
- Actual or possible behavior: The current SharedLibs output has no visible Mails HUD flow.
- Impact: The feature cannot demonstrate opening, viewing, claiming, and refreshing mail state.
- Recommended fix: Re-inherit Mails HUD and UI flow with a minimal runnable generic HUD.
- Required validation: Trace source HUD scripts, UI-triggered actions, and Manager query/event dependencies.

### 4. Missing UI Asset

- Severity: High
- Confidence: Confirmed
- Category: Missing UI Asset
- Evidence: No Mails UI asset was found under `Assets/HUDs/`.
- Affected repository-relative paths:
  - `Assets/HUDs/`
- Affected flow: Primary UI and user interaction
- Expected behavior: The generic module should include a runnable minimal Mails UI asset if the source feature has required UI.
- Actual or possible behavior: No Mails UI assets are present.
- Impact: The Mails primary flow cannot demonstrate the required user interaction.
- Recommended fix: Re-inherit minimal generic UI assets for Mails.
- Required validation: Trace source UI assets and classify required versus optional UI elements.

### 5. Missing Load Flow

- Severity: High
- Confidence: Likely
- Category: Missing Load Flow
- Evidence: No SharedLibs Mails Manager file was found under `Assets/Scripts/Managers/`, so no `Load Data` section can be verified.
- Affected repository-relative paths:
  - `Assets/Scripts/Managers/`
- Affected flow: Load Data
- Expected behavior: Persistent Managers should clearly separate `Load Data`.
- Actual or possible behavior: Current SharedLibs output does not show a Mails load section.
- Impact: Persistence behavior and readiness flow are unverified or absent.
- Recommended fix: Re-inherit Mails Manager with explicit section organization.
- Required validation: Trace source Mails load path, default data creation, deserialization, cache initialization, and ready signaling.

### 6. Missing Save Flow

- Severity: High
- Confidence: Likely
- Category: Missing Save Flow
- Evidence: No SharedLibs Mails Manager file was found under `Assets/Scripts/Managers/`, so no `Save Data` section can be verified.
- Affected repository-relative paths:
  - `Assets/Scripts/Managers/`
- Affected flow: Save Data
- Expected behavior: Persistent Managers should clearly separate `Save Data`.
- Actual or possible behavior: Current SharedLibs output does not show a Mails save section.
- Impact: Persistence and rollback behavior remain unverified.
- Recommended fix: Re-inherit Mails Manager with explicit save organization and persistence documentation.
- Required validation: Trace source serialization, save calls, disconnect save behavior, and shutdown handling.

### 7. Missing Action Flow

- Severity: High
- Confidence: Likely
- Category: Missing Action Flow
- Evidence: No SharedLibs Mails Manager file was found under `Assets/Scripts/Managers/`, so no `Actions` section can be verified.
- Affected repository-relative paths:
  - `Assets/Scripts/Managers/`
- Affected flow: User actions
- Expected behavior: Authoritative Mails actions should follow `Request -> Check -> Process`.
- Actual or possible behavior: Current SharedLibs output does not expose a verifiable Mails action flow.
- Impact: Claim and state-change flows cannot be validated.
- Recommended fix: Re-inherit Mails Manager with explicit action sections and review by `review-request-check-process`.
- Required validation: Trace source claim and selection flows end to end.

### 8. Deprecated Logic Included or Unfiltered

- Severity: Medium
- Confidence: Needs verification
- Category: Deprecated Logic Included
- Evidence: The source Mails system was reported to include deprecated logic and old API versions, but the current SharedLibs output lacks an active API inventory and does not document omitted legacy APIs.
- Affected repository-relative paths:
  - `reports/inheritance/mails/`
  - `reports/reviews/mails/`
- Affected flow: API inheritance scope
- Expected behavior: Active API inventory should document latest active, compatibility-only, and omitted deprecated APIs.
- Actual or possible behavior: No active API review artifact is currently present.
- Impact: Future inheritance may copy obsolete flows again.
- Recommended fix: Require `review-active-api-surface` and an API inventory in the correction task.
- Required validation: Trace versioned Mails APIs and current call sites in Steal A Pet.

## Recommended Mails Correction Task

The next dedicated Mails correction task should:

1. Build a complete feature-surface inventory
2. Trace active config and CSV loading
3. Trace active HUD and UI flow
4. Trace `Load Data`
5. Trace `Save Data`
6. Trace `Actions`
7. Produce an active API inventory
8. Re-inherit only the latest active Mails flows
9. Add a minimal runnable Mails HUD and UI asset
10. Add a config reader and minimal example CSV
11. Run:
   - `review-feature-completeness`
   - `review-request-check-process`
   - `review-data-lifecycle`
   - `review-active-api-surface`

## Notes

- No Steal A Pet files were modified during this review.
- This report records gaps in the current SharedLibs state and the inheritance system improvements needed for the next correction pass.
