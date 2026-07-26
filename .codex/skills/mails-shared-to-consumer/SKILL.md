---
name: mails-shared-to-consumer
description: Integrate the active SharedLibs Mails package through preserve-first repository inspection, safe stage completion, consumer portability assessment, and exact MCP-last blockers.
---

# Purpose

Apply the common shared-to-consumer framework without reading the original source
project.

# Required Inputs

- router-validated SharedLibs and consumer roots, with SharedLibs treated as
  workflow read-only and the consumer read-write
- portability manifest, public contracts, and consumer package when available

# Workflow

1. Inspect SharedLibs repository artifacts and select the latest active contracts.
2. Inventory serialized assets, config, definitions, localization, scripts, and
   references.
3. Search SharedLibs and consumer definitions for custom IDs, components, enums,
   scripts, utilities, textures, and target equivalents.
4. Build the smallest complete dependency closure.
5. Preserve compatible serialized values and transfer assets and contracts
   faithfully.
6. Map persistence, rewards, notifications, UI entry points, and business rules to
   consumer integration points.
7. Reuse compatible consumer utilities and definitions; adapt only proven
   incompatibilities.
8. Preserve Request -> Check -> Process and data lifecycle.
9. Complete every safe independent stage.
10. Assess consumer portability separately from transfer fidelity.
11. Apply Adapter-Last; omit deprecated, compatibility-only, demo, mock, and
   placeholder artifacts unless evidence requires them.
12. Run serialized-asset, dependency, portability, architecture, action, lifecycle,
   and production
   reviews as applicable.
13. Use MCP only for exact unresolved blockers.
14. Generate stage-based integration and rollback reports.

# Common References

Load applicable files under `.codex/references/inheritance/`:

- `repository-first.md`
- `serialized-assets.md`
- `dependency-closure.md`
- `mcp-last.md`
- `runtime-verification.md`
- `preserve-first-bindings.md`
- `repository-definition-search.md`
- `stage-based-completion.md`
- `standalone-portability.md`
- `explicit-mcp-blockers.md`

Load module references progressively for contract mapping, business adaptation,
placeholder cleanup, validation, and rollback.

# Reviews

- Use `review-serialized-asset-fidelity` for serialized assets.
- Use `review-asset-dependency-closure` for referenced files or assets.
- Use `review-standalone-portability`.
- Use `review-folder-architecture` when files change.
- Use `review-utility-reuse`, `review-static-definitions`,
  `review-request-check-process`, `review-data-lifecycle`, and
  `review-production-readiness` only when their triggers apply.

# Constraints

- Never require or inspect the original source project.
- Preserve available shared assets; do not recreate simplified versions.
- Preserve compatible custom values before remapping and resolve local files without
  MCP.
- Adapt only consumer integration points and retain active shared APIs.
- Modify only the validated consumer target when implementation is requested.
- Pending live runtime verification does not block filesystem integration.

# Required Evidence and Reports

Record active contracts, assets and ID handling, dependency closure,
definition searches, preserve/remap decisions, copied/adapted/omitted files, stage
statuses, integration mappings, utility and texture handling, consumer portability,
exact MCP blockers, runtime status, validation, and rollback.

Write results under `reports/consumer-integrations/[consumer-project]/mails/`.
