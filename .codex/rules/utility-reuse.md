# Utility Reuse

- Before writing parsing, serialization, structured-data conversion, JSON-like handling, default-value, migration, list, map, split, join, or primitive collection helpers:
  1. inspect `Assets/Scripts/Utils/DataUtils.fcg`;
  2. inspect other relevant files under `Assets/Scripts/Utils/`;
  3. compare behavior and encoding compatibility;
  4. reuse an existing API when compatible.
- Extend an existing utility only when the new behavior is broadly reusable.
- Keep a helper feature-local only when its behavior is feature-specific.
- Do not duplicate a `DataUtils` function under another name, create a feature-specific wrapper without a concrete need, copy an equivalent source utility, or place generic conversion logic inside a Manager.
- When a legacy encoding must be preserved, isolate compatibility conversion, use `DataUtils` for the canonical format, and document the migration boundary.
- Run `review-utility-reuse` when a feature parses, serializes, converts, or stores structured data.
- When a serialized asset references a source-wide utility, inspect the complete
  utility and classify the APIs it actually uses. Reuse, copy the smallest reusable
  surface, extract broadly reusable behavior, or isolate source-specific behavior.
- Do not block an entire feature merely because a referenced utility has multiple
  dependencies.
