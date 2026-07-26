# Feature Completeness

- Start every source-to-shared inheritance by discovering the complete feature surface.
- Do not assume the primary Manager file represents the whole module.
- Inspect and classify related assets and code under:
  - `Assets/HUDs/`
  - `Assets/Scripts/HUDs/`
  - `Assets/Scripts/Managers/`
  - `Assets/Scripts/Manager/`
  - `Assets/Scripts/Configs/`
  - `Assets/Scripts/Utils/`
  - `Assets/CSV/`
- Trace readable serialized assets, UI and HUD, scripts, config, CSV, data models,
  utilities, localization, dependencies, database registration, components, events,
  callbacks, cross-Manager integrations, and initialization entry points.
- Inspect repository evidence and build dependency closure before MCP.
- Produce a feature-surface inventory before implementation with:
  - source file
  - responsibility
  - required or optional status
  - active, legacy, deprecated, or uncertain status
  - evidence label
  - target handling decision
- Use the evidence labels in
  `.codex/references/inheritance/repository-first.md`.
- Mark Manager through Custom enums with a stage status from
  `.codex/references/inheritance/stage-based-completion.md`.
- Mark Standalone portability with a portability status and Runtime verification
  with a runtime status from their respective references.
- Complete Stage A clone fidelity before Stage B genericization.
- A feature with an available readable source asset is incomplete when the target
  contains only an invented simplified replacement.
- Map every generated file to its architectural layer and reject mixed feature folders by default.
- Confirm the primary flow is executable or testable without requiring standalone demo handlers.
- Report unnecessary demo artifacts, utility reuse decisions, static-definition decisions, adapter justifications, and final source file count.
- Report Manager, config, CSV, persistence, actions, events, HUD script, serialized
  HUD, textures, utilities, custom components, custom enums, standalone portability,
  and runtime verification independently.
- Do not mark the whole feature incomplete when only one presentation, portability,
  optional dependency, or runtime stage is unresolved.
