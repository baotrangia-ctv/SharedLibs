# Static Definitions Review

**Result:** Retain feature definitions.

`DailyRewardsDefinitions.fcg` owns persistence keys, user types, status strings,
CSV column indexes, and payload names. This prevents duplicated literals across
Manager/Config while keeping feature-private values out of generic `StatusCodes`.

Target mail status values remain in `StatusCodes.fcg` and are reused unchanged.
Persisted field names retain source values. The database name/key are explicit
SharedLibs portability adaptations and are not silently merged into the mail or
generic database definitions.

