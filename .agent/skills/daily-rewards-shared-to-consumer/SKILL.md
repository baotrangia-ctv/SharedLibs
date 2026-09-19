---
name: daily-rewards-shared-to-consumer
description: Transfer the SharedLibs Daily Rewards package into a consumer while preserving its public contract, persistence, mail claim flow, and consumer integration boundaries.
---

# Purpose

Treat SharedLibs as the authoritative read-only package for downstream
consumers. Do not require the original source project.

# Required workflow

1. Inspect the SharedLibs Daily Rewards skill, reports, FC scripts, CSVs, and
   generated registration symbols.
2. Validate the consumer root and search consumer definitions for equivalent
   mail, database, time, reward, UI, and user-type contracts.
3. Transfer the smallest complete dependency closure and preserve compatible
   serialized values and IDs.
4. Map only consumer-specific adapters: user type/rebirth provider, claim UI,
   prompt/feedback, and reward presentation.
5. Preserve `Request -> Check -> Process`, database readiness, reconnect/load,
   save/quit, and seven-day streak behavior.
6. Run serialized-asset, dependency-closure, portability, architecture,
   utility/static-definition, action, lifecycle, and production reviews.
7. Record integration and rollback evidence separately from SharedLibs clone
   fidelity and runtime verification.

# Prohibited shortcuts

Do not reimplement the module from memory, edit generated EditorGen files, or
replace an available SharedLibs CSV/config with a simplified placeholder.

