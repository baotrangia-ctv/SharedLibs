# Mails Primary Flow Validation

Validate this primary flow without requiring standalone demo service classes:

```text
Open Mails HUD
    ->
Display available mails
    ->
Select or inspect a mail
    ->
Claim through Manager Request
    ->
Refresh claimed state
    ->
Display success or failure feedback
```

Use existing SharedLibs services first. Make optional integrations no-op or callback-driven when safe. Create a demo-specific source file only when all Demo-Last conditions are satisfied.

When a readable serialized HUD asset exists, preserve it and run
`review-serialized-asset-fidelity`; do not substitute a generic HUD. If no serialized
asset exists, use a minimal fallback only after repository evidence is exhausted and
record exact asset parity as unavailable. Track live rendering and runtime-only
bindings separately as `Needs Studio verification`.
