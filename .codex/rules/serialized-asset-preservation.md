# Serialized Asset Preservation

- Treat readable serialized JSON and structured-text assets as authoritative source
  files.
- Clone or faithfully reconstruct available source assets before considering a
  replacement.
- Preserve hierarchy, ordering, names, properties, references, bindings, and
  unresolved serialized data when safe.
- Preserve IDs by default; regenerate only for target validity or confirmed
  collisions, then remap and report every reference.
- Do not invent simplified assets, discard unknown properties, or remove custom data
  without evidence.
- Preserve unknown enums, components, properties, and bindings unless repository
  evidence proves they are structurally invalid in the target.
- Follow `.codex/references/inheritance/serialized-assets.md`.
