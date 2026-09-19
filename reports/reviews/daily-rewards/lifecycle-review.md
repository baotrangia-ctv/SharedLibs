# Data Lifecycle Review

**Result:** Pass with live reconnect verification pending.

1. `OnAwake` initializes maps and registers the `DailyRewards` database.
2. `OnPlayerJoin` creates defaults.
3. `OnDatabaseLoad` reads `PlayerSave/pDailyRewards`, retries through
   `DatabaseController`, extracts defaults, and marks ready.
4. Runtime refresh computes the GMT day index, increments the streak once per
   day, cleans sentinel zeroes, and maintains claim state.
5. `OnDatabaseSave` serializes fields, writes the same key, marks saved only on
   success, waits for storage completion, and clears cache.
6. `MailsManager` remains the authoritative mail persistence/claim dependency.

The dedicated key avoids collision with the source's combined Activities
record. A downstream consumer must decide whether to merge that state into a
larger player-save schema.

