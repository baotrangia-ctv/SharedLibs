# Active API review

| API | Version | Call sites | Status | Inheritance decision |
| --- | --- | --- | --- | --- |
| `LeaderboardManager.GetLeaderboardType` | Current persistent/global leaderboard | `HudLeaderboard.UpdateLeaderboardLayout` | Latest active | Inherit as `RequestLeaderboard` with explicit state output |
| `LeaderboardManager.LoadLeaderboard` | Current database loader | `GetLeaderboardType`, `CheckUpdateLeaderboardScore` | Latest active | Preserve load/cache flow; substitute mock provider |
| `LeaderboardManager.SavePlayerLeaderboard` | Current database writer | quit-save event | Active | Defer because the user explicitly requested mock scores |
| `RankingManager.UpdateRanking` in `GlobalLeaderboard.fcg` | In-session ranking | `PlayerBase` attachment/runtime | Active | Exclude; separate non-HUD gameplay ranking |
| `Wealth` and `Like` score branches | Current HUD tabs | HUD and `CustomUIUtils` | Active | Exclude by explicit two-type scope |

Finding: the source has no V2/V3 or deprecated replacement for the selected persistent
HUD flow. The similarly named `GlobalLeaderboard.fcg` is not an older API; it owns a
different in-session ranking flow. Evidence: `Verified from source script`.
