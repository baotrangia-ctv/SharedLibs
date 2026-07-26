---
name: review-request-check-process
description: Review public module actions to ensure they follow Request to Check to Process, keep validation read-only, keep mutation Manager-owned, and prevent duplicate or partial processing.
---

# Purpose

Validate that user-facing and public Manager actions follow:

```text
Request
    ->
Check
    ->
Process
```

# Trigger Conditions

- The module exposes user actions.
- The module exposes public Manager operations.
- The module grants rewards, modifies state, or writes persistence through public APIs.

# Required Inputs

- Target module Manager files
- Related HUD files
- Relevant cross-Manager call sites

# Expected Outputs

- Action-flow findings using the shared finding format
- Evidence-backed confirmation of compliant flows where applicable

# Path Validation Requirement

- Respect router-validated source and target roots.
- Do not widen scope to unvalidated repositories.

# Main Workflow

1. Identify each public action or user-triggered operation.
2. Trace the flow from HUD or external caller to Manager `Request`.
3. Verify `Request` calls `Check`.
4. Verify `Check` is read-only.
5. Verify `Process` owns authoritative mutation and persistence.
6. Verify failure does not partially mutate state.
7. Verify one-time actions are idempotent or protected against duplicate execution.
8. Write findings and required validation steps.

# Code-Tracing Order

```text
User-facing entry point
    ->
HUD event or external API
    ->
Manager Request
    ->
Manager Check
    ->
Manager Process
    ->
Cross-Manager dependencies
    ->
State mutation
    ->
Persistence write
    ->
Success or failure result
```

# Reference-Loading Conditions

- Read `references/action-flow-checklist.md` when the module exposes user actions or public Manager methods.
- Read `references/idempotency-cases.md` when the module grants one-time rewards, applies purchases, changes progression, or can receive duplicate calls.

# Combination Rules

- Usually combine with a module workflow skill.
- Combine with `review-data-lifecycle` when public actions also touch persistence, readiness, cache, reconnect, or one-time rewards.
- Combine with `review-production-readiness` when replacing demo handlers with real systems.

# Allowed Files to Inspect

- Manager files
- HUD files
- Relevant config files when they affect action gating
- Cross-Manager public API calls

# Allowed Files to Modify

- Review output files only

# Required Evidence

- Repository-relative file paths
- Public action entry points
- Request, Check, and Process call sites
- Mutation and persistence call sites

# Stop Conditions

- No public actions or user-triggered Manager operations exist
- Required flow evidence cannot be located in validated repositories

# Report Format and Destination

- Use the shared finding format.
- Write results to `reports/reviews/[module-name]/request-check-process-review.md` or `reports/bootstrap/validation-report.md` for bootstrap tasks.
