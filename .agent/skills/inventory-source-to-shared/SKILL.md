---
name: inventory-source-to-shared
description: Inherit Steal A Pet Storage core logic into the SharedLibs Inventory module without using or conflating Steal A Pet's separate InventoryManager.
---

# Module identity

This skill is for the SharedLibs module named `Inventory`. Its source feature is
Steal A Pet `StorageManager`, not Steal A Pet `InventoryManager`. The source
InventoryManager owns mutagens, weather generators, and event pets and is an
explicitly excluded feature.

# Trigger and inputs

- Trigger: inherit the Storage core from `D:\Craftland\StealAPet` into
  `D:\Craftland\_Libs\SharedLibs`.
- Required intake: `reports/inheritance/inventory/00-intake.md`.
- Active source evidence: `Assets/Scripts/Manager/StorageManager.fcg` and its
  active call sites.

# Module-specific surface

Preserve the Storage-derived core contract:

- persistence keys `pStoragePets` and `pStorageBalance` in `PlayerSave`
- player-keyed pet list, balance, capacity, income, lock, and runtime caches
- load retry, ready signaling, save, delayed cache cleanup, and reconnect-safe
  initialization
- 8-hour retrieve lock and 4% storage-income multiplier
- store/retrieve Request -> Check -> Process actions
- large-number balance arithmetic through `BigNumberHandler`

Keep source-specific integrations outside SharedLibs behind the public hooks in
`InventoryManager.fcg`: capacity inputs, pet income inputs, timestamp, offline
delta, multiplier, pet snapshot, base-slot availability, feature availability,
wallet claim result, UI/prompt, and consumer pet transfer.

# Required common references

Load the router-selected common references under
`.agent/references/inheritance/`:

- `repository-first.md`
- `clone-first-workflow.md`
- `serialized-assets.md` when reviewing source UI/prefab assets
- `dependency-closure.md`
- `clone-fidelity.md`
- `mcp-last.md`
- `runtime-verification.md`
- `preserve-first-bindings.md`
- `repository-definition-search.md`
- `faithful-clone-mode.md`
- `stage-based-completion.md`
- `standalone-portability.md`
- `explicit-mcp-blockers.md`

Always run the `review-inherited-module` sections Clone Fidelity, Standalone
Portability, Feature Completeness, Folder Architecture, Asset Dependency
Closure, Active API Surface, Utility Reuse, Static Definitions,
Request-Check-Process, and Data Lifecycle.

# Workflow

1. Validate the configured source and SharedLibs roots and create the intake
   record before any non-report write.
2. Select the latest active `StorageManager` implementation from source call
   sites; do not select `InventoryManager`.
3. Inventory Storage persistence, actions, runtime state, config-derived
   capacity, income, lock, UI/trigger artifacts, and all transitive imports.
4. Clone the persistence and arithmetic behavior, reusing SharedLibs
   `DatabaseController` and `DataUtils` and copying only the missing generic
   `BigNumberHandler` utility.
5. Isolate source-only Managers and editor-owned UI/scene assets. Do not edit
   source assets or copy the Storage UI when the request is core logic only.
6. Validate the target with the full FC compiler. Record source-compatible
   behavior, consumer obligations, runtime gaps, and rollback requirements.
7. Generate inheritance, feature-surface, dependency, clone-fidelity, and
   portability reports plus the paired shared-to-consumer skill.

# Evidence requirements

Every material decision must cite a repository-relative path, symbol or key,
and an evidence label from `repository-first.md`. Explicitly record:

- the excluded source InventoryManager search and closure result
- source-to-target API mappings and intentionally omitted source-only APIs
- storage schema and formula fidelity
- utility reuse/copy decisions
- consumer hooks and the need to avoid running two managers against the same
  persistence keys
- exact FC compiler command and warnings

# Stop conditions

Stop only for invalid roots, missing intake, missing active Storage evidence, or
an exact strict MCP blocker. Missing runtime verification, source-only UI,
partial portability, and optional integrations do not block safe core output.

# Reports

- `reports/inheritance/inventory/`
- `reports/reviews/inventory/`
