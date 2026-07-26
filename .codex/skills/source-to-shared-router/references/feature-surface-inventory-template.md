# Feature Surface Inventory Template

Create before Stage A cloning:

| Source artifact | Responsibility | Active status | Evidence label | Clone classification | Binding classification | Stage status | Portability impact | Target layer | Target handling |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

Active status:

- `Latest active`
- `Active compatibility`
- `Deprecated`
- `Unused`
- `Unresolved`

Clone classification:

- `Reusable as-is`
- `Reusable after path adjustment`
- `Reusable after dependency isolation`
- `Source-specific dependency`
- `Consumer integration point`
- `Deprecated`
- `Compatibility-only`
- `Unused`
- `Unresolved`

Stage status:

- `Complete`
- `Complete with unresolved bindings`
- `Partially complete`
- `Blocked`
- `Not applicable`
- `Runtime verification pending`

Use evidence labels from
`.codex/references/inheritance/repository-first.md`. Directly serialized values are
verified, not inferred.

Inventory scripts, serialized assets, config, CSV, persistence, events, public APIs,
utilities, assets, localization, custom components, integration points, and
transitive dependencies. Include preserve-first binding classifications, definition
search evidence, and standalone-portability impact. Do not replace an available
serialized asset with an invented simplified asset.
