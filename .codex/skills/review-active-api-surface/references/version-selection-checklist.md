# Version Selection Checklist

Use this reference when multiple implementations of the same user flow exist.

Check:

- current HUD call sites
- current Manager call sites
- event registration
- config references
- feature flags
- runtime entry points
- tests or comments indicating active replacement

Default rule:

- inherit only the latest active implementation

Do not inherit every historical version by default.
