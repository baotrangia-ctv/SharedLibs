# Static definitions review

| Definition group | Call sites | Recommendation | Compatibility |
| --- | --- | --- | --- |
| Income/Collection type IDs | Manager, provider, future HUD | Move to feature definitions | Values preserve source names |
| Loading/success/empty/error states | Manager, provider, future HUD | Move to feature definitions | New explicit UI contract |
| Row and player-summary indices | Provider, future HUD | Move to feature definitions | Preserves source list positions |
| Mock delay | Mock provider only | Keep private in Manager-equivalent provider | No public compatibility impact |
| Mock numeric rows | Mock provider only | Keep local | Replaced with real scores later |

The cohesive placement is `Assets/Scripts/Configs/LeaderboardDefinitions.fcg`; no
one-file-per-constant fragmentation was introduced.
