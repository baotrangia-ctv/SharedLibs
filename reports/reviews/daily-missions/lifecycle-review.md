# Data lifecycle review — Daily Missions

Status: **Pass for static review; runtime persistence pending**.

The manager registers a dedicated database, initializes per-player maps on join, loads with retry, reconstructs persisted mission state, marks the database ready, saves all state fields, marks saved state on success, waits for the target save convention, and clears in-memory state. Date changes reset mission progress, claims, and milestone points. A Studio playtest is still required to verify the target runtime's actual database event ordering and save/reload behavior.

