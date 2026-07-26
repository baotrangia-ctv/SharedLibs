# Production Placeholder Cleanup

Do not copy SharedLibs demo or placeholder handlers into production.

Inspect and remove or replace:

- mock reward handlers
- notification-only reward flows when real delivery is required
- mock persistence
- placeholder UI behavior
- unused provider or adapter classes

Prefer existing consumer services, optional integrations, no-op defaults, callbacks, or a simple interface. Retain an adapter only when it translates a real contract or representation boundary.

Document files omitted, removed, adapted, and justified.
