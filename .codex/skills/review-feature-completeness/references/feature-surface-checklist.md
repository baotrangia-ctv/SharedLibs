# Feature Surface Checklist

Use this reference for every source-to-shared inheritance.

Verify and status independently:

- Manager
- Config
- CSV
- Persistence
- Actions
- Events
- HUD script
- Serialized HUD asset
- Textures
- Utilities
- Custom components
- Custom enums
- Standalone portability
- Runtime verification

Also verify the inheritance considered:

- primary Manager
- runtime helpers
- database registration
- load flow
- save flow
- action flow
- HUD scripts
- serialized UI assets
- other serialized assets
- config readers
- CSV files
- utility dependencies
- events and callbacks
- assets and localization
- custom components and serialized bindings
- dependency closure
- consumer integration points
- executable or testable primary flow
- documentation
- portability manifest
- target architectural-layer mapping
- minimal source file set
- existing utility reuse
- static-definition ownership
- adapter justification
- unnecessary demo artifacts

Mark Manager through Custom enums `Complete`, `Complete with unresolved bindings`,
`Partially complete`, `Blocked`, `Not applicable`, or `Runtime verification pending`.

Mark Standalone portability with a status from the standalone-portability reference.
Mark Runtime verification with a status from the runtime-verification reference.

Verify repository evidence was inspected before MCP and important findings use a
label from `.codex/references/inheritance/repository-first.md`.

When a readable serialized source asset exists, reject a target containing only an
invented simplified replacement.

Do not fail all surfaces because one optional dependency, presentation binding,
standalone-portability task, or runtime check remains unresolved.

Do not accept "Manager logic exists" as proof that the feature is complete.

Do not mark a module incomplete merely because it has no standalone demo handlers. Flag demo files that duplicate infrastructure, are unused by the primary flow, satisfy only an outdated rule, or increase integration complexity.
