# Asset dependency closure review

| Referencing artifact | Dependency | Required | Classification | Target handling | Stage |
| --- | --- | --- | --- | --- | --- |
| `Assets/HUDs/Leaderboard.ui` | `Assets/Sprites/Leaderboard/RankNo{1,2,3}.png` | Yes | Exists and can be copied | Import with metadata | Serialized asset clone |
| `Assets/HUDs/Leaderboard.ui` | `Assets/Sprites/Backgrounds/{BG,LabBG,SubTitleBG,TitleBG}.png` | Yes | Exists and can be copied | Import by serialized file IDs | Serialized asset clone |
| `Assets/HUDs/Leaderboard.ui` | `Assets/Sprites/Icons/CloseIcon.png` | Yes | Exists and can be copied | Import by serialized file ID | Serialized asset clone |
| `Assets/HUDs/Leaderboard.ui` | `Assets/Sprites/Shapes/ShadowSquareRounded.png` | Yes | Exists and can be reused | Reuse target matching file ID | Complete |
| `Assets/HUDs/Leaderboard.ui` | `lib://fftextures/WorkshopIconLibrary/T_34_M_WS_ICON_SQUARE.png` | Optional visual | Engine-owned | Preserve URI | Runtime verification |
| `Assets/HUDs/Leaderboard.ui` | `Assets/Scripts/Utils/CustomUIUtils.fcg` | Yes in source | Exists but source-specific | Replace attachment with leaderboard HUD control | Shared refactor |
| `HudLeaderboard.fcg` | `UIUtils.fcg` | Yes in source | Exists but source-specific | Use target-native `GetWidgetFromCustomUI` pattern | Shared refactor |
| `HudLeaderboard.fcg` | `BigNumberHandler.fcg` | Formatting only | Definition can be extracted | Keep the source money-rank conversion feature-local | Shared refactor |

Conclusion: the smallest complete asset set is the HUD, seven missing source-local
textures, one reused target texture, one preserved engine URI, and target HUD/control
scripts. No unrelated sprite directory needs copying. Evidence is `Verified from UI
JSON` and `Verified from asset metadata`.
