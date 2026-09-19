# Giftcode Feature-Surface Inventory

## Scope decision

This inheritance request covers the reusable Giftcode core: config lookup,
authoritative redeem validation, one-time/reusable state, mail delivery, and the
Mails database lifecycle. The source HUD and editor-owned assets are recorded as
consumer integration points, not copied into the core package.

## Active source evidence

| Surface | Source evidence | Classification |
| --- | --- | --- |
| Giftcode config reader | `Assets/Scripts/Configs/MailConfigs.fcg:77-180`, `Assets/CSV/giftcode.csv` | Active; source schema is game-specific. |
| Authoritative redeem flow | `Assets/Scripts/Manager/MailsManager.fcg:424-498`, `:727-807` | Latest active implementation. |
| Used-code persistence | `Assets/Scripts/Manager/MailsManager.fcg:109-165`, `:331-403` | Required lifecycle dependency. |
| Player-facing entry point | `Assets/Scripts/HUDs/HudGiftCode.fcg:67-84` | Consumer integration point; maps code to ID then calls Manager. |
| Legacy player cache | `Assets/Scripts/Player/PlayerGiftCode.fcg:14-212` | No meaningful method call-sites found; source-specific/unused for the active redeem path. |
| Giftcode UI | `Assets/HUDs/GiftCode.ui`, `.meta` | Readable serialized asset; source-specific UI integration. |
| UI routing and registration | `Assets/Scripts/Utils/CustomUIUtils.fcg:560-572`, `ProjectSettings/ResourceRegisteration.asset` | Consumer/editor integration point. |
| Giftcode localization | `Assets/Localization/key.csv` keys `PROMPT_*` and `HUD_GIFTCODE_*` | Consumer presentation dependency. |

Evidence labels: `Verified from source script`, `Verified from CSV`,
`Verified from serialized asset`, `Verified from asset metadata`, and
`Inferred from call-site evidence`.

## Target surface

| Target artifact | Result | Evidence |
| --- | --- | --- |
| `Assets/Scripts/Configs/MailConfigs.fcg` | Reused and kept as the SharedLibs config contract. It reads registered `EResCSV.Gifts` and exposes code, detail, window, reuse, and reward getters. | `Verified from source script`; target `EditorGenLib.fcc:22-24` confirms `EResCSV.Gifts`. |
| `Assets/CSV/Mails/Gifts.csv` | Reused target fixture/schema; source production rows are not copied into the generic library. | `Verified from CSV`; target registration is present in `ProjectSettings/ResourceRegisteration.asset`. |
| `Assets/Scripts/Managers/MailsManager.fcg` | Extended with source-aligned `CheckRedeemGiftCode`, start/end checks, and a read-only used-code getter. | `Verified from source script`; target functions at lines `178-224`, `324-370`. |
| `Assets/Scripts/Consts/MailsDefinitions.fcg` | Reused for data keys, persistence keys, CSV columns, and mail limits. | `Verified from source script`; target definition file. |
| `Assets/Scripts/Consts/StatusCodes.fcg` | Reused for portable string result codes. | `Verified from source script`; target definition file. |
| `Assets/Scripts/Utils/DataUtils.fcg` | Reused for target mail/gift structured-data parsing and serialization. | `Verified from source script`; target call-sites in config/Manager. |

## Omitted or isolated source behavior

- `RebirthManager.CanUseGiftcode(...)` is source-specific. SharedLibs does not
  invent a rebirth provider; a consumer may add an eligibility check before
  calling the public Manager request.
- `PetsManager` slot checks from `PlayerGiftCode` are source-specific reward
  presentation logic and are not part of the generic redeem gate.
- `OnShowPrompt`, `OnReadMail`, `PlayerDataTracking`, and `HudGiftCode` are
  consumer feedback/UI integrations.
- Source `Limit`/`GiftCodeLimit` accumulation data has no active validation
  call-site in the source redeem path, so it is not copied as an unverified
  global quota rule.
- Source `PlayerGiftCode` is retained as evidence only; its imported graph has
  no active calls to the listed cache methods in the validated source tree.

