## Codex Skill Routing

Use project paths from `.codex/project-paths.json`.

Available global routers:

Skill: `source-to-shared-router`
Use when: The user asks to inherit, generalize, adapt, or inspect a Steal A Pet module for this SharedLibs project.
May combine with: `review-clone-fidelity`, `review-standalone-portability`, `review-serialized-asset-fidelity`, `review-asset-dependency-closure`, `review-feature-completeness`, and focused architecture or behavior reviews.

Skill: `shared-to-consumer-router`
Use when: The user asks to add a completed SharedLibs module to another consumer project.
May combine with: `review-standalone-portability`, `review-serialized-asset-fidelity`, `review-asset-dependency-closure`, and focused architecture or integration reviews.

Available reusable review skills:

Skill: `review-clone-fidelity`
Use when: Every source-to-shared inheritance must prove faithful capture before genericization.
May combine with: `source-to-shared-router`, `review-feature-completeness`.

Skill: `review-standalone-portability`
Use when: A faithful clone must be assessed for remaining source-project, utility, component, enum, consumer, or runtime dependencies.
May combine with: `source-to-shared-router`, `shared-to-consumer-router`, `review-clone-fidelity`.

Skill: `review-serialized-asset-fidelity`
Use when: Readable serialized assets are copied, reconstructed, adapted, or compared.
May combine with: `source-to-shared-router`, `shared-to-consumer-router`.

Skill: `review-asset-dependency-closure`
Use when: Inherited scripts or assets reference other files, assets, configs, components, events, or services.
May combine with: `source-to-shared-router`, `shared-to-consumer-router`.

Skill: `review-data-lifecycle`
Use when: A module loads or saves player data, keeps runtime cache, registers readiness, handles reconnect, quit, shutdown, or persistent rewards.
May combine with: `source-to-shared-router`, `shared-to-consumer-router`.

Skill: `review-request-check-process`
Use when: A module exposes public Manager actions or user-triggered operations.
May combine with: `source-to-shared-router`, `shared-to-consumer-router`.

Skill: `review-production-readiness`
Use when: Real persistence or rewards are connected, placeholder behavior is removed, or an integration is intended for release.
May combine with: `shared-to-consumer-router`, `review-data-lifecycle`, `review-request-check-process`.

Skill: `review-feature-completeness`
Use when: A source-to-shared inheritance must confirm that Manager, HUD, config, CSV, persistence, events, executable primary flow, documentation, and portability layers were fully considered.
May combine with: `source-to-shared-router`, `review-request-check-process`, `review-data-lifecycle`.

Skill: `review-active-api-surface`
Use when: Duplicate, versioned, legacy, deprecated, or compatibility APIs may exist in the source feature.
May combine with: `source-to-shared-router`, `review-feature-completeness`.

Skill: `review-folder-architecture`
Use when: Generated or integrated files must be checked for responsibility-based placement and mixed-layer feature folders.
May combine with: `source-to-shared-router`, `shared-to-consumer-router`.

Skill: `review-utility-reuse`
Use when: A feature parses, serializes, converts, or stores structured data and should reuse `DataUtils` or other existing utilities.
May combine with: `source-to-shared-router`, `shared-to-consumer-router`.

Skill: `review-static-definitions`
Use when: A feature introduces repeated fields, statuses, action names, config keys, state identifiers, or result codes.
May combine with: `source-to-shared-router`, `shared-to-consumer-router`.

Future module workflow skill naming:

- `[module]-source-to-shared`
- `[module]-shared-to-consumer`

Users normally do not need to name skills explicitly.

Example requests:

- `Inherit Activities from Steal A Pet into the shared project.`
- `Add the shared Activities module to this game.`

General review principles:

- Combine only the smallest sufficient set of skills.
- Every source-to-shared inheritance uses `review-clone-fidelity`.
- Every source-to-shared inheritance reports `review-standalone-portability`
  separately from clone fidelity.
- Every source-to-shared inheritance uses `review-feature-completeness`.
- Every source-to-shared inheritance uses `review-folder-architecture`.
- Every task involving readable serialized assets uses `review-serialized-asset-fidelity`.
- Every task involving referenced files or assets uses `review-asset-dependency-closure`.
- Use `review-active-api-surface` when duplicate, versioned, legacy, or deprecated APIs exist.
- Use `review-utility-reuse` when a feature parses, serializes, converts, or stores structured data.
- Use `review-static-definitions` when repeated fields, statuses, action names, config keys, state identifiers, or result codes are introduced.
- Use `review-request-check-process` for public Manager actions.
- Use `review-data-lifecycle` for persistence, cache, readiness, reconnect, quit, shutdown, or persistent rewards.
- Use `review-production-readiness` for release-facing or real consumer integration work.
- Do not invoke demo-related skills or generate demo service classes by default.
- Inspect repository files before MCP, clone the latest active source implementation before genericization, and preserve available serialized assets rather than inventing simplified replacements.
- Preserve serialized bindings before remapping; unknown meaning does not mean
  structural invalidity.
- Search source and shared repository definitions before MCP.
- Complete all safe independent stages and use Faithful Clone Mode before standalone
  refactoring.
