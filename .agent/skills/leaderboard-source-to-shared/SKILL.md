---
name: leaderboard-source-to-shared
description: Inherit the active Steal A Pet leaderboard system into SharedLibs through faithful-clone-first discovery, preserving exactly the two source leaderboard types, UI/data flow, states, and dependencies before introducing a mockable score-provider seam.
---

# Leaderboard Source to Shared

## Inputs and scope

- Read configured roots from `.agent/project-paths.json`.
- Treat `steal_a_pet` as read-only and `shared_libs` as read-write.
- Support only leaderboard types proven active by source call sites.
- Do not add leaderboard types, demo services, or simplified replacement assets.

## Required workflow

1. Load the common inheritance references required by `source-to-shared-router`.
2. Validate distinct source and target roots, access modes, and repository markers.
3. Inventory active Manager, HUD, UI assets, config, models, events, data flow,
   navigation, loading/empty/error states, persistence, utilities, and dependencies.
4. Trace duplicate or versioned implementations and select only the latest active API.
5. Build the smallest complete transitive dependency closure and search both
   repositories for reusable definitions and services.
6. Create a Stage A faithful clone before Stage B genericization.
7. Preserve readable serialized assets and bindings byte-faithfully when available.
8. In Stage B, replace the score source only with a small provider seam whose default
   implementation returns deterministic mock rows matching the source data contract.
9. Keep UI behavior, sorting, refresh, state handling, and navigation source-faithful.
10. Organize target files by architectural responsibility and reuse SharedLibs utilities.
11. Run required reviews and FC validation, keeping clone fidelity, standalone
    portability, serialized clone, and runtime verification statuses separate.

## Required reviews

- `review-inherited-module` sections Clone Fidelity, Standalone Portability,
  Feature Completeness, and Folder Architecture
- Serialized Asset Fidelity when readable serialized assets exist
- Asset Dependency Closure when artifacts reference dependencies
- Active API Surface when duplicate or versioned APIs exist
- Utility Reuse when structured data is parsed or serialized
- Static Definitions for repeated types, fields, states, or action identifiers
- Request-Check-Process for public Manager actions
- Data Lifecycle for cache, readiness, persistence, reconnect, or shutdown flow

## Leaderboard-specific evidence

Record:

- the exact two active leaderboard type identifiers and every call site;
- row, request, response, state, and error structures;
- score ordering and tie behavior;
- refresh timing and loading, empty, success, and error transitions;
- HUD hierarchy, bindings, navigation entry/exit, and selected-type behavior;
- original score-system dependencies and the mock-provider replacement boundary;
- source-specific dependencies kept, isolated, adapted, or deferred.

## Asset and FC boundary

- Inspect readable serialized repository evidence before MCP.
- Use Craftland Studio for semantic asset edits, registration, attachments, or live
  bindings; read `instructions://index` first.
- Edit only user-owned `.fcg` and `.fcc` text directly.
- Validate all FC edits with full `fccompile.exe -i Assets`.

## Reports

Write the inheritance report to `reports/inheritance/leaderboard/` and review reports
to `reports/reviews/leaderboard/`.

## Stop conditions

Stop only for invalid configured roots, identical source and target roots, incorrect
access modes, missing authoritative source artifacts for the affected required stage,
or an exact MCP blocker satisfying all common blocker conditions. Continue all safe
independent stages and report runtime-only verification separately.
