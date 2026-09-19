# Known Incident Patterns

Use this reference only when the requested change affects a previously unsafe pattern or resembles a known incident class.

Known pattern:

- Async initialization completes after a database-ready flag is set, allowing other systems to consume incomplete player state.

Preventive checks:

- Verify readiness signals occur only after required async initialization completes.
- Verify dependent systems do not unlock behavior solely from an early ready flag.
- Verify retries and delayed callbacks cannot backfill state after consumers have already acted on incomplete data.
