# Mails Lifecycle Review

Date: 2026-07-27
Module: `mails`

- Player join / database load: `OnDatabaseLoad` routes the registered `Mails` database to `LoadMailsDatabase`.
- Default-data creation: `InitPlayerMails` creates empty mail, used-gift, and in-flight claim state.
- Cache initialization: current and pending mail data are combined into `_PlayerMails`.
- Database-ready signal: `DatabaseController.SetDatabaseReady(playerUID, "Mails", true)` is preserved after load completes.
- Runtime updates: receive and claim actions mutate only the in-memory cache.
- Save: `OnDatabaseSave` routes to `SaveMailsDatabase`, which writes used-gift ids plus current mails and marks the database saved.
- Shutdown cleanup: `ClearData` is called after save to mirror the existing SharedLibs manager pattern.

Findings:

- The source manager's compensate flow and analytics/prompt callbacks were intentionally omitted from the shared runtime and therefore do not participate in the shared lifecycle yet.
- No reconnect-specific recovery logic was introduced beyond the normal database load path.
