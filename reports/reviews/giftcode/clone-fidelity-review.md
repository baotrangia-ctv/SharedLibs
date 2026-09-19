# Giftcode Clone Fidelity Review

Result: `Pass, source-compatible` for the requested core scope.

## Preserved

- Configured code-to-ID lookup and gift metadata remain in `MailConfigs`.
- The Manager action still follows `RequestReceiveMail` -> condition check ->
  process mutation.
- One-time codes are persisted in the Mails database and reusable codes are not
  appended to the used-code list.
- Current/pending mail loading, ready signaling, save, and cache clearing remain
  in the target Mails Manager.
- Target structured reward data is preserved instead of inventing a second reward
  parser.

## Intentionally changed or isolated

- `CustomStatusCode`/typed source enums became target string contracts in the
  pre-existing SharedLibs Mails module.
- Source day-index validation is represented by target exact epoch-second window
  checks because the target CSV contract stores timestamp values and already
  exposed `IsGiftWindowValid`.
- Rebirth gating, pet-slot checks, prompt dispatch, tracking, and Giftcode HUD
  are consumer/source-specific integration points.
- Source production `giftcode.csv` rows are not copied into the generic target
  fixture.

## Runtime status

Serialized clone completed for core logic. Runtime Studio verification was not
performed. Remaining UI/editor registration work is explicitly outside the core
scope and is covered by the portability and serialized-asset reviews.

