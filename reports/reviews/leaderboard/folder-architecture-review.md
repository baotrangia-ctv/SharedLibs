# Folder architecture review

| File | Responsibility | Correct target folder | Decision | Evidence |
| --- | --- | --- | --- | --- |
| `Assets/Scripts/Managers/LeaderboardManager.fcg` | Authoritative query/cache logic | `Assets/Scripts/Managers/` | Retain | Manager layer convention |
| `Assets/Scripts/Configs/LeaderboardDefinitions.fcg` | Shared type/state/row definitions | `Assets/Scripts/Configs/` | Retain | Used by Manager, provider, and future HUD |
| `Assets/Scripts/Mockups/LeaderboardMockScoreProvider.fcg` | Temporary mock score source | `Assets/Scripts/Mockups/` | Retain with documented exception | Target already has a Mockups layer; isolated replacement seam |
| `Assets/HUDs/Leaderboard.ui` | Serialized UI | `Assets/HUDs/` | Retain when imported | UI asset layer convention |
| Future `HudLeaderboard.fcg` and control | UI behavior | `Assets/Scripts/HUDs/Leaderboard/` | Retain with documented exception | Two closely related HUD-only files match existing Mails/Collection convention |

No mixed `Assets/Scripts/Leaderboard/` feature folder was introduced.
