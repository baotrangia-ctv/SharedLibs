# Cache Invariants Checklist

Use this reference only when the module keeps runtime cache, ownership maps, identifiers, or in-memory mirrors of persistent state.

Review:

- Cache initialization source of truth
- Cache and database consistency
- Ownership boundaries between managers
- Duplicate identifiers
- Stale or partially initialized cache state
- Invalid direct mutation from unrelated systems
- Cache cleanup on player quit or teardown
- Cache rebuild behavior after reconnect or reload

Look for cases where cache updates and persistent updates can diverge.
