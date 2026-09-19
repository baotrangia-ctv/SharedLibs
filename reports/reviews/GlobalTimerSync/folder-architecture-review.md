# GlobalTimerSync Folder Architecture Review

**Result:** `Retain`

| Responsibility | Current path | Decision | Evidence |
| --- | --- | --- | --- |
| Shared timing algorithm | `Assets/Scripts/Utils/GlobalTimerSync.fcg` | Retain | Generic utility with no player-state ownership |
| Preserved time anchor surface | `Assets/Scripts/Utils/TimeManager.fcg` | Retain | Generic engine-time utility; unrelated source Manager dependencies excluded |
| Public anchor definitions | `Assets/Scripts/Configs/GlobalTimerSyncDefinitions.fcg` | Retain | Folder mapping places feature contract/config definitions under Configs |
| Existing daily-time compatibility API | `Assets/Scripts/Utils/DailyRewardsTime.fcg` | Retain | Existing consumer API preserved and delegates to canonical utility |
| Inheritance evidence | `reports/inheritance/GlobalTimerSync/` | Retain | Router-required report location |
| Review evidence | `reports/reviews/GlobalTimerSync/` | Retain | Review-required report location |
| Paired module skills | `.agent/skills/GlobalTimerSync-*` | Retain | Auto-pair skill-generation output |

No mixed feature folder, HUD/config/Manager crossing, copied source directory, or
feature subfolder exception was introduced.
