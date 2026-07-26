# Layer-Based File Placement

- Organize generated files by architectural responsibility, not in one mixed feature folder.
- Use this default mapping:
  - authoritative feature logic: `Assets/Scripts/Managers/`
  - HUD behavior: `Assets/Scripts/HUDs/`
  - UI assets: `Assets/HUDs/`
  - config and CSV readers: `Assets/Scripts/Configs/`
  - generic utilities: `Assets/Scripts/Utils/`
  - execution and review reports: `reports/`
  - skill references: `.codex/skills/[skill]/references/`
  - framework-wide inheritance references: `.codex/references/inheritance/`
- Include the feature and responsibility in filenames, such as
  `[Module]Manager.fcg`, `[Module]HUD.fcg`, `[Module]Configs.fcg`, and
  `[Module]Definitions.fcg`.
- Reject mixed folders such as `Assets/Scripts/[Module]/` containing Manager, HUD,
  Config, and Utils files.
- Allow a feature subfolder only inside one architectural layer when that layer has many related files, the project uses that convention consistently, responsibilities remain unmixed, and the reason is documented.
- Run `review-folder-architecture` before completing every source-to-shared inheritance.
