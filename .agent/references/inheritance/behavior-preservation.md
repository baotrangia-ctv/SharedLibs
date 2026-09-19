# Behavior Preservation

- Genericization must preserve active source behavior and externally observable
  contracts.
- For each source-specific subsystem, choose and document: keep reusable behavior,
  use a SharedLibs equivalent, add a small interface, add a justified adapter, make
  optional, defer to consumer integration, remove as deprecated, or remove as
  source-only.
- Document affected source behavior, reason, replacement, consumer responsibility,
  and compatibility impact.
- Do not delete active behavior before an equivalent extension path exists.
