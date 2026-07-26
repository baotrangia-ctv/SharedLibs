# Clone First, Refactor Second

- Stage A faithfully captures the latest active source behavior, contracts, assets,
  lifecycle, integrations, and complete dependency closure.
- Stage A uses Faithful Clone Mode and may remain source-compatible while standalone
  portability work continues separately.
- Stage B isolates source-specific dependencies, reuses SharedLibs infrastructure,
  introduces minimal extension points, and organizes files by layer.
- Do not genericize, redesign, simplify assets, or remove active behavior before
  Stage A clone fidelity is reviewed.
- Preserve behavior during genericization and document every abstraction, removal,
  replacement, compatibility impact, and consumer responsibility.
- Follow `.codex/references/inheritance/clone-first-workflow.md`.
