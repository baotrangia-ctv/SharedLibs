# MCP-Last Verification

- Craftland Studio Connect MCP is optional and must be used only after repository
  scripts, readable serialized assets, dependencies, reports, and documentation have
  been inspected.
- Repository-accessible CSV and parsing code do not require Studio.
- Do not require MCP because an asset is UI, large, complex, custom, unfamiliar, or
  not yet visually tested.
- Stop because MCP is unavailable only when all six strict conditions in
  `.codex/references/inheritance/explicit-mcp-blockers.md` are true.
- When MCP is unavailable but non-blocking, continue repository inheritance,
  preserve unresolved serialized data when safe, record `Needs Studio verification`
  gaps, and report runtime verification separately.
- A serialized clone may complete without live Studio validation. Never claim runtime
  validation that was not performed.
- This policy governs inheritance evidence and completion. It does not authorize
  unsupported semantic editing or registration of opaque editor-owned assets outside
  the managed Craftland Studio rules.
- Unknown custom values, unresolved optional bindings, local textures, repository
  utilities, partial portability, and unavailable runtime verification are not
  full-task blockers.
