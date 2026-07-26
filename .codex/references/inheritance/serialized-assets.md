# Serialized Asset Handling

Treat readable JSON and structured-text assets as authoritative source files unless
repository evidence proves otherwise.

## Inspection

Inspect and preserve, where present:

- root type, asset version, prefab or variant references
- entity hierarchy, names, IDs, ordering, tags, layers, and visibility states
- component and widget types, properties, attached scripts, and custom components
- transforms, anchors, pivots, positions, sizes, rotations, alpha, and priority
- text, localization keys, sprites, file paths, asset IDs, and resource references
- layout, scroll, button, event, binding, and custom enum data

Do not treat directly serialized fields as inferred.

Apply `.codex/references/inheritance/preserve-first-bindings.md` to custom enums,
components, IDs, properties, scripts, and bindings. Unknown meaning is not evidence
of invalidity.

## Asset Clone Workflow

```text
Locate serialized source asset
    ->
Parse structure and properties
    ->
Inventory dependencies
    ->
Copy or reconstruct faithfully
    ->
Resolve or adjust references
    ->
Validate target fidelity
    ->
Refactor only confirmed source-specific content
```

When a readable source asset exists, do not replace it with an invented minimal or
simplified asset merely because MCP is unavailable.

## Identity

Preserve entity names, hierarchy, ordering, and references by default. Preserve IDs
when accepted by the target, collision-free, referenced, or fidelity-improving.
Regenerate an ID only when required for target validity or a confirmed collision.
When regenerating IDs, update every reference, validate the remapping, and report:

- `Preserved`
- `Regenerated`
- `Partially remapped`
- `Not applicable`

## Unknown Data

Do not delete unknown fields, components, enum values, or bindings automatically.
Classify each as:

- `Verified reusable`
- `Verified source-specific`
- `Potentially reusable`
- `Unresolved serialized binding`
- `Deprecated`
- `Unused`
- `Unsafe to copy`

Preserve unresolved data when safe. Delete it only with evidence that it is
deprecated, unused, invalid, unsafe, or tied exclusively to a replaced source-only
system. Document every deletion.

Repository inspection and fidelity comparison do not authorize unsupported semantic
editing or editor registration of opaque assets. Follow the repository's managed
asset rules for those operations.
