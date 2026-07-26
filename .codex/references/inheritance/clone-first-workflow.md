# Clone-First Workflow

Use two explicit stages.

## Stage A: Faithful Source Clone

Run Stage A in Faithful Clone Mode using
`.codex/references/inheritance/faithful-clone-mode.md`.

1. Discover the complete source feature surface.
2. Identify the latest active implementation from call sites and registrations.
3. Inventory scripts, Managers, HUD scripts, serialized assets, config, CSV,
   persistence, events, utilities, localization, public APIs, and reports.
4. Build the smallest complete dependency closure.
5. Faithfully clone the active behavior, data contracts, assets, lifecycle,
   integrations, and dependencies.
6. Validate clone completeness before abstraction.

Do not redesign architecture, invent replacement assets, or remove active
source-specific behavior during Stage A.

Classify every discovered artifact as:

- `Reusable as-is`
- `Reusable after path adjustment`
- `Reusable after dependency isolation`
- `Source-specific dependency`
- `Consumer integration point`
- `Deprecated`
- `Compatibility-only`
- `Unused`
- `Unresolved`

Only the latest active implementation is cloned unless active compatibility evidence
proves that an older path is still required.

## Stage B: Shared Module Refactor and Portability

1. Classify source-specific dependencies.
2. Reuse compatible SharedLibs utilities.
3. Isolate source-specific behavior behind the smallest necessary extension point.
4. Remove only confirmed deprecated, unused, or source-only artifacts.
5. Organize files by architectural responsibility.
6. Preserve externally observable behavior and public contracts.
7. Document every behavior change, abstraction, removal, and consumer obligation.
8. Run final architecture and quality reviews.

Clone-first must not become adapter-first. Apply Adapter-Last and Demo-Last during
Stage B. Report standalone portability separately; a source-compatible Stage A clone
may complete before Stage B is fully portable.
