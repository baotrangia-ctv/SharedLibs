# Folder architecture review — Daily Missions

Status: **Pass**.

The manager is under `Assets/Scripts/Managers`, configuration readers under `Assets/Scripts/Configs`, constants under `Assets/Scripts/Consts`, and source data under `Assets/CSV`. No source-project `Manager`/`HUDs` folder layout was copied into SharedLibs. The dedicated manager avoids extending the unrelated target Daily Rewards manager and keeps reward/provider adapters out of the reusable core.

