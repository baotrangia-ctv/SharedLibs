# Stage-Based Completion

Track each stage independently:

1. Source discovery
2. Active API analysis
3. Manager clone
4. Config and CSV clone
5. Data lifecycle clone
6. Serialized asset clone
7. Dependency closure
8. Shared refactor
9. Runtime verification

Use one status per stage:

- `Complete`
- `Complete with unresolved bindings`
- `Partially complete`
- `Blocked`
- `Not applicable`
- `Runtime verification pending`

For the Runtime verification stage, this status reports stage progress only. Also
report the independent runtime result from `runtime-verification.md`; do not use a
stage status as the runtime result.

Complete every safe independent stage. Standalone portability is a separate
assessment, not an additional stage. A blocked asset or runtime stage and a partial
portability assessment do not erase completed Manager, config, CSV, lifecycle, or
reporting work.

Do not report `No files were modified` when safe outputs can be created. Block the
whole task only when writing any useful target output would be destructive or
misleading. Otherwise report the affected stage, completed stages, safe files, and
remaining work.
