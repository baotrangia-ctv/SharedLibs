---
name: giftcode-source-to-shared
description: Inherit Giftcode's authoritative redeem, reuse, mail-delivery, and persistence core from Steal A Pet into SharedLibs while isolating source-only UI and eligibility systems.
---

# Purpose

Route source-to-SharedLibs Giftcode inheritance. The reusable surface is the
`MailConfigs` + `MailsManager` redeem contract; `HudGiftCode`, `GiftCode.ui`,
source prompts, rebirth checks, and pet-slot checks are consumer integrations.

# Workflow

1. Validate roots through `source-to-shared-router` and require the module intake
   record before any non-report edit.
2. Select the latest active flow from source call-sites:
   `HudGiftCode.ApplyGiftCode` -> `MailConfigs.GetGiftIdByCode` ->
   `MailsManager.RequestReceiveMail` -> `CheckRedeemGiftCode` ->
   `ProcessReceiveMail`.
3. Inventory config schema, used-code persistence, mail lifecycle, status results,
   UI/asset registration, localization, and all transitive Manager/utility
   dependencies. Treat `PlayerGiftCode` as legacy/unused unless a new call-site
   proves otherwise.
4. Preserve Stage A behavior and data contracts before adapting to target string
   definitions and structured rewards. Reuse target `DataUtils`,
   `DatabaseController`, `MailsDefinitions`, and `StatusCodes`.
5. Keep `Request -> Check -> Process` explicit. Checks must not mutate used-code
   or mail state.
6. Do not copy source production gift rows, rebirth/pet Managers, prompt routing,
   or editor-owned Giftcode UI into the core package without explicit consumer
   scope and current target registration evidence.
7. Run the applicable `review-inherited-module` sections: Clone Fidelity,
   Standalone Portability, Feature Completeness, Folder Architecture, Serialized
   Asset Fidelity, Asset Dependency Closure, Active API Surface, Utility Reuse,
   Static Definitions, Request-Check-Process, and Data Lifecycle.
8. Run full FC validation after every `.fcg` edit. Use the configured compiler;
   if it rejects `-agent`/`-session`, use the documented legacy fallback and
   report it. Runtime Studio verification is separate.

# Required outputs

- `reports/inheritance/giftcode/00-intake.md`
- `feature-surface-inventory.md`, `inheritance-report.md`, and
  `portability-manifest.md`
- the applicable `reports/reviews/giftcode/*.md` files
- the paired `giftcode-shared-to-consumer` skill after completion

# Allowed scope

Read the validated source and SharedLibs repositories. Modify only the validated
SharedLibs target plus inheritance reports and the two module workflow skills.

# Stop conditions

Stop for invalid roots, incomplete intake, missing active source evidence, or a
structurally invalid mandatory target dependency. Missing MCP blocks only an
editor/runtime stage unless all strict blocker conditions are met.

