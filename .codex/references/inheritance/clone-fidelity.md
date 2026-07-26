# Clone Fidelity

Review Stage A independently from Stage B.

Verify that:

- the latest active source implementation was selected
- deprecated and unused implementations were excluded
- required compatibility behavior was retained only with call-site evidence
- active Manager and HUD behavior was captured
- public APIs, callbacks, events, and Request -> Check -> Process were preserved
- config and CSV schemas and loading flows were preserved
- load, save, runtime-state, and persistence lifecycle were preserved
- readable serialized assets, identity, references, and bindings were preserved
- localization and required local assets were included
- the complete dependency closure was inventoried and clone-critical dependencies
  were included or structurally preserved
- source-specific dependencies and consumer integration points were classified
- all removed behavior and every abstraction were documented
- no abstraction preceded faithful capture
- no available source asset was replaced by an unjustified simplified asset

Record each comparison as `Preserved`, `Intentionally changed`, `Missing`, `Added`,
`Remapped`, `Unresolved`, or `Not applicable`, with repository-relative evidence.

Clone fidelity can pass with runtime verification pending when serialized and source
evidence is complete and no strict MCP blocker applies. It can also pass as
source-compatible when unknown values are structurally preserved and standalone
portability gaps are explicit.
