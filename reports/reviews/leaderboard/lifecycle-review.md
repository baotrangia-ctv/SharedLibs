# Data lifecycle review

Trigger: runtime cache exists; persistence does not.

- Cache initialization is idempotent in `LeaderboardManager.Init`.
- Global leaderboard rows are keyed only by supported type and contain no per-player
  account data in the mock provider.
- Current-player details are resolved per request, preventing the first requesting
  player from leaking into the global cache.
- `ReloadLeaderboard` invalidates rows, state, and loaded flag together.
- No disconnect, reconnect, save, quit, or shutdown path is required for the mock
  cache.
- Future real providers may preserve global row caching but must resolve player rank
  per request and define refresh/expiry behavior.

Finding: no persistence divergence or reconnect duplication exists in the mock stage.
