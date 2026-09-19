# Giftcode Request-Check-Process Review

Status: `Pass for core flow`.

1. `MailsManager.RequestReceiveMail` receives the public payload and delegates to
   `CheckConditionReceiveMail`.
2. `CheckConditionReceiveMail` verifies player cache and mail capacity, then calls
   `CheckRedeemGiftCode` for configured gifts.
3. `CheckRedeemGiftCode` is read-only: it checks configured ID, start/end window,
   reuse policy, and used-code state.
4. `ProcessReceiveMail` owns mutation: it adds the used ID when required and
   appends the normalized mail record.
5. Failed checks return before any mail or used-code mutation.

The target Manager API returns portable string status codes; UI notification and
reward application remain consumer responsibilities. Repeated sequential calls
are guarded by the persisted used-code check for non-reusable gifts.

