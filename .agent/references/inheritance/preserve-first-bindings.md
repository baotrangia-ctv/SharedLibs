# Preserve-First Bindings

For serialized enums, components, IDs, properties, scripts, and bindings, use this
decision order:

```text
Can preserve unchanged safely?
    -> Preserve unchanged
Cannot preserve, but a repository definition exists?
    -> Copy or adapt the definition
Cannot copy, but behavior can be isolated?
    -> Create the smallest integration point
Cannot preserve, copy, adapt, or isolate safely?
    -> Consider MCP
MCP unavailable and target would be structurally invalid?
    -> Block only the affected stage
```

Classify each binding:

- `Meaning known and valid`
- `Meaning unknown but structurally preservable`
- `Definition found in repository`
- `Definition missing but optional`
- `Source-specific and isolatable`
- `Requires remapping`
- `Structurally invalid in target`
- `Runtime verification required`

Unknown meaning is not invalidity. Preserve unfamiliar numeric IDs, property IDs,
generated values, complete custom-component data, source entity IDs, copyable script
references, and alternate serialized bindings when structurally safe.

Require concrete repository evidence before `Requires remapping` or `Structurally
invalid in target`. Do not remap merely to obtain a display name. Do not delete,
regenerate, or reinterpret a value without evidence and a complete reference update.
