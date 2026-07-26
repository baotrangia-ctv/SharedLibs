# Repository-First Evidence

Use repository-accessible files as the primary source of truth for inheritance.

## Evidence Priority

```text
Repository scripts and serialized assets
    ->
Referenced repository files and dependencies
    ->
Existing reports and documentation
    ->
Craftland Studio Connect MCP
```

Inspect scripts, readable serialized UI and asset files, HUD assets, CSV, config,
metadata, serialized components and events, localization, referenced local assets,
reports, and documentation before requesting MCP access.

Do not require MCP because a feature has UI, custom components, serialized events,
CSV, asset references, a complex hierarchy, or unfamiliar enum values.

## Evidence Labels

Use exactly one label for every important finding:

- `Verified from source script`
- `Verified from serialized asset`
- `Verified from UI JSON`
- `Verified from CSV`
- `Verified from config`
- `Verified from asset metadata`
- `Verified from serialized component data`
- `Verified through Studio MCP`
- `Inferred from call-site evidence`
- `Needs Studio verification`
- `Unresolved`

Directly serialized values are verified evidence, not inference. Use `Inferred from
call-site evidence` only when a conclusion is derived from usage rather than stored
directly.

Record repository-relative paths and the exact symbols, fields, IDs, or references
supporting each material decision.
