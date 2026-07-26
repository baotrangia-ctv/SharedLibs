# Mails Dependency Analysis

Before design or implementation, trace:

- Manager files
- HUD scripts
- UI assets
- config readers
- CSV files
- utility dependencies
- database registration
- events and callbacks
- cross-Manager integrations
- initialization entry points
- existing reports and documentation
- existing SharedLibs utilities, including `Assets/Scripts/Utils/DataUtils.fcg`
- repeated fields, statuses, actions, config keys, state identifiers, and result codes

Inspect repository-accessible evidence first. Do not request Studio merely to reproduce exact visual layout.

Produce the feature-surface and transitive dependency inventories before Stage A.
Use evidence labels from `.codex/references/inheritance/repository-first.md` and
dependency classifications from
`.codex/references/inheritance/dependency-closure.md`. Directly serialized details
are verified evidence; only runtime-only or editor-only gaps are
`Needs Studio verification`.

Map every source file to a target architectural layer. Reject a mixed `Assets/Scripts/Mails/` target and design the smallest complete file set.
