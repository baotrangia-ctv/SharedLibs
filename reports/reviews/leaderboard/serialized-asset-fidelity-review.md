# Serialized asset fidelity review

Status: `Missing` — failed for the current serialized-asset stage.

- Source: `Assets/HUDs/Leaderboard.ui`
- Source file ID: `t2tdftm3e8h-mgqeyw21-b1bw8lyztw`
- Source SHA-256:
  `85C140389F42B65A91ADDFCE35FA0053AC5DB9C3A7BF750237280AF681E773BF`
- Source size: 291,380 bytes
- Source structure: 89 entities; 1 root, 16 empty, 19 image, 31 text, 7
  button, 3 layout, 1 scroll view, and 11 profile entities.
- Expected scope adaptation after faithful import: remove `WealthButton`,
  `LikeButton`, and inactive `TabsRegion`; replace only the root
  `CustomUIUtils.fcg` attachment.
- Target asset: absent because the connected Studio context cannot resolve the
  validated target project.

The source is readable and must not be replaced with a simplified UI. Runtime status:
`Not performed`.
