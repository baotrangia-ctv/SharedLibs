# MCP-Last Verification

Craftland Studio Connect MCP is optional and used only after repository inspection.

Valid MCP uses include runtime-only behavior, editor-only relationships absent from
files, runtime-generated relationships, unrecorded import or registration state,
unresolvable engine-generated references, custom-enum meaning proven to affect
structural validity or authoritative behavior, scene-level
relationships absent from files, visual corruption diagnosis, and live runtime
validation.

UI presence, large or complex assets, custom components, unfamiliar properties, CSV,
filesystem path resolution, a preference for visual inspection, and untested visual
rendering are not valid reasons to require MCP.

## Strict MCP Stop Conditions

Use all six conditions and exact evidence fields from
`.codex/references/inheritance/explicit-mcp-blockers.md`.

Potential blockers include an unknowable authoritative behavior, critical runtime
binding, public API, data schema, required runtime registration, or a risk of invalid
or destructive target files.

When MCP is unavailable but non-blocking, complete every safe stage, preserve
unresolved serialized data when safe, mark portability and runtime gaps separately,
enumerate exact blockers, and do not claim runtime validation.
