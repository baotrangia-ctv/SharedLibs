# Leaderboard source-to-shared inheritance report

## 1–4. Module, projects, and repository evidence

- Module: Leaderboard.
- Source: `D:\Craftland\StealAPet` (read-only).
- Target: `D:\Craftland\_Libs\SharedLibs` (read-write).
- Evidence inspected: active Manager/HUD scripts, navigation call sites, generated
  `LeaderboardType` and button definitions, serialized `Leaderboard.ui`, metadata,
  texture definitions, Git history/blame, target Managers/HUDs/Mockups/Configs/Utils,
  and target generated FC libraries.

## 5–7. Active selection, exclusions, and cloned files

- Selected active implementation: `LeaderboardManager.fcg` +
  `HudLeaderboard.fcg` + `Leaderboard.ui` (`Verified from source script`,
  `Verified from UI JSON`).
- `GlobalLeaderboard.fcg` is an active but separate in-session ranking flow and was
  excluded.
- Source-active `Wealth` and `Like` were intentionally excluded because the user
  requires exactly two score types.
- Safe target files created:
  - `Assets/Scripts/Configs/LeaderboardDefinitions.fcg`
  - `Assets/Scripts/Managers/LeaderboardManager.fcg`
  - `Assets/Scripts/Mockups/LeaderboardMockScoreProvider.fcg`

## 8–13. Omissions, serialized assets, IDs, bindings, and dependencies

- The serialized HUD and textures are not yet cloned because Craftland Studio is
  connected to another/no project context. `Assets/HUDs/Mail.ui`, which exists in the
  validated target repository, returns `Asset not found`; importing the source HUD
  returns `Import failed`.
- Source UI SHA-256:
  `85C140389F42B65A91ADDFCE35FA0053AC5DB9C3A7BF750237280AF681E773BF`.
- Source UI structure: 89 entities, including four score buttons, loading label,
  ten rank rows, and current-player row.
- Preserve UI and texture IDs on import. Reuse target
  `ShadowSquareRounded.png` by its matching source file ID.
- Replace only the source-wide `CustomUIUtils.fcg` binding with a target
  leaderboard-specific HUD control after import.
- Dependency closure is recorded in
  `reports/reviews/leaderboard/asset-dependency-closure-review.md`.

## 14–20. Config, CSV, lifecycle, APIs, dependencies, and genericization

- Config fidelity: two type identifiers, UI states, row indices, and mock-state
  identifiers are centralized in `LeaderboardDefinitions.fcg`.
- CSV: not applicable.
- Persistence: deliberately deferred; no database writes or quit-save behavior are
  included while scores are mocked.
- Public query contract preserves rows, current-player summary, and state output.
- Source score Managers (`WalletManager`, `CollectionManager`, `ProfileManager`,
  `PlayerBase`, `PlayersManager`, `PlayerGMT`) are isolated behind the single imported
  mock provider.
- Genericization changes: enum keys became portable string definitions; the real
  database score source became `LeaderboardMockScoreProvider`; loading, empty, and
  error states are explicit.

## 21–25. Utilities, interfaces, adapters, placement, and demos

- Existing `List.Clone` and standard Map/List APIs are reused. `DataUtils` is not
  applicable because no parsing or serialization is performed.
- The score replacement seam is the Manager import
  `LeaderboardMockScoreProvider as LeaderboardScoreProvider`.
- No pass-through adapter was introduced.
- Files follow Configs, Managers, Mockups, HUDs, and HUD asset layers.
- No demo service or unrelated leaderboard type was added.

## 26–31. Clone, runtime, MCP, Studio gaps, consumer work, and stages

- Serialized clone status: `Incomplete`.
- Runtime verification status: `Not performed`.
- MCP usage: repository inspection preceded MCP. MCP was used only for the target UI
  import/registration attempt.
- Studio-only gap: open the SharedLibs project, import the HUD and textures, remove
  `WealthButton`, `LikeButton`, and the inactive `TabsRegion`, replace the UI script
  attachment, save, regenerate editor symbols, and build.
- Consumer work: replace the mock provider import/implementation with the real score
  provider later; no HUD/Manager contract change is required.
- Stages:
  - Source discovery: `Complete`
  - Active API analysis: `Complete`
  - Manager clone: `Complete`
  - Config and CSV clone: `Complete`
  - Data lifecycle clone: `Complete`
  - Serialized asset clone: `Blocked`
  - Dependency closure: `Complete`
  - Shared refactor: `Partially complete`
  - Runtime verification: `Runtime verification pending`

## 32–39. Files, fidelity, portability, runtime, and dependency analysis

- Safe files created are listed above plus inheritance/review reports and the
  module workflow skill.
- Safe files modified: local `.codex/project-paths.json`.
- Faithful clone status: `Source-compatible`, script/query subset only.
- Clone fidelity status: `Fail` until the required serialized HUD and HUD scripts
  are present.
- Standalone portability status: `Consumer adaptation required`.
- FC validation: full `fccompile_external.exe -i Assets` passed for the safe script
  stage; existing unrelated deprecation warnings remain in `HudControls.fcg`.
- Utility dependency analysis: standard Map/List APIs suffice.
- Texture dependency analysis: seven source-local textures are required, one source
  shape already exists by matching ID, and one engine-library texture is preserved.

## 40–49. Definitions, preserved/remapped values, blockers, and remaining work

- Custom enums: source `LeaderboardType` has four values. Target uses exactly two
  string identifiers to honor scope and avoid importing unrelated enum values.
- Custom components: none required.
- Definitions found: all local texture file IDs, source HUD keys, source button enum
  call sites, and target shared shape.
- Preserved unchanged: row ordering, score ordering, row index contract, current-rank
  summary, cache-on-first-load behavior, and the loading-first UI flow.
- Remapped: `LeaderboardType.Income` → `"Income"`;
  `LeaderboardType.Collection` → `"Collection"`.
- Unresolved but preserved: engine-library profile placeholder reference, pending UI
  import.
- Exact MCP blocker:
  - Identifier: target UI asset import/registration for source file ID
    `t2tdftm3e8h-mgqeyw21-b1bw8lyztw`.
  - Source file: `Assets/HUDs/Leaderboard.ui`.
  - Target file: `Assets/HUDs/Leaderboard.ui`.
  - Dependency type: required serialized HUD.
  - Searches: validated source/target HUD and metadata paths; target asset open.
  - Definition found: yes, in source repository.
  - Safe preservation: yes, byte-faithful import is planned.
  - Filesystem adaptation: semantic tab/script edits require Studio.
  - Invalidity reason: current MCP editor context does not index the target project.
  - MCP resolution: open the target SharedLibs project and retry import/edit/save.
  - Affected stage: Serialized asset clone.
  - Other stages may continue: yes; Manager/config/mock compilation completed.
- Work completed without MCP: discovery, API/type selection, dependency inventory,
  Manager/config/mock implementation, full local FC compile, and reports.
- Work remaining with Studio: HUD import, dependency import, entity removal, script
  attachment, save, symbol regeneration, editor build, and runtime visual checks.
- Consumer adaptation: implement real score loading/current-player lookup behind the
  provider boundary and preserve the returned row/state contract.
