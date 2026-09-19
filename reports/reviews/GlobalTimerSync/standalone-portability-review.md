# GlobalTimerSync Standalone Portability Review

**Result:** `Standalone with optional integrations`  
**Runtime:** `Not performed`

| Dependency / integration | Required | Handling | Consumer responsibility |
| --- | --- | --- | --- |
| `List.fcc`, `Map.fcc`, `StdLibrary.fcc` | Yes | Reuse engine libraries verified through local declarations | Keep standard library resolution available |
| `EditorGenLib.fcc` | Yes by target FC import convention | Reuse target generated library; not edited | Keep project compiler/editorGen valid |
| `Utils/TimeManager.fcg` | Yes | Included in the shared package with preserved anchor surface | Use shared utility or provide a compatible consumer binding |
| `GlobalTimerSyncDefinitions.fcg` | Yes | Included under `Configs/` | Use the public anchor identifiers and default epoch |
| Weather/Rotation/Global Spawn configs | No for core | Abstracted as `List<int>` and optional phase/epoch inputs | Build durations in milliseconds and pass the appropriate anchor mode |
| Weather/Rotation/Global Spawn Managers | No for core | Consumer integration points only | Retain business logic, events, state, and side effects |
| UI, scene, texture, localization, custom components | No | Excluded; no replacement invented | Consumer owns presentation and registration |
| Persistence/reconnect/database services | No | Not applicable | None |

The module compiles without source-project Managers, Configs, CSVs, UI, or
persistence. It remains runtime-dependent on the engine's server timestamp and
region APIs, which is an expected engine integration rather than a source-project
dependency. No exact MCP blocker exists.
