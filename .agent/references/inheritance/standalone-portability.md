# Standalone Portability

Evaluate portability separately from faithful clone fidelity.

Clone fidelity asks whether active behavior, serialized assets, APIs, data flows, and
required source dependencies were captured accurately.

Standalone portability asks whether the module can operate without source-project
infrastructure, including source-wide utilities, components, enums, services, and
consumer-specific behavior.

Use one portability status:

- `Standalone`
- `Standalone with optional integrations`
- `Source-compatible only`
- `Consumer adaptation required`
- `Blocked by exact dependency`
- `Runtime verification pending`

`Runtime verification pending` means the portability assessment cannot be finalized
without live evidence; it is not the runtime result. Always report the independent
runtime-verification status from `runtime-verification.md`.

For each remaining dependency, record whether it is required or optional, how it can
be copied, reused, adapted, extracted, isolated, or deferred, and the consumer work
remaining. Partial standalone portability does not fail a faithful clone.
