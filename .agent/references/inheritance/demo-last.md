# Demo-Last

- The primary feature flow must be executable or testable without Steal A Pet-specific systems.
- Do not create demo persistence, reward, player, notification, time, analytics, feature-flag, or provider classes by default.
- Before creating a demo-specific source file, confirm all of the following:
  - the primary flow cannot execute or be validated without an implementation;
  - no existing SharedLibs implementation is compatible;
  - an optional integration, no-op, callback, or documentation example is insufficient;
  - the file is small, clearly marked, and required for lifecycle validation.
- A module is not incomplete merely because it has no standalone demo handlers.
- Review and report `Unnecessary Demo Artifacts`: demo files that duplicate shared infrastructure, are unused by the primary flow, exist only for an outdated requirement, or increase integration complexity.
