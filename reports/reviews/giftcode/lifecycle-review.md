# Giftcode Data Lifecycle Review

Status: `Complete with documented runtime verification gap`.

- `OnAwake` initializes Mails state once and registers the `Mails` database.
- `OnDatabaseLoad` initializes per-player maps, loads used gift IDs and current/
  pending mails, combines them, flushes pending data, then marks the database
  ready.
- `OnDatabaseSave` writes used IDs and current mail data, marks saved, waits, and
  clears UUID-keyed runtime caches.
- Reconnect rebuilds used-code and mail state from persistence through the same
  load path; no separate Giftcode cache is introduced.
- Runtime Studio verification of load/save callbacks and real persistence was not
  performed.

Known inherited limitation: target save helpers do not expose write status to the
caller before `SetDatabaseSaved`; this pre-existing Mails behavior is recorded for
follow-up and was not changed in this core inheritance.

