# Module Inheritance Routing

This file is the shared routing index for Codex and Claude Code. Full inheritance
content lives under `.agent/references/inheritance/` and `.agent/skills/`.

## Route by user request

- Inherit a module from Steal A Pet into SharedLibs: use
  `.agent/skills/source-to-shared-router/SKILL.md`.
- Add or inherit a SharedLibs module into another project: use
  `.agent/skills/shared-to-consumer-router/SKILL.md`.
- Review an inherited module: use
  `.agent/skills/review-inherited-module/SKILL.md` and select the applicable
  sections there.

User descriptions are sufficient; the user does not need to name a skill.

## Module skill naming

Module-specific skills use both pairs:

- `[module]-source-to-shared`
- `[module]-shared-to-consumer`

After a source-to-shared inheritance, the paired shared-to-consumer skill is
always generated from the collected feature surface, public contract, and
dependency closure.

## Mandatory intake gate

Before any file change outside `reports/`, the routed skill requires creating a
`00-intake.md` record under the module's report folder (see the router
SKILL.md's "Intake Gate" section and its `references/intake-record-template.md`).
This applies even to a single, simple module and even when a force keyword is
used. A missing or incomplete `00-intake.md` is a Stop Condition.

## Shared-to-consumer planning gate

Without an explicit force keyword, evaluate Complexity Gate before changing code.
A module is complex when it has at least four component types from {Manager,
HUD/UI script, Config/CSV, Persistence, Event, Public API/contract, independent
serialized asset}, or when it uses persistence, reconnect, runtime cache, or
network/server synchronization.

For a complex module, propose a concrete phase plan and stop for user approval.
After each approved phase, report the work and stop for review before continuing.

Explicit force keywords include `force`, `làm luôn`, `không cần plan`, `just do
it`, and `skip plan`. Force skips the approval stop but still records the
Complexity Gate result.

## Shared paths and invariants

- Project paths: `.agent/project-paths.json`.
- Inheritance references: `.agent/references/inheritance/`.
- Shared skills: `.agent/skills/`.
- Reports remain under `reports/inheritance/[module]/` and
  `reports/reviews/[module]/`; do not change that structure.
- Preserve module-specific workflow and behavior. Update references and
  structure only unless the active inheritance request explicitly requires
  implementation work.

Adapters in `.codex/` and `.claude/` point here and must not duplicate the full
inheritance rules or skill content.
