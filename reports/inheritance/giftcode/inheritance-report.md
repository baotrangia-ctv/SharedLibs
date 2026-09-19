# Giftcode Inheritance Report

Date: 2026-09-19
Module: `giftcode`
Route: `source-to-shared-router`

## Validated roots

- Source: `D:\Craftland\StealAPet` — configured `read-only`, repository marker
  `.git`, source `AGENTS.md` present.
- Target: `D:\Craftland\_Libs\SharedLibs` — configured `read-write`, repository
  marker `.git`, target `AGENTS.md` and `.agent/` present.
- Roots are distinct and the intake gate exists at
  `reports/inheritance/giftcode/00-intake.md`.
- Source worktree already contained a modified
  `ProjectSettings/SceneScreenshot.png`; it was not touched.

## Latest active implementation

The active redeem path is:

`HudGiftCode.ApplyGiftCode` -> `MailConfigs.GetGiftIdByCode` ->
`MailsManager.RequestReceiveMail` -> `CheckConditionReceiveMail` ->
`CheckRedeemGiftCode` -> `ProcessReceiveMail`.

This is verified from `Assets/Scripts/HUDs/HudGiftCode.fcg:67-84` and
`Assets/Scripts/Manager/MailsManager.fcg:424-498, 777-807`. The
`PlayerGiftCode` cache graph has no active method call-sites in the validated
source tree and was classified as source-specific/unused for this path.

## Implemented target changes

- Extended `Assets/Scripts/Managers/MailsManager.fcg` to route configured mail
  validation through `CheckRedeemGiftCode`.
- Added source-aligned start/end checks using the target's epoch-second config
  contract, preserving the target's existing exact-timestamp window behavior.
- Added `GetPlayerUsedGiftcodes` with a cloned return value so consumers cannot
  mutate Manager-owned state directly.
- Preserved the target's generic structured reward representation and existing
  `MailsDefinitions`, `StatusCodes`, `DataUtils`, database, and CSV registration
  contracts.

## Stage status

| Stage | Status | Notes |
| --- | --- | --- |
| Source discovery | Complete | Source docs, scripts, CSV, UI, metadata, registrations, and call-sites inspected. |
| Active API analysis | Complete | Active Manager path separated from unused player cache and UI-only paths. |
| Manager clone | Complete | Redeem validation, used-code state, mail mutation, and persistence remain in the target Manager. |
| Config and CSV clone | Complete with documented adaptation | Target `Gifts.csv` is a generic structured-reward fixture rather than source production rows. |
| Data lifecycle clone | Complete | Target Mails load/save/ready/clear path already existed and remains authoritative. |
| Serialized asset clone | Not applicable to core scope | Source `GiftCode.ui` is recorded as a consumer integration point; it was not copied into core. |
| Dependency closure | Complete with isolated source dependencies | Source-only rebirth, pet-slot, prompt, tracking, and editor registration dependencies are documented. |
| Shared refactor | Complete | Minimal additions reuse the existing target contract and utilities. |
| Runtime verification | Runtime verification pending | No live Craftland Studio session was used. |

## Fidelity and portability

Faithful Clone Mode result: `Source-compatible` for the authoritative core,
`Not yet standalone` only for the omitted player-facing integrations.

Standalone portability: `Standalone with optional integrations`. The core has no
mandatory source-project Manager dependency after adaptation; consumer work is
required for UI, feedback, reward claiming, and optional rebirth/pet rules.

## Validation

- Local full FC compile passed with exit code `0` using the configured legacy
  compiler at `C:\Users\giabao.tran\AppData\Local\Programs\Craftland Studio\resources\LocalData\Utilities\UGCLanguage\release\fccompile_external.exe`.
- The compiler rejected the newer `-agent` and `-session` flags, so the required
  legacy fallback was used without those flags.
- Compile emitted pre-existing deprecation warnings in
  `Assets/Scripts/HUDs/HudControls.fcg`; no Giftcode error was reported.
- Craftland Studio runtime/editor verification was not performed.
- The bundled skill validator was attempted for both generated skills but could
  not start because the environment lacks Python's `yaml` module; frontmatter,
  naming, placeholder, path, and diff checks passed through repository commands.
