# Mails Request Check Process Review

Date: 2026-07-27
Module: `mails`

- `RequestReceiveMail` -> `CheckConditionReceiveMail` -> `ProcessReceiveMail` is preserved in `Assets/Scripts/Managers/MailsManager.fcg`.
- `RequestClaimMail` -> `CheckConditionClaimMail` -> `ProcessClaimMail` is preserved in `Assets/Scripts/Managers/MailsManager.fcg`.
- Check methods remain read-only and reject full mailbox, invalid gift ids, reused non-reusable gifts, duplicate claims in progress, and invalid mail indexes before mutation.
- Process methods own mutation by inserting or removing mail entries and updating used-gift state.
- Shared claim processing intentionally stops before reward granting because the source reward subsystem is not portable as-is; claimed mail data is surfaced for the consumer to resolve.

Residual validation need:

- Consumer integration must ensure reward application is idempotent before persisting any external grant side effects.
