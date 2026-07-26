# Repository Definition Search

Before MCP, search the validated source and shared repositories for:

- custom enum and component definitions
- component registration and generated metadata
- script references, attached scripts, utility scripts, and consumers
- property IDs, enum IDs, entity IDs, and call sites
- related serialized assets and alternate binding data
- asset import metadata, local files, textures, and target equivalents

Do not infer editor-only ownership from a `CustomComponent` name or generated ID.

For every custom identifier, report:

| Identifier | Definition path | Usage paths | Definition found | Preserve unchanged | Adaptation required | Evidence |
| --- | --- | --- | --- | --- | --- | --- |

Search by exact identifier, serialized value, property key, file name, asset ID, and
consumer API. Record repository-relative paths and searches performed. An absent
human-readable label does not prove the serialized value is invalid.
