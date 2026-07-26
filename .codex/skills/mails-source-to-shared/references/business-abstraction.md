# Business Abstraction

Separate:

1. Generic feature mechanics
2. Required infrastructure
3. Steal A Pet-specific business rules
4. UI dependencies
5. Data persistence dependencies
6. Config dependencies
7. Optional integrations

For each removed or abstracted behavior, document:

- original behavior
- why it is project-specific
- generic handling
- consumer integration point
- whether the integration is direct, optional, no-op, callback-driven, or interface-based
- adapter justification when an adapter is retained

Apply Adapter-Last. Do not create an adapter or demo provider solely to preserve the source project's class boundaries.
