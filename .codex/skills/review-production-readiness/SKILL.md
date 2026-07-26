---
name: review-production-readiness
description: Review whether a module or consumer integration is release-ready, with real persistence and rewards where required, placeholder behavior removed, adapters justified, and rollback behavior documented.
---

# Purpose

Review whether a feature is ready for production use and free of active placeholder behavior.

# Trigger Conditions

- Demo persistence is replaced
- Demo reward handlers are replaced
- Real rewards or currency are granted
- Real database schemas are connected or changed
- Consumer business logic is introduced
- The feature is intended for release

# Required Inputs

- Target module or consumer integration files
- Portability manifest
- Integration documentation
- Relevant config and adapter files

# Expected Outputs

- Production-readiness findings using the shared finding format
- Explicit list of remaining demo-only behavior, required adapters, rollback notes, and release blockers

# Path Validation Requirement

- Respect router-validated source and target roots.
- Do not widen scope to unvalidated repositories.

# Main Workflow

1. Confirm the task has moved beyond demo-only behavior.
2. Identify remaining mocks, demo handlers, and placeholder integrations.
3. Verify real system connections and justify each retained adapter under Adapter-Last.
4. Review config completeness, persistence integration, failure handling, logging, and rollback instructions.
5. Confirm known limitations are documented.
6. Write findings and required validation steps.

# Code-Tracing Order

```text
Shared module contracts
    ->
Consumer or target adapters
    ->
Real persistence and reward integration
    ->
Failure handling
    ->
Observability and logs
    ->
Rollback and release notes
```

# Reference-Loading Conditions

- Read `references/demo-replacement-checklist.md` when demo handlers, mock persistence, or placeholder rewards are being replaced.
- Read `references/release-readiness.md` when the integration is intended for release or user-facing rollout.
- Read `references/rollback-readiness.md` when the integration changes persistence, adapters, or observable behavior that may require rollback.

# Combination Rules

- Usually combine with a module workflow skill when replacing demos with real systems.
- Combine with `review-request-check-process` when production integrations affect public actions.
- Combine with `review-data-lifecycle` when production integrations affect persistence or cache behavior.

# Allowed Files to Inspect

- Manager files
- Config files
- Adapter files
- Portability manifests
- Consumer integration files
- Documentation relevant to release behavior

# Allowed Files to Modify

- Review output files only

# Required Evidence

- Repository-relative file paths
- Remaining demo-only components
- Real adapter and persistence call sites
- Rollback or release documentation evidence

# Stop Conditions

- The task is still purely demo-only and no production replacement is being attempted
- Required production integration evidence cannot be located in validated repositories

# Report Format and Destination

- Use the shared finding format.
- Write results to `reports/reviews/[module-name]/production-readiness-review.md` or `reports/consumer-integrations/[consumer-project]/[module-name]/validation-report.md`.
