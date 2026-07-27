# Mails Active API Review

Date: 2026-07-27
Module: `mails`

| API | Status | Inheritance decision | Evidence |
| --- | --- | --- | --- |
| `RequestReceiveMail` | Latest active | Inherit | Called by source mail-receive and gift-code flows. |
| `RequestClaimMail` | Latest active | Inherit | Called by the source mail HUD. |
| `GetPlayerMails`, `GetPlayerMailByIndex`, `GetPlayerMailsCount`, `IsHavingMail`, `GetExpireDatesLeft` | Active | Inherit | Queried by the source HUD flow. |
| `LoadOldMails` | Compatibility-only | Do not expose as shared public API | Source comments mark the path deprecated and temporary. |
| `LoadPlayerMails_Deprecated` | Deprecated | Omit from shared active API | Source comments mark the method deprecated. |
| `ExtractPlayerMails_Deprecated` | Deprecated | Omit from shared active API | Source comments mark the method deprecated. |
| `CleanMails_Deprecated` | Deprecated | Omit from shared active API | Source comments mark the method deprecated. |

Conclusion:

- The active shared surface should center on receive, claim, query, and persistence APIs.
- Deprecated migration helpers were documented but not carried forward as live shared contracts.
