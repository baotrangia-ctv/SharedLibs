# Reconnect Cases Checklist

Use this reference only when the feature tracks per-player runtime state or reacts to disconnect and reconnect.

Review:

- Disconnect during load
- Reconnect before save finishes
- Repeated join or initialization callbacks
- Duplicate runtime initialization
- Stale session data reuse
- Restored Manager state
- Restored UI state if the UI depends on cached runtime state
- Pending transaction state
- Multiple active session assumptions

Flag any case where reconnect can duplicate processing or skip required cleanup.
