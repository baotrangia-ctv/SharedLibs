# UI Completeness

- When a source feature has UI, inheritance must include both the feature Manager and the feature HUD.
- Inspect readable serialized UI assets, HUD scripts, Manager call sites, events,
  query APIs, metadata, localization, and referenced local assets before MCP.
- Inspect:
  - UI assets under `Assets/HUDs`
  - HUD scripts
  - buttons
  - lists
  - tabs
  - detail panels
  - empty states
  - notification flows
  - Manager events consumed by HUD
  - Manager query APIs used for rendering
  - user actions initiated from HUD
- Classify each UI element as:
  - required generic UI
  - optional UI
  - source-project-specific visual behavior
  - validation-only replacement
  - consumer extension point
- When readable source UI exists, clone or faithfully reconstruct it before
  genericization. An invented simplified HUD is not an acceptable replacement.
- Preserve hierarchy, IDs or documented remapping, ordering, components, bindings,
  properties, localization, and dependencies according to
  `.codex/references/inheritance/serialized-assets.md`.
- Create a minimal replacement only as a final fallback when no serialized source
  asset exists, repository evidence and call sites support a safe implementation, and
  exact asset parity is reported as unavailable.
- Record live-rendering, editor-registration, and runtime-only gaps as
  `Needs Studio verification`; do not classify serialized values as inferred.
- HUD scripts may render data and receive input, but must not:
  - mutate database state directly
  - call `Process` directly
  - bypass Manager query or `Request` APIs
- Do not mark a module complete if required HUD functionality was silently omitted.
- Do not stop inheritance merely because live visual validation is unavailable when
  the serialized clone is safe and the strict MCP stop conditions do not apply.
