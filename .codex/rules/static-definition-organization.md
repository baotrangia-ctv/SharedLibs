# Static Definition Organization

- Centralize reused field keys, config identifiers, feature states, result codes, and action identifiers in a small number of responsibility-owned static definition files.
- Use this decision order:
  - one function: local constant;
  - one Manager only: private Manager constant;
  - Config and Manager: static Config or Definitions file;
  - Manager and HUD: public feature definitions;
  - multiple modules: shared definitions or a broadly reusable utility.
- Place config fields, serialized keys, CSV columns, and config defaults under `Assets/Scripts/Configs/`.
- Place feature statuses, result codes, and reused action identifiers in a grouped feature definition file, normally under `Assets/Scripts/Configs/`.
- Keep private implementation details in the Manager when centralizing them would increase coupling.
- Prefer one cohesive file such as `[Module]Definitions.fcg` over one file per
  constant.
- Do not place feature-specific constants in `Assets/Scripts/Utils/`.
- Run `review-static-definitions` when repeated fields, statuses, action names, config keys, state identifiers, or result codes are introduced.
