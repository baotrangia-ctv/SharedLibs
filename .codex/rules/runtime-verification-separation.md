# Runtime Verification Separation

- Track serialized clone fidelity independently from live runtime verification.
- Track standalone portability independently from both clone fidelity and runtime
  verification.
- A source clone may complete from repository evidence while Studio runtime
  verification remains `Not performed` or `Needs Studio verification`.
- Do not claim compile, asset load, rendering, event, persistence, action, or runtime
  success without performing the corresponding live validation.
- Do not block filesystem inheritance solely because live Studio verification is
  unavailable.
- Follow `.codex/references/inheritance/runtime-verification.md`.
