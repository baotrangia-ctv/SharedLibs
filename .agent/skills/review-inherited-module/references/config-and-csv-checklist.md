# Config and CSV Checklist

Use this reference when the source feature uses CSV configuration or config readers.

Verify:

- CSV file inspected
- config reader inspected
- schema inspected
- default values identified
- Stage A parsing logic preserved
- Stage A validation logic preserved
- lookup methods preserved
- related enums or constants traced
- runtime consumers traced
- required reusable rows preserved and consumer-owned rows explicitly classified
- repository-accessible CSV and parsing code were inspected directly
- MCP was considered only after repository evidence was exhausted and strict stop
  conditions were evaluated

Flag missing config readers, schema changes, or hardcoded replacements. Stage B
changes require behavior, compatibility, and consumer-responsibility notes.

Do not flag unavailable Studio access when the CSV schema and runtime use are verified from repository files.
