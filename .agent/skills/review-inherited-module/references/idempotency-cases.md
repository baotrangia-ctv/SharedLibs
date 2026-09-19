# Idempotency Cases Checklist

Use this reference only when the module grants one-time rewards, applies purchases, changes progression, or can receive duplicate calls.

Check:

- Duplicate `Request` calls
- Retry after partial failure
- Repeated button taps
- Replayed external messages
- Duplicate reward or purchase processing
- Repeated claim or completion events
- Guard conditions for once-only actions

Flag any case where duplicate processing can produce duplicate state changes or partial mutation.
