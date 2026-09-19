# Dependency Closure

Build the smallest complete dependency closure for every inherited module.

Inspect references to scripts, Managers, HUD scripts, UI assets, textures, icons,
fonts, config, CSV, localization, utilities, component definitions, prefabs,
variants, shared assets, engine libraries, events, data services, and persistence
services.

## Utilities

Inspect a referenced source utility and its dependencies. Classify APIs as `Generic
reusable`, `Source-specific`, `Deprecated`, or `Unused by module`. Reuse a compatible
target utility, copy the smallest reusable surface, extract broadly reusable behavior,
or isolate source-specific behavior. A source-wide utility reference is not a
whole-feature blocker.

## Textures and Files

For each local texture or readable file reference: locate it, verify existence, check
the target, copy only when required, adjust paths only when necessary, and validate
the result. Preserve `lib://` and other engine-library paths unless evidence requires
localization.

Classify textures as `Required blocking asset`, `Required but replaceable asset`,
`Optional visual asset`, `Engine library asset`, or `Missing unresolved asset`. Only
a required, non-replaceable dependency that makes the target structurally invalid can
block its affected asset stage.

Classify each dependency as:

- `Already exists in target`
- `Copy from source`
- `Adjust path`
- `Reuse target equivalent`
- `Abstract as integration point`
- `Engine library reference`
- `Source-specific and excluded`
- `Deprecated`
- `Missing`
- `Unresolved`

Also record whether a dependency exists and can be copied, reused, extracted, is
source-specific, engine-owned, missing, requires MCP, or only needs runtime
verification.

Trace references transitively until every active local reference has a handling
decision. Validate relative paths and distinguish local assets from engine-library
URIs.

Do not copy only a root file with broken references, copy unrelated directories,
silently replace a missing asset, duplicate existing target utilities, or copy an
engine-library reference locally without evidence.

For a missing dependency, search the validated repositories for relocated or
equivalent artifacts, continue all independent work, and report the gap. After
repository inspection, MCP may optionally resolve or verify Studio-only information.
Unavailable MCP blocks inheritance only when Studio is the sole authoritative source
and all strict MCP stop conditions apply.
