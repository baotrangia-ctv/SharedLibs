# Utility Decision Checklist

For each helper, compare:

- input and output types
- delimiter or encoding format
- nil, empty, and default handling
- parsing failure behavior
- collection mutation or cloning behavior
- ordering guarantees
- persistence compatibility
- current call sites

Choose:

- `Reuse existing utility` when behavior is compatible.
- `Extend existing utility` when the behavior is broadly reusable and backward compatible.
- `Keep feature-local` when the logic expresses feature business rules.
- `Remove duplicate` when an equivalent utility already exists.
- `Needs compatibility wrapper` only when a legacy representation must be translated.

Reject wrappers that merely rename or pass through an existing utility.
