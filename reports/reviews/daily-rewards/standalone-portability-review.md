# Standalone Portability Review

**Result:** Pass with unresolved consumer integration bindings.

| Dependency | Required | Handling |
| --- | --- | --- |
| `DatabaseController` | Yes | Reused target utility and database lifecycle |
| `MailsManager` / `MailConfigs` | Yes | Reused target contract; added daily gift closure/open windows |
| `DataUtils` | Yes | Reused target JSON/list conversion |
| `DailyRewardsTime` | Yes | Extracted source GMT day-index logic |
| `PlayersManager` | No in SharedLibs core | Consumer supplies user type/revival decision |
| `RebirthManager` | No in SharedLibs core | Consumer passes rebirth level |
| `HudActivities` and prompt/effect APIs | No in core | Consumer owns presentation |
| `DailyRewardManager` Lucky Spin | No | Separate adjacent module |
| textures/entities/custom components/enums | No | No core references |

The package can compile and load independently when the existing target mail and
database managers are present. It is not a drop-in UI package; consumer wiring is
required. No exact MCP blocker exists.

