# Dependency Closure

- Identify the smallest complete transitive dependency closure for every inherited
  module and consumer integration.
- Classify every script, asset, config, CSV, localization, component, event, service,
  and engine-library dependency using
  `.codex/references/inheritance/dependency-closure.md`.
- Do not copy a root with broken references, copy unrelated directories, silently
  replace missing files, duplicate target utilities, or localize engine references
  without evidence.
- Report missing and unresolved dependencies and continue independent work when safe.
