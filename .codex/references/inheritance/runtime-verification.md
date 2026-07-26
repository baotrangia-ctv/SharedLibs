# Runtime Verification

Track runtime verification separately from serialized clone fidelity and standalone
portability.

## Serialized Clone Status

Confirm source discovery, active-version selection, asset fidelity, dependency
closure, script/config/CSV/API/lifecycle fidelity, and integration-point
classification.

Use one status:

- `Complete`
- `Complete with documented unresolved runtime gaps`
- `Incomplete`
- `Blocked by strict MCP stop condition`

## Runtime Verification Status

When a supported live Studio session is available, verify project open, compile,
asset load, UI render, events, actions, persistence, and runtime errors.

Use one status:

- `Passed`
- `Failed`
- `Partially verified`
- `Not performed`
- `Needs Studio verification`

Never infer runtime success from serialized fidelity. A valid completion statement is:

```text
Serialized clone completed.
Runtime Studio verification was not performed.
```

Unavailable runtime verification alone does not block serialized clone completion.
Use `.codex/references/inheritance/standalone-portability.md` for the independent
portability status; do not infer it from either clone or runtime status.
