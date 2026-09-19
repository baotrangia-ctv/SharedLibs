# Adapter-Last

- Do not introduce an adapter merely to separate code or mirror a source-project boundary.
- Prefer a direct reusable implementation when behavior is stable and game-independent.
- Prefer a simple interface or callback when only one behavior varies.
- Use an adapter only when an external contract, incompatible representation, platform boundary, or multiple concrete integrations require translation.
- Document every adapter's varying behavior, translated contract, consumers, and why a direct implementation or simple interface is insufficient.
- Remove pass-through adapters that add no validation, translation, lifecycle ownership, or compatibility value.
