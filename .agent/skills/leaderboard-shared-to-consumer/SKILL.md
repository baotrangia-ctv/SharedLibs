---
name: leaderboard-shared-to-consumer
description: Integrate the SharedLibs leaderboard into a consumer while preserving the two-type Income/Collection contract, query states, cache behavior, and the mock-provider replacement boundary.
---

# Leaderboard Shared to Consumer

Use this module skill with `.agent/skills/shared-to-consumer-router/SKILL.md`.
The original source project is out of scope; use the completed SharedLibs evidence
and the validated consumer project only.

## Inputs and scope

- Read configured roots from `.agent/project-paths.json`.
- Treat SharedLibs as workflow read-only and the validated consumer as read-write.
- Select the active SharedLibs leaderboard implementation from the existing
  Manager, Config, mock-provider, portability, and inheritance evidence.
- Preserve exactly the two supported score types: `Income` and `Collection`.
- Do not add `Wealth`, `Like`, `GlobalLeaderboard`, demo services, or simplified
  replacement assets.
- Use the source-to-shared evidence already collected in:
  - `reports/inheritance/leaderboard/feature-surface-inventory.md`
  - `reports/inheritance/leaderboard/inheritance-report.md`
  - `reports/reviews/leaderboard/`

## Complexity Gate evidence

This module is complex under the shared-to-consumer gate because its feature
surface contains at least four component types: Manager, HUD/UI script, Config,
Public API/contract, and an independent serialized UI asset. The current mock
stage has no persistence requirement, but a consumer that connects real score
persistence must also trigger the sensitive-state condition.

The router must propose and approve phases before consumer file changes unless the
user explicitly forces the work. Keep the following phase shape unless the actual
consumer evidence requires a documented adjustment:

1. Contract, definitions, and consumer config.
2. Manager/provider integration and public query contract.
3. HUD/UI asset import, attachments, navigation, and visual states.
4. Real score provider and persistence/lifecycle only when the consumer requires
   publishing or persistent scores.
5. Production readiness and runtime verification.

## Required contract

Preserve these SharedLibs contracts unless consumer evidence proves an explicit,
compatible adaptation:

- Supported types: `Income`, `Collection`.
- Income row: `[rank:int, playerUid:UUID|nil, score:int]`.
- Collection row: `[rank:int, playerUid:UUID|nil, score:int, petsCount:int, variants:string]`.
- Current-player summary: `[rank:int, score:int]`.
- UI states: loading, success, empty, and error.
- Preserve score ordering, tie behavior, row indices, current-player lookup,
  first-load cache behavior, reload invalidation, refresh behavior, and selected
  type handling.

Do not add writes to the read-only `RequestLeaderboard` contract. If the consumer
adds score publishing, introduce a separate Request → Check → Process flow and run
the Request-Check-Process and Data Lifecycle sections of `review-inherited-module`.

## Consumer workflow

1. Validate distinct SharedLibs and consumer roots, repository markers, and access
   modes before modification.
2. Load `.agent/references/inheritance/repository-first.md`,
   `serialized-assets.md`, `dependency-closure.md`, `mcp-last.md`,
   `runtime-verification.md`, `preserve-first-bindings.md`,
   `repository-definition-search.md`, `stage-based-completion.md`,
   `standalone-portability.md`, and `explicit-mcp-blockers.md` as their conditions
   apply.
3. Inspect the SharedLibs Manager, definitions, mock provider, portability status,
   and the reports listed above. Do not inspect the original Steal A Pet project.
4. Build the smallest complete consumer dependency closure and search consumer
   definitions before adapting paths, IDs, utilities, or bindings.
5. Preserve the Manager query/cache flow and the two-type contract.
6. Replace `LeaderboardMockScoreProvider` only at the provider boundary when the
   consumer has a real score source. Do not spread consumer-specific score access
   through HUD or Manager query code.
7. Integrate files by responsibility: Manager, Config/definitions, HUD scripts,
   serialized UI, textures, and consumer runtime attachment layers.
8. Preserve serialized hierarchy, IDs, bindings, metadata, and engine-library URI
   references. Remove only the out-of-scope `WealthButton`, `LikeButton`, and
   inactive `TabsRegion` after faithful UI import and evidence review.
9. Reuse the consumer equivalent of `ShadowSquareRounded.png` when the matching
   target file ID is valid. Replace source-wide `CustomUIUtils.fcg` only with a
   justified leaderboard-specific consumer control.
10. Complete safe filesystem stages independently, then run the required reviews
    and consumer runtime verification.

## Review routing

Always run these `review-inherited-module` sections:

- Clone Fidelity
- Standalone Portability
- Feature Completeness
- Folder Architecture

Run these when applicable:

- Serialized Asset Fidelity — `Assets/HUDs/Leaderboard.ui` or related UI assets.
- Asset Dependency Closure — leaderboard textures, HUD scripts, IDs, utilities,
  and engine-library references.
- Active API Surface — duplicate leaderboard APIs or additional score types.
- Static Definitions — type IDs, UI states, row indices, or public result values.
- Request-Check-Process — only if the consumer introduces public mutations.
- Data Lifecycle — only if real persistence, reconnect, cache ownership, or
  shutdown behavior is introduced.
- Production Readiness — only for release-facing real score integration.

## Known evidence and stage boundaries

- Manager/config/mock subset is source-compatible and locally compiled.
- Serialized leaderboard HUD clone is currently incomplete and must not be replaced
  by an invented simplified HUD.
- Required source-local textures and the HUD import are a separate asset stage.
- `ShadowSquareRounded.png` has a matching target file ID and may be reused when
  the consumer repository confirms it.
- The engine profile placeholder URI remains engine-owned and requires runtime
  verification.
- Runtime verification has not been performed; do not claim build, rendering,
  attachment, event, persistence, or runtime success without live evidence.
- A wrong or unavailable Studio context blocks only the serialized asset/registration
  stage when other safe consumer stages can continue. Record the exact target asset
  identifier, searched paths, affected stage, and safe work completed.

## Evidence requirements

Record repository-relative paths, active contract decisions, copied/adapted/omitted
files, type and row schemas, state transitions, cache/refresh behavior, provider
boundary, serialized ID and binding handling, dependency closure, definitions,
utility and texture decisions, review sections, phase statuses, exact MCP blockers,
runtime status, rollback notes, and remaining consumer work.

## Reports

Write consumer integration evidence under
`reports/consumer-integrations/[consumer-project]/leaderboard/`, using the shared
consumer integration report template. Keep filesystem integration, portability,
clone fidelity, and runtime verification as separate statuses.

## Stop conditions

Stop before modification for invalid roots, identical roots, incorrect access modes,
or a missing authoritative SharedLibs contract. Block only the affected stage for a
missing optional dependency, pending runtime verification, or unavailable Studio;
use the exact six-condition MCP blocker evidence before blocking the whole task.
