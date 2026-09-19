# Giftcode Portability Manifest

## Status

`Standalone with optional integrations` for the core redeem/mail contract.
Consumer adaptation is required for player UI, prompts, reward application, and
optional source-specific eligibility rules.

## Public contract

### Config

- `MailConfigs.GetGiftIdByCode(code)` resolves a configured code to an ID.
- `MailConfigs.GetGiftCodeById(id)` returns the configured code.
- `MailConfigs.GetGiftStartById(id)`, `GetGiftEndById(id)`, and
  `GetGiftReuseById(id)` expose redeem-window and reuse policy.
- `MailConfigs.GetGiftRewardsById(id)` returns the target structured reward list.
- `MailConfigs.IsGiftWindowValid(id, timestamp)` remains available for callers
  that already use the target config contract.

### Manager

- `MailsManager.RequestReceiveMail(payload, out statusCode)` is the public
  redeem/mail entry point. For a configured gift, the payload must include
  `PlayerUID`, `IsConfigMail = true`, and `MailId`.
- `MailsManager.CheckRedeemGiftCode(playerUID, giftId, out statusCode)` performs
  read-only validity, time-window, reuse, and used-code checks.
- `MailsManager.GetPlayerUsedGiftcodes(playerUID)` returns a cloned snapshot.
- `MailsManager.HasUsedGiftcode(...)` and `AddPlayerUsedGiftcode(...)` retain the
  source one-time/reusable semantics.

## Required consumer adapters

- Map raw user text to an ID with `MailConfigs.GetGiftIdByCode`; the source HUD
  uppercases input before lookup, so consumers should preserve that behavior.
- Display `StatusCodes.STATUS_GIFT_CODE_INVALID`, `..._HAS_USE`,
  `..._EXPIRED`, `...PLAYER_FULL_MAIL`, or `...PLAYER_DISCONNECT` as appropriate.
- Provide optional UI/event feedback after a successful request.
- Provide reward claiming/application for the structured mail payload.
- Add an explicit eligibility provider if the consumer needs source behavior such
  as rebirth-level gating or pet-slot validation.
- Register and wire a consumer-owned Giftcode UI if player-facing code entry is
  required; the source `GiftCode.ui` is not part of this core package.

## Persistence and rollback

- The core uses the existing `Mails` database registration and persists used gift
  IDs under `GiftCodeHasUse/OwnGiftCodeHasUse` plus current/pending mail data.
- Disable the UI caller first to roll back presentation without changing the
  persisted contract. Do not remove the used-code fields without a migration.

