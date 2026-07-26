# Config Preservation

- Preserve reusable CSV-loading mechanisms when the source module uses CSV configuration.
- Inspect repository-accessible CSV files and config readers directly before considering Studio or MCP access.
- Inspect:
  - CSV file
  - config reader
  - config schema
  - default values
  - parsing logic
  - validation logic
  - lookup methods
  - related enums or constants
  - runtime consumers of the config
- During Stage A, preserve the active CSV-driven flow, schema, parsing, validation,
  defaults, and required rows. Do not replace it with hardcoded values.
- During Stage B, shared modules should normally retain:
  - a generic config model
  - a CSV reader
  - schema validation
  - source rows required to preserve reusable behavior
  - documentation for adding rows
  - mapping between CSV fields and runtime behavior
- Classify production rows before Stage B. Preserve reusable rows, defer
  consumer-owned rows through a documented integration point, and remove
  source-specific rows only after their behavior and replacement path are documented.
- Do not require Studio to read a CSV file or parsing code that is available on disk.
- After repository inspection, MCP may optionally verify runtime-only CSV
  registration. Unavailable MCP blocks the whole inheritance only when all conditions
  in `.codex/references/inheritance/explicit-mcp-blockers.md` apply; otherwise block
  only the affected registration or runtime stage.
