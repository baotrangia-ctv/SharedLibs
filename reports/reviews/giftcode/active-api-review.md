# Giftcode Active API Review

| API/surface | Status | Evidence |
| --- | --- | --- |
| `MailsManager.RequestReceiveMail` | Latest active | Called by source `HudGiftCode` and other source reward flows. |
| `MailsManager.CheckConditionReceiveMail` | Active gate | Calls `CheckRedeemGiftCode` for configured gifts. |
| `MailsManager.CheckRedeemGiftCode` | Active helper | Validates ID, window, reuse, and used-code state. |
| `MailsManager.ProcessReceiveMail` | Active mutation | Adds used ID and mail after checks pass. |
| `MailsManager.IsGiftWindowValid` | Compatibility helper | Existing target API; retained while Manager uses explicit start/end helpers. |
| `PlayerGiftCode` cache methods | Unused/source legacy for this path | Only import-only references were found; no active method call-site. |
| Source `GiftCodeLimit` accumulation | Unresolved optional | Declared and tracked by source but not used to gate the active redeem request. |

No deprecated source API was copied into the target core.

