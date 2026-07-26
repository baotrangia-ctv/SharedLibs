# Explicit MCP Blockers

MCP may block the entire inheritance only when all conditions are true:

1. Repository discovery is complete.
2. Required definitions cannot be found.
3. Values cannot safely be preserved.
4. The affected dependency is mandatory.
5. No filesystem copy, adaptation, isolation, or fallback is possible.
6. Writing any useful target output would be destructive or misleading.

Otherwise block only the affected stage and continue safe independent work.

For every MCP blocker, report:

| Field | Required value |
| --- | --- |
| Identifier | Exact ID, path, property, component, enum, or binding |
| Source file | Repository-relative path |
| Target file | Repository-relative path |
| Dependency type | Exact dependency category |
| Repository searches performed | Queries and roots |
| Definition found | Yes or no |
| Safe preservation possible | Yes or no, with evidence |
| Filesystem adaptation possible | Yes or no, with evidence |
| Invalidity reason | Concrete structural failure |
| MCP resolution | Exact information or operation MCP can provide |
| Affected stage | One stage |
| Other stages may continue | Yes or no, with reason |

Do not use vague blockers such as `editor-owned custom dependencies`. Unknown enum
meaning, unknown display names, many dependencies, partial portability, unavailable
runtime verification, or one unresolved optional binding are not full-task blockers.
