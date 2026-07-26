# Mails Architecture Cleanup Gap Review

Date: 2026-07-26
Module: `mails`
Scope: Current SharedLibs filesystem, inheritance framework, and Mails workflow artifacts

## Summary

The current repository does not contain an inherited Mails Manager, Config, HUD, UI asset, model, status, constants, utility, adapter, or demo source file. Therefore, this review cannot confirm that current Mails code mixes layers, duplicates `DataUtils`, declares excessive inline constants, or contains unjustified adapters.

The filesystem does contain empty Mails-oriented directories, including the forbidden mixed-layer target `Assets/Scripts/Mails/` and the demo-first remnant `modules/mails/demo/`. The inheritance framework also contained requirements and wording that could encourage demo artifacts and did not previously enforce layer mapping, utility reuse, static-definition ownership, or Adapter-Last.

This report validates the framework correction. It does not claim the Mails implementation architecture is fixed.

## Repository Evidence

| Finding | Repository Evidence | Evidence Status |
| --- | --- | --- |
| No Mails implementation files exist under `Assets/`. | `rg --files Assets` returned no Mails file; `Assets/Scripts/Mails/` is empty. | `Verified from source files` |
| No Mails implementation files appear in available Git history. | `git log --all --name-status -- Assets` contains no Mails source path. | `Verified from source files` |
| An empty mixed-layer Mails folder exists locally. | `Assets/Scripts/Mails/` exists and has no children. | `Verified from source files` |
| An empty demo-first folder exists locally. | `modules/mails/demo/` exists and has no children. | `Verified from source files` |
| Mails reports and workflow skills exist. | `.codex/skills/mails-source-to-shared/`, `.codex/skills/mails-shared-to-consumer/`, and `reports/reviews/mails/`. | `Verified from source files` |
| The reported Mails code previously mixed layers, duplicated utilities, overused constants, or generated demo scripts. | No current or historical Mails implementation file is available to inspect. | `Inferred` |

Empty directories are not tracked by Git, so their existence is local filesystem evidence rather than a committed source artifact.

## Architecture Findings

### Mixed Feature Folder

- Severity: High for future generation
- Current evidence: `Assets/Scripts/Mails/` exists but is empty.
- Finding: The path represents the forbidden mixed-layer architecture even though no files currently occupy it.
- Future action: Do not place generated files under this directory. Remove the empty directory during the implementation cleanup.

Required future placement:

| Responsibility | Future Target |
| --- | --- |
| Authoritative Mails behavior | `Assets/Scripts/Managers/MailsManager.fcg` |
| Mails HUD behavior | `Assets/Scripts/HUDs/MailsHUD.fcg` |
| Mails config reader | `Assets/Scripts/Configs/MailsConfigs.fcg` |
| Reused fields, states, results, and actions | `Assets/Scripts/Configs/MailsDefinitions.fcg` initially |
| Mails UI asset | `Assets/HUDs/` with the exact editor-owned filename verified before registration |
| Broadly reusable conversion helpers | Existing `Assets/Scripts/Utils/DataUtils.fcg`, extended only when justified |

Use layer-local Mails subfolders only if one layer grows large enough to justify them. Never recreate `Assets/Scripts/Mails/` as a cross-layer container.

### Demo Artifacts

- Severity: Medium
- Confirmed current source files: none
- Confirmed structural remnant: empty `modules/mails/demo/`
- Future action: Remove the empty directory and do not create standalone Mails demo persistence, rewards, player, notifications, time, analytics, feature flags, or provider scripts by default.
- Allowed exception: Create one small validation-only implementation only when the primary flow cannot execute safely, no existing SharedLibs service is compatible, and no optional, no-op, callback, or documentation alternative works.

No current demo source file can be recommended for removal because none exists.

## Utility Reuse Findings

`Assets/Scripts/Utils/DataUtils.fcg` is the mandatory first reuse target. Confirmed candidate APIs include:

| DataUtils API | Path Reference | Candidate Use |
| --- | --- | --- |
| `ListIntToString` | `Assets/Scripts/Utils/DataUtils.fcg:11` | Integer-list serialization |
| `StringToListInt` | `Assets/Scripts/Utils/DataUtils.fcg:23` | Integer-list deserialization |
| `ListListIntToString` | `Assets/Scripts/Utils/DataUtils.fcg:44` | Nested integer-list serialization |
| `StringToListListInt` | `Assets/Scripts/Utils/DataUtils.fcg:56` | Nested integer-list deserialization |
| `ListIntToStringUseComma` | `Assets/Scripts/Utils/DataUtils.fcg:105` | Delimiter-based integer-list serialization |
| `StringToListIntV2` | `Assets/Scripts/Utils/DataUtils.fcg:124` | Delimiter-based integer-list parsing |
| `JsonStringToKeyValue` | `Assets/Scripts/Utils/DataUtils.fcg:178` | Key/value parsing |
| `JsonStringToListKeyValue` | `Assets/Scripts/Utils/DataUtils.fcg:198` | List-of-map parsing |
| `ListKeyValueToJsonString` | `Assets/Scripts/Utils/DataUtils.fcg:225` | List-of-map serialization |
| `JsonStringToListKeyValueV2` | `Assets/Scripts/Utils/DataUtils.fcg:258` | Alternate list-of-map parsing |

