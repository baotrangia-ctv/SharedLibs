# Folder Mapping

Use this default mapping:

| Responsibility | Required Location |
| --- | --- |
| Authoritative feature logic | `Assets/Scripts/Managers/` |
| UI behavior | `Assets/Scripts/HUDs/` |
| UI assets | `Assets/HUDs/` |
| CSV or config reader | `Assets/Scripts/Configs/` |
| Feature fields, statuses, results, actions, and config definitions | `Assets/Scripts/Configs/` |
| Generic utilities | `Assets/Scripts/Utils/` |
| Execution and review reports | `reports/` |
| Skill references | `.codex/skills/[skill]/references/` |

Reject `Assets/Scripts/[Feature]/` when it mixes Manager, HUD, Config, or Utils responsibilities.

Allow a feature subfolder only inside one layer when the layer has many files, repository convention supports it, responsibilities remain unmixed, and the reason is documented.

Require filenames to identify both feature and responsibility when practical.
