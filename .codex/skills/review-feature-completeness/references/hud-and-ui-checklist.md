# HUD and UI Checklist

Use this reference when the source feature has any user-facing HUD or UI flow.

Verify:

- readable serialized UI assets, metadata, localization, and referenced assets
  inspected
- HUD scripts inspected
- buttons, lists, tabs, detail panels, or empty states traced when applicable
- Manager events or query APIs used by HUD are identified
- user actions initiated from HUD are traced
- source hierarchy and properties are preserved when a readable source asset exists
- HUD refresh after state changes is demonstrated
- directly serialized controls and bindings use verified evidence labels
- inferred controls have supporting call-site evidence
- ID preservation or complete remapping is documented
- custom enums, components, properties, and bindings were searched in repository
  definitions and preserved unchanged when structurally safe
- utilities and local textures were resolved through dependency closure
- runtime-only rendering and registration gaps are `Needs Studio verification`

Flag silent omission of required HUD behavior.

Do not accept a minimal replacement when a readable source asset exists. When no
serialized asset exists, a minimal replacement is a final fallback only after scripts,
metadata, config, and documentation are exhausted, and exact parity must be reported
as unavailable.