No Mails parsing or serialization code exists to compare against these APIs. A future cleanup must compare delimiters, nil and empty handling, failure behavior, collection mutation, ordering, and persistence compatibility before selecting an API.

Exact future decisions:

- Remove any generic `MailsDataUtils` or Manager-local serializer that duplicates compatible `DataUtils` behavior.
- Keep mail-expiration, claim eligibility, or reward-shape logic feature-local because it expresses Mails business rules.
- Add a compatibility wrapper only if persisted legacy Mails encoding differs from the canonical SharedLibs format.
- Extend `DataUtils` only for behavior that is broadly reusable outside Mails.

## Static Definition Findings

No Mails Manager or definition file exists, so excessive `FIELD_*`, `STATUS_*`, action, result, or state declarations cannot be confirmed.

Future consolidation:

1. Keep constants used in one function local.
2. Keep implementation-only constants used by one Manager private in `MailsManager.fcg`.
3. Place CSV columns, serialized field names, config identifiers, and defaults in Mails Config or Definitions.
4. Place fields, states, claim result codes, and action identifiers shared by Manager and HUD in one cohesive `MailsDefinitions.fcg`.
5. Split `MailsDefinitions.fcg` only when file size or ownership creates a clear maintenance boundary.
6. Do not create one file per constant or place Mails-specific definitions in Utils.

## Adapter Findings

No current Mails adapter source file exists, so adapter justification cannot be reviewed.

Apply Adapter-Last during future implementation:

- Use direct reusable behavior when the contract is stable.
- Use an optional callback or simple interface when only reward delivery, notification, or persistence behavior varies.
- Retain an adapter only for a real external contract, incompatible representation, platform boundary, or multiple integration implementations.
- Remove pass-through adapters with no translation, validation, lifecycle ownership, or compatibility value.

## Demo Rule and Reference Decisions

| File or Area | Old Purpose | Decision | Replacement Behavior |
| --- | --- | --- | --- |
| `.codex/skills/mails-source-to-shared/references/demo-requirements.md` | Required a runnable Mails demo flow. | Remove and replace. | `primary-flow-validation.md` validates the flow without requiring demo service classes. |
| `.codex/skills/mails-shared-to-consumer/references/demo-replacement.md` | Drove replacement of generated demo handlers. | Remove and replace. | `production-placeholder-cleanup.md` omits or cleans existing placeholders without assuming they should exist. |
| `.codex/skills/source-to-shared-router/references/module-source-to-shared-template.md` | Required demo CSV and did not enforce minimal output. | Simplify. | Require minimal example config only when needed, minimal file-set design, Demo-Last, utility reuse, and new reviews. |
| `.codex/skills/review-feature-completeness/` | Treated demo flow as a completeness layer. | Simplify. | Require executable or testable primary flow and report `Unnecessary Demo Artifacts`. |
| `.codex/rules/manager-organization.md` | Reserved a Manager section for demo-only integrations. | Simplify. | Use `Optional Integrations`; do not generate demo handlers by default. |
| `.codex/rules/config-preservation.md` | Required minimal demo CSV data. | Simplify. | Use minimal example CSV data only when config rows are required for validation. |
| `.codex/skills/review-production-readiness/references/demo-replacement-checklist.md` | Checked replacement of existing demos and mocks. | Retain with narrower guidance. | Use only to clean existing placeholders; never use it to require demo generation. |

No demo-specific standalone skill was found, so no skill was deleted.

## Exact Future Cleanup

When a Mails implementation is available:

1. Remove the empty `Assets/Scripts/Mails/` and `modules/mails/demo/` structural remnants.
2. Move or create each source file in its responsibility-owned layer.
3. Produce a complete file inventory before moving anything.
4. Compare all Mails parsing and serialization with the current `DataUtils`.
5. Consolidate reused public definitions into one initial `MailsDefinitions.fcg`.
6. Keep private implementation constants in the Manager.
7. Remove unused demo providers and pass-through adapters.
8. Run:
   - `review-folder-architecture`
   - `review-utility-reuse`
   - `review-static-definitions`
   - `review-feature-completeness`
   - `review-request-check-process`
   - `review-data-lifecycle`
   - `review-active-api-surface` when legacy or versioned APIs exist
9. Compile all changed FC files and validate editor-owned assets through the required Craftland workflow.

## Remaining Unknowns

- Actual Mails source file names and responsibilities
- Whether any Mails serializer duplicates `DataUtils`
- Persisted Mails encoding and compatibility requirements
- Actual `FIELD_*`, `STATUS_*`, action, result, and state declarations
- Whether Manager, Config, HUD, and Utils were previously mixed in files that are no longer present
- Whether any generated adapter or demo file was used by the primary flow
- Exact UI asset filename and editor bindings

These questions require an actual Mails implementation artifact or a future inheritance task. They do not justify claiming the current Mails architecture is fixed.
