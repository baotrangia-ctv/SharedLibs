# Giftcode Static Definitions Review

Status: `Retain existing target definitions`.

- `MailsDefinitions.fcg` owns persistence keys, mail field keys, CSV columns,
  database type, and mail limits shared by Config, Manager, and HUD.
- `StatusCodes.fcg` owns portable result strings including invalid, used,
  expired, full-mail, disconnect, and no-error outcomes.
- No new duplicate Giftcode constants file was needed.
- Source-only typed enums (`RequestParameter`, `DataKey`, `CustomStatusCode`) are
  not re-created in SharedLibs; the target string contract is already active.

