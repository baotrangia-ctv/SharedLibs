# Minimal Source Generation

- Generate the smallest complete dependency closure that preserves the active feature
  flow. Minimal means no unrelated files, not a simplified replacement.
- During Stage A, retain each active artifact required for clone fidelity even when
  Stage B may later consolidate or isolate it.
- Prefer existing SharedLibs infrastructure, optional integrations, no-op defaults, callbacks, extension comments, and documentation examples over new provider classes.
- Do not create a file only to satisfy a template, but do not omit an active asset or
  dependency merely to reduce file count.
- Before completion, list files intentionally not created and confirm that each remaining file is used by the primary flow, required validation, or a documented public contract.
- Remove or consolidate unused wrappers, duplicate helpers, empty abstractions, and one-purpose files that increase integration cost without preserving behavior.
