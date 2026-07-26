# Load and Save Lifecycle Checklist

Use this reference only when the module reads or writes persistence, registers readiness, or saves on disconnect or shutdown.

Review:

- Player join entry point
- Database registration
- Load ordering across managers
- Default data creation timing
- Async callbacks that may finish after readiness changes
- Database-ready signaling
- Feature initialization that depends on loaded state
- Partial load failure handling
- Save ordering
- Duplicate save protection
- Player quit and server shutdown behavior
- Schema compatibility assumptions
- Save timeout or retry behavior

Flag any case where another system can consume incomplete state after a ready signal.
