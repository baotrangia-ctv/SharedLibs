# Manager Organization

- Every generated primary Manager file should use clearly separated sections in this order where applicable:
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
- At minimum, persistent Managers must clearly distinguish:
  - `Load Data`
  - `Save Data`
  - `Actions`
- `Load Data` should contain database registration, loading, default-data creation, deserialization, cache initialization, migration handling, and database-ready signaling.
- `Save Data` should contain serialization, save payload construction, save calls, dirty-state handling, disconnect save behavior, player quit behavior, and server shutdown behavior.
- `Actions` should contain user or system operations and preserve:
  - `Request -> Check -> Process`
- Do not scatter load, save, and action methods throughout the file without clear grouping.
- Do not place generic parsing, serialization, or conversion helpers in the Manager when `DataUtils` or another shared utility is compatible.
- Keep small private implementation constants local, but move reused fields, statuses, result codes, and action identifiers to a cohesive feature definition file.
