# Standalone portability review

Status: `Consumer adaptation required`.

| Dependency | Required | Handling | Consumer responsibility |
| --- | --- | --- | --- |
| `LeaderboardMockScoreProvider` | Yes for current build | Isolated mock source | Replace its two provider functions with real score access later |
| Leaderboard HUD asset | Yes | Import/adapt in target Studio | None after target asset stage completes |
| Player HUD script attachment | Yes | Target integration point | Attach HUD graph to player/runtime entry point |
| UI control script attachment | Yes | Target integration point | Attach target leaderboard control to imported UI |
| Persistent database writes | No for current scope | Deferred | Add only when real scoring requires publishing scores |
| Source Wallet/Collection/Profile Managers | No | Excluded behind mock seam | Real provider may map equivalent consumer APIs |

The Manager/config/mock subset is standalone and compiles. The complete feature is not
standalone until its HUD and runtime attachments are registered. Runtime verification:
`Not performed`.
