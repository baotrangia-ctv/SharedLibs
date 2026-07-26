# Module Shared-to-Consumer Skill Template

Future `[module]-shared-to-consumer` skills must:

1. Validate SharedLibs and consumer roots, treat SharedLibs as workflow read-only,
   and require the consumer to be read-write.
2. Inspect SharedLibs files directly without requiring the original source project.
3. Always load common repository-first, MCP-last, and runtime-verification
   references plus preserve-first, definition-search, stage-completion, portability,
   and explicit-blocker references. Load serialized-asset and dependency-closure
   references when those artifact types are present.
4. Select the latest active public contract and required portability artifacts.
5. Search SharedLibs and consumer definitions, preserve compatible serialized values,
   and remap only proven incompatibilities.
6. Build and transfer the smallest complete dependency closure.
7. Map only consumer integration points and reuse compatible consumer utilities.
8. Preserve consumer folder conventions where compatible with layer responsibilities.
9. Avoid deprecated, compatibility-only, mock, placeholder, and demo artifacts unless
   active compatibility or validation evidence requires them.
10. Apply Adapter-Last and preserve Request -> Check -> Process and lifecycle
    behavior.
11. Invoke `review-serialized-asset-fidelity` and
    `review-asset-dependency-closure` when applicable, plus focused architecture and
    integration reviews.
12. Complete every safe independent stage and assess consumer portability separately
    from transfer fidelity.
13. Generate stage-based consumer integration and rollback reports with exact MCP
    blockers.
14. Report filesystem integration, portability, and runtime verification separately.

Never create a simplified replacement when an available shared serialized asset can
be transferred faithfully. Missing MCP alone is not a stop condition.
