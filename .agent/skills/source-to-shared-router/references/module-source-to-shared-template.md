# Module Source-to-Shared Skill Template

Future `[module]-source-to-shared` skills must remain module-focused and load shared
policy rather than duplicate it.

## Required Common References

- `repository-first.md` always
- `clone-first-workflow.md` always
- `serialized-assets.md` when readable serialized assets exist
- `dependency-closure.md` when files or assets reference other artifacts
- `clone-fidelity.md` before Stage B
- `mcp-last.md` before any MCP request or MCP-related stop
- `runtime-verification.md` when reporting completion
- `preserve-first-bindings.md` always
- `repository-definition-search.md` when custom or unresolved definitions exist
- `faithful-clone-mode.md` always
- `stage-based-completion.md` always
- `standalone-portability.md` always
- `explicit-mcp-blockers.md` before blocking any stage for unavailable MCP

All paths are under `.agent/references/inheritance/`.

## Required Workflow

```text
Validate paths
    ->
Discover complete feature surface
    ->
Identify latest active implementation
    ->
Inventory scripts, Managers, HUD scripts, serialized assets, Config, CSV,
persistence, events, Utils, localization, and public APIs
    ->
Build dependency closure
    ->
Search repository definitions
    ->
Choose preserve, copy, adapt, or isolate handling
    ->
Complete safe independent stages
    ->
Create Faithful Clone Mode output
    ->
Run serialized, dependency, and clone-fidelity reviews
    ->
Assess standalone portability
    ->
Refactor safe SharedLibs stages
    ->
Introduce minimal extension points
    ->
Organize files by architectural layer
    ->
Run architecture and quality reviews
    ->
Generate reports
    ->
Use MCP only for exact unresolved blockers and optionally verify runtime
```

## Required Skill Content

Define trigger, inputs, outputs, validated read/write scope, module-specific surface
and lifecycle checks, feature-specific references, relevant reusable reviews,
evidence requirements, strict stop conditions, and report locations.

Always require the `review-inherited-module` sections Clone Fidelity, Standalone
Portability, Feature Completeness, and Folder Architecture. Conditionally require
the Serialized Asset Fidelity, Asset Dependency Closure, Active API Surface,
Utility Reuse, Static Definitions, Request-Check-Process, Data Lifecycle, and
Production Readiness sections.

Stage A must preserve source-specific behavior before Stage B isolates it. Do not
create simplified assets when readable source assets exist. A minimal replacement is
allowed only when no serialized source asset exists, repository evidence supports a
safe fallback, and exact parity is reported unavailable.

Keep source projects read-only. Apply layer placement, utility reuse, Adapter-Last,
and Demo-Last. Report stage completion, faithful clone fidelity, standalone
portability, and runtime verification separately. Unknown custom values and one
blocked optional dependency do not block all safe output.