- Require exact identifier and repository evidence for every MCP blocker.
- Do not block the whole inheritance for one unresolved optional dependency.
- Track serialized clone completion separately from live runtime verification.
- Track clone fidelity, standalone portability, and runtime verification separately.
- Organize files by architectural layer, copy the smallest complete dependency closure, reuse existing utilities, centralize only reused definitions, and require justification for every adapter.

Repository-first and MCP-last policy:

- Inspect scripts, readable serialized assets, dependencies, reports, and documentation before MCP.
- Preserve directly serialized hierarchy, properties, identity, references, and unknown data when safe.
- Use MCP only for unresolved runtime-only or editor-only information after repository inspection.
- Stop the whole inheritance for unavailable MCP only when all six strict conditions
  in `.codex/references/inheritance/explicit-mcp-blockers.md` are true.
- A serialized clone may complete while runtime Studio verification remains pending.
- A minimal replacement is a final fallback only when no readable source asset exists and repository evidence supports a safe implementation.
- These inheritance rules do not authorize unsupported semantic editing or registration of opaque editor-owned assets outside the managed rules below.

<!-- BEGIN craftland-studio-asset-rules -->
## Synced from craftland-studio-assets.mdc

# Craftland Studio Asset Rules

## Core Rule

Craftland Studio is the authoritative editor for game assets in this project.

- Any access to or modification of game assets must use Craftland Studio.
- Only `.fcc` and `.fcg` files may be edited directly as text and compiled through the FC toolchain.
- If a task involves non-text game assets, especially `.eca` files, the agent must first check whether Craftland Studio is available through MCP.
- If Craftland Studio is not available for the current session, the agent must tell the user to open the game editor first before attempting that asset task.
- The agent must not guess or hand-edit serialized asset formats such as `.eca` when Craftland Studio is required but unavailable.

## Directory Scope

The following directories belong to the Craftland Studio project structure:

- `Assets/` user asset files, including `.fcc` and `.fcg`
- `ProjectSettings/` user configuration asset files
- `Temp/` temporary files, records, debug output, and compilation results
- `Libraries/` library files
- `Cache/` project cache

## Working Rules

- For requests involving `.fcc` or `.fcg`, direct text editing is allowed.
- For requests involving assets under the directories above that are not `.fcc` or `.fcg`, prefer Craftland Studio and related MCP tools.
- Before handling `.eca`, entity attachment, asset registration, scene assets, workflow assets, or other editor-owned assets, first verify whether Craftland Studio MCP is connected.
- Once Craftland Studio MCP is connected, the agent must read `instructions://index` before using other Craftland Studio MCP tools or resources.
- If the MCP is unavailable, stop and ask the user to open Craftland Studio, then retry the task after the editor-side connection is ready.
<!-- END craftland-studio-asset-rules -->

## Inheritance Evidence Scope

For source-to-shared and shared-to-consumer inheritance, readable serialized JSON
and structured-text assets are repository evidence and may be inspected directly.
A byte-faithful Stage A copy of such an artifact is not a semantic editor operation.
The managed asset rules govern semantic asset editing, entity attachment, editor
registration, opaque formats, and live Studio validation. Their unavailable-MCP stop
applies only to the blocked editor-owned subtask, not to read-only repository
inspection, dependency inventory, fidelity review, or other safe inheritance work.
Semantic target changes and registration must still use the permitted Studio or
toolchain workflow.

<!-- BEGIN craftland-studio-fc-workflow -->
# Craftland Studio FC Agent Entry

This managed section is for any agent that reads the project root `AGENTS.md`. Craftland Studio sync must update only this section and must not overwrite the user's full `AGENTS.md`.

## Scope

This is a Craftland Studio UGC project. Any task involving `.fcg`, `.fcc`, FC APIs, FC imports, FC diagnostics, or FC generated project symbols is an FC task.

FC tasks mainly involve:

- `Assets/`: user-owned `.fcg` / `.fcc` source files.
- `Temp/UGCLanguage/`: toolchain config, generated libraries, symbol tables, and referenced package caches.

## Required Entry Point

Every FC coding task must read and strictly follow the official Craftland Studio agent workflow:

- `.craftland/agents/rules/fc-workflow.mdc`

Skills must be loaded from:

- `.craftland/agents/skills/`

If the official `.craftland/agents/` workflow is missing or cannot be read, stop and report the missing file. Do not bypass the workflow and handle FC tasks directly.

Legacy `.cursor/rules/` and `.cursor/skills/` FC rules may still exist in older projects, but Craftland Studio no longer maintains them. When `.craftland/agents/` exists, it has higher priority than any existing `.cursor` FC rules.

## Non-Negotiable Rules

- Do not invent FC APIs, types, events, enum values, component names, imports, assetIds, entityIds, or generated project symbols from memory.
- Craftland Studio is the authority for asset registration. Agents must not fake registration by writing FC code.
- Generated files under `Temp/UGCLanguage/editorGen/` are read-only references and must not be edited as user source.
- Any `.fcg` / `.fcc` edit is not complete until full `fccompile.exe -i Assets` validation or an equivalent Craftland Studio MCP build validation has run.
<!-- END craftland-studio-fc-workflow -->
