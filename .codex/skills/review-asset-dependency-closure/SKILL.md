---
name: review-asset-dependency-closure
description: Review the smallest complete transitive dependency closure for scripts, serialized assets, configs, CSV, localization, components, events, services, and engine references. Use whenever inherited files or assets reference other artifacts.
---

# Purpose

Prevent broken local references, missing dependencies, unnecessary bulk copies, and
silent asset substitutions.

# Required Inputs

- validated source and target roots
- root artifact inventory
- dependency-handling decisions

# Workflow

1. Read `.codex/references/inheritance/repository-first.md`.
2. Read `.codex/references/inheritance/dependency-closure.md`.
3. Read `.codex/references/inheritance/repository-definition-search.md`.
4. Read `.codex/references/inheritance/stage-based-completion.md`.
5. Parse file paths, asset IDs, script references, component definitions, config and
   CSV references, localization keys, events, services, and engine-library URIs.
6. Follow local references transitively and inspect utility API usage.
7. Validate relative texture and file paths and distinguish local from engine-owned
   dependencies.
8. Search source, shared, and applicable consumer repositories for definitions and
   equivalents.
9. Classify each dependency:
   - `Exists and can be copied`
   - `Exists and can be reused`
   - `Exists but source-specific`
   - `Definition can be extracted`
   - `Engine-owned`
   - `Missing`
   - `Requires MCP`
   - `Runtime verification required`
10. Flag incomplete closure and unrelated bulk copying.
11. Record affected-stage status and independent work that can continue.

# Allowed Changes

Modify only `reports/reviews/[module]/asset-dependency-closure-review.md`. Do not copy
or edit dependencies during this review.

# Required Evidence

Include repository-relative referencing, definition, and referenced paths; dependency
type; required or optional status; classification; target handling; texture or utility
analysis; affected stage; and smallest-complete-set conclusion.

# Stop Conditions

Stop the review when validated roots or root artifacts are unavailable. Do not block
an entire asset for one optional unresolved dependency. Require exact evidence from
`.codex/references/inheritance/explicit-mcp-blockers.md` before `Requires MCP`.
