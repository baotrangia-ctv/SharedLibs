# Faithful Clone Mode

Faithful Clone Mode captures the active source implementation before standalone
genericization. It may preserve structurally valid source dependencies and serialized
bindings that are not yet portable.

Report any applicable intermediate status:

- `Source-compatible`
- `Not yet standalone`
- `Consumer adaptation required`
- `Runtime verification pending`

A faithful clone is acceptable when active behavior and contracts are captured,
unknown serialized values are preserved safely, dependencies are inventoried, and
portability gaps are explicit. Do not force complete standalone portability in one
execution when doing so would rewrite behavior prematurely or reduce source fidelity.

Clone fidelity and standalone portability are independent dimensions. High clone
fidelity with partial portability is not total inheritance failure.
