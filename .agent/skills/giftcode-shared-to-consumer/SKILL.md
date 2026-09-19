---
name: giftcode-shared-to-consumer
description: Integrate the SharedLibs Giftcode core into a consumer project without reading Steal A Pet, preserving redeem validation, one-time persistence, mail lifecycle, and explicit UI/eligibility adapters.
---

# Purpose

Treat the completed SharedLibs Giftcode package, portability manifest, and public
contract as authoritative. This workflow must not read the original source
project.

# Public contract to map

- `MailConfigs.GetGiftIdByCode` and gift metadata getters.
- `MailsManager.RequestReceiveMail(payload, out statusCode)` for configured gifts.
- `MailsManager.CheckRedeemGiftCode` for read-only preflight checks.
- `MailsManager.GetPlayerUsedGiftcodes`, `HasUsedGiftcode`, and
  `AddPlayerUsedGiftcode` for read-only/query or Manager-owned state boundaries.
- Target `MailsDefinitions` field/persistence keys and `StatusCodes` results.

# Workflow

1. Validate SharedLibs and consumer roots through `shared-to-consumer-router` and
   create its consumer intake record before inspecting implementation files.
2. Read `reports/inheritance/giftcode/portability-manifest.md` and the SharedLibs
   Giftcode reports. Do not access Steal A Pet.
3. Inspect the consumer's database, mail/reward claimant, status/notification,
   UI registration, and optional eligibility systems.
4. Transfer the smallest complete dependency closure and preserve the Mails
   persistence keys and target Gift CSV structure.
5. Map raw code input to a gift ID (preserving source uppercase behavior), then
   call `RequestReceiveMail`; never call `ProcessReceiveMail` from UI code.
6. Add consumer adapters only for UI, prompts, reward application, and optional
   rebirth/pet-slot eligibility. Keep checks read-only and mutations Manager-owned.
7. Run serialized-asset, dependency-closure, portability, architecture,
   static-definition, request-check-process, data-lifecycle, and production
   reviews when their surfaces are present.
8. Validate FC compilation and, when consumer UI/editor assets are changed,
   complete Craftland Studio build/log verification separately from filesystem
   fidelity.

# Required consumer outputs

- consumer integration intake record
- integration and rollback reports
- explicit mapping for Giftcode UI, status feedback, reward claiming, and any
  eligibility provider
- runtime verification status independent from serialized portability

# Stop conditions

Stop for invalid consumer paths, missing SharedLibs contract/manifest, or a
mandatory consumer dependency that cannot be safely copied, adapted, or isolated.
Missing MCP blocks only the affected editor/runtime stage unless all strict blocker
conditions are satisfied.

