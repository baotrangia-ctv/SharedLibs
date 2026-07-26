# Preserve First, Remap Only When Required

- Inspect repository definitions and usages before changing serialized enums,
  components, IDs, properties, scripts, or bindings.
- Preserve serialized values by default when structurally safe.
- Unknown meaning does not mean invalid. Require evidence before remapping,
  regenerating, deleting, or classifying structural invalidity.
- Copy or adapt repository definitions before introducing an integration point.
- Consider MCP only after preserve, copy, adapt, and isolate options are exhausted.
- Follow `.codex/references/inheritance/preserve-first-bindings.md`.
