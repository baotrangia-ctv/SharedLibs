# Manager Organization Checklist

Use this reference when the inherited feature has a primary Manager.

Verify the generated Manager file clearly separates, where applicable:

1. Constants and Types
2. Runtime State and Cache
3. Initialization
4. Load Data
5. Save Data
6. Query APIs
7. Actions
8. Events and Callbacks
9. Internal Helpers
10. Optional Integrations

At minimum for persistent Managers, confirm:

- `Load Data`
- `Save Data`
- `Actions`

are clearly grouped and not scattered.

Confirm generic parsing and serialization are not embedded in the Manager when existing Utils are compatible. Confirm reused fields, statuses, results, and actions are centralized without moving truly private constants out of the Manager.
