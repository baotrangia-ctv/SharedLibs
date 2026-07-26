---
name: review-folder-architecture
description: Review source-to-shared and shared-to-consumer file placement by architectural responsibility, detect mixed feature folders, and recommend exact move, split, remove, or documented layer-subfolder decisions.
---

# Purpose

Verify that generated or integrated files follow the repository's layer-based architecture instead of collecting unrelated responsibilities in one feature folder.

# Required Inputs

- Target module file inventory
- Target repository structure and naming conventions
- Inheritance or consumer integration report draft

# Expected Outputs

- Placement findings for every misplaced or ambiguous file
- Exact target folder and move, split, remove, or retain decision
- Documented exceptions for allowed feature subfolders

# Main Workflow

1. Inventory all module source, asset, report, and skill-reference files.
2. Assign one current responsibility to each file.
3. Map each responsibility using `references/folder-mapping.md`.
4. Detect mixed feature folders, misplaced reports, unclear filenames, and layer-crossing files.
5. Verify any feature subfolder exception is layer-local, consistent with repository conventions, justified, and large enough to need grouping.
6. Recommend `Move`, `Split`, `Remove`, or `Retain with documented exception`.
7. Write findings before module completion.

# Reference-Loading Conditions

- Read `references/folder-mapping.md` for every review.

# Combination Rules

- Combine with every source-to-shared workflow.
- Combine with shared-to-consumer workflows that create, copy, move, or adapt files.
- Combine with `review-feature-completeness` when missing layers may be mistaken for placement errors.

# Allowed Files to Inspect

- Target `Assets/` source and asset files
- Target reports and portability artifacts
- Relevant `.codex/skills/**/references/`
- Repository naming and folder conventions

# Allowed Files to Modify

- Review output files only

# Commands

- Use `rg --files` to inventory tracked and visible files.
- Use `Get-ChildItem -Force` when empty or ignored directories may affect the review.
- Use `rg -n` to identify a file's architectural responsibility when the filename is ambiguous.

# Safety Constraints

- Do not move files during a review-only task.
- Do not recommend a folder solely because the source project used it.
- Do not inspect or modify unvalidated repositories.
- Do not require a feature subfolder when flat layer placement is sufficient.

# Required Evidence

- Repository-relative file path
- Current responsibility
- Current folder
- Required target folder
- Decision: move, split, remove, or retain
- Exception justification, when applicable

# Stop Conditions

- Target repository path is not validated
- File responsibility cannot be determined from source or call-site evidence
- A proposed move has concrete evidence that it would invalidate editor registration
  and cannot be preserved or path-adjusted safely

Defer only that move finding and continue reviewing independent files. Use exact
blocker evidence rather than a broad `editor-owned dependency` label.

# Report Format and Destination

For each finding, report:

| Misplaced File | Current Responsibility | Correct Target Folder | Decision | Evidence |
| --- | --- | --- | --- | --- |

Write results to `reports/reviews/[module-name]/folder-architecture-review.md` or the relevant consumer integration report directory.
