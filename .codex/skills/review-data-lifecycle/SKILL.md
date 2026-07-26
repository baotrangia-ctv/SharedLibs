---
name: review-data-lifecycle
description: Review load and save lifecycle behavior, readiness signaling, cache ownership, reconnect cases, shutdown paths, rollback safety, and known incident patterns for modules that touch persistent or per-player state.
---

# Purpose

Review lifecycle-sensitive behavior for modules that load, save, cache, initialize asynchronously, or handle reconnect and shutdown flows.

# Trigger Conditions

- The module loads or saves player data.
- The module maintains per-player runtime cache.
- The module registers database readiness.
- The module handles reconnect.
- The module handles player quit or server shutdown.
- The module grants persistent or one-time rewards.
- The module changes progression data.

# Required Inputs

- Target module files
- Relevant Manager, Config, HUD, and utility files
- Repository-relative evidence for persistence, cache, and lifecycle hooks

# Expected Outputs

- Lifecycle findings using the shared finding format
- Evidence-backed risks and validation requirements
- Clear statement when lifecycle review is not applicable

# Path Validation Requirement

- Respect router-validated source and target roots.
- Do not widen scope to unvalidated repositories.

# Main Workflow

1. Confirm the module triggers lifecycle review.
2. Trace the lifecycle in this order:
   - player join
   - database load
   - default-data creation
   - cache initialization
   - database-ready signal
   - feature initialization
   - runtime updates
   - save
   - disconnect
   - reconnect
   - player quit
   - server shutdown
3. Load only the references required by observed behavior.
4. Classify findings with severity, confidence, category, impact, and validation.
5. Write lifecycle review results to the appropriate report destination.

# Code-Tracing Order

```text
Player join
    ->
Database load
    ->
Default-data creation
    ->
Cache initialization
    ->
Database-ready signal
    ->
Feature initialization
    ->
Runtime updates
    ->
Save
    ->
Disconnect
    ->
Reconnect
    ->
Player quit
    ->
Server shutdown
```

# Reference-Loading Conditions

- Read `references/load-save-lifecycle.md` when the module reads or writes persistence, registers readiness, or saves on disconnect or shutdown.
- Read `references/cache-invariants.md` when the module maintains in-memory state, identifiers, ownership maps, or cache rebuild behavior.
- Read `references/reconnect-cases.md` when the module handles per-player runtime state, repeated initialization callbacks, or reconnect flows.
- Read `references/rollback-cases.md` when the module changes schemas, adapters, or rollout behavior that may require rollback.
- Read `references/known-incidents.md` when the observed flow resembles a previously unsafe pattern or touches async readiness ordering.

# Combination Rules

- Usually combine with a module workflow skill.
- May combine with `review-request-check-process` for modules that expose public actions.
- May combine with `review-production-readiness` when demo handlers are being replaced with real systems.

# Allowed Files to Inspect

- Manager files
- Config files
- Utility files
- Module documentation or portability artifacts
- Relevant HUD files only when they affect lifecycle timing

# Allowed Files to Modify

- Review output files only

# Required Evidence

- Repository-relative file paths
- Relevant function names or callbacks
- Lifecycle order evidence
- Readiness, cache, or save/load call sites

# Stop Conditions

- The module has no persistence, cache, readiness, reconnect, or shutdown behavior and the review is not applicable
- Required lifecycle evidence cannot be located in validated repositories

# Report Format and Destination

- Use the shared finding format.
- Write results to `reports/reviews/[module-name]/lifecycle-review.md` or `reports/bootstrap/validation-report.md` for bootstrap tasks.
