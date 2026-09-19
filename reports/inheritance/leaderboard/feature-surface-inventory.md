# Leaderboard feature-surface inventory

Validated roots:

- Source: `D:\Craftland\StealAPet` (`read-only`, Git repository).
- Target: `D:\Craftland\_Libs\SharedLibs` (`read-write`, Git repository).

| Source artifact | Responsibility | Active status | Evidence label | Clone classification | Binding classification | Stage status | Portability impact | Target layer | Target handling |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `Assets/Scripts/Manager/LeaderboardManager.fcg` | Persistent global score loading and saving | Latest active | Verified from source script | Reusable after dependency isolation | Source-specific and isolatable | Partially complete | Source score Managers and database APIs removed | `Assets/Scripts/Managers/` | Preserve load/query/cache flow; replace score and persistence dependencies with mock provider |
| `Assets/Scripts/HUDs/HudLeaderboard.fcg` | HUD creation, two-state tab visuals, row rendering | Latest active | Verified from source script | Reusable after path adjustment | Requires remapping | Blocked | Requires imported HUD keys and attachment | `Assets/Scripts/HUDs/` | Adapt after target UI is registered |
| `Assets/HUDs/Leaderboard.ui` | Serialized leaderboard UI | Latest active | Verified from UI JSON | Reusable after path adjustment | Meaning known and valid | Blocked | Studio must be connected to target for import/edit | `Assets/HUDs/` | Import faithfully, then remove out-of-scope tabs and source-only script binding |
| `Assets/Scripts/Utils/CustomUIUtils.fcg` | Source-wide button router | Latest active | Verified from source script | Source-specific dependency | Source-specific and isolatable | Complete | Not portable | — | Exclude; replace with a leaderboard-only target HUD control |
| `Assets/Scripts/Manager/GlobalLeaderboard.fcg` | In-session world ranking | Active | Verified from source script | Source-specific dependency | Meaning known and valid | Not applicable | Separate gameplay flow | — | Exclude; not called by `HudLeaderboard` |
| `Assets/Sprites/Leaderboard/RankNo1.png` | First-place icon | Latest active | Verified from asset metadata | Reusable as-is | Meaning known and valid | Blocked | Import required | `Assets/Sprites/Leaderboard/` | Import with original metadata |
| `Assets/Sprites/Leaderboard/RankNo2.png` | Second-place icon | Latest active | Verified from asset metadata | Reusable as-is | Meaning known and valid | Blocked | Import required | `Assets/Sprites/Leaderboard/` | Import with original metadata |
| `Assets/Sprites/Leaderboard/RankNo3.png` | Third-place icon | Latest active | Verified from asset metadata | Reusable as-is | Meaning known and valid | Blocked | Import required | `Assets/Sprites/Leaderboard/` | Import with original metadata |
| `Assets/Sprites/Backgrounds/{BG,LabBG,SubTitleBG,TitleBG}.png` | Shared leaderboard backgrounds | Latest active | Verified from asset metadata | Reusable after path adjustment | Definition found in repository | Blocked | Import required | `Assets/Sprites/Backgrounds/` | Import by file ID; serialized paths are stale but IDs resolve to these definitions |
| `Assets/Sprites/Icons/CloseIcon.png` | Close icon | Latest active | Verified from asset metadata | Reusable after path adjustment | Definition found in repository | Blocked | Import required | `Assets/Sprites/Icons/` | Import by file ID |
| `Assets/Sprites/Shapes/ShadowSquareRounded.png` | Shared shape | Latest active | Verified from asset metadata | Reusable as-is | Meaning known and valid | Complete | None | Existing target sprite | Reuse target file ID `3cf4tu5o4v5-mbhqq60r-mcgu54jdbo` |
| `lib://fftextures/WorkshopIconLibrary/T_34_M_WS_ICON_SQUARE.png` | Engine profile placeholder | Latest active | Verified from UI JSON | Reusable as-is | Runtime verification required | Runtime verification pending | Engine-owned | Engine library | Preserve reference |

## Requested type scope

The source currently exposes four score tabs: `Income`, `Collection`, `Wealth`, and
`Like`. The requested shared scope explicitly allows only two. The inherited types
are `Income` and `Collection`; `Wealth` and `Like` are active source APIs intentionally
excluded by the user constraint.

Data contracts:

- Income row: `[rank:int, playerUid:UUID|nil, score:int]`.
- Collection row: `[rank:int, playerUid:UUID|nil, score:int, petsCount:int, variants:string]`.
- Current-player summary: `[rank:int, score:int]`.
