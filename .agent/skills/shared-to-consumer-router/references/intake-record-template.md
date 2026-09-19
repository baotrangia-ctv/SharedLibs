# Intake Record Template (00-intake.md)

Every shared-to-consumer integration must create this record at
`reports/consumer-integrations/[consumer-project]/[module]/00-intake.md`
before touching any file outside `reports/`. Include:

1. Module name covered by this request
2. Confirmed route: `shared-to-consumer-router` (SharedLibs -> consumer
   project)
3. Validated SharedLibs root and access mode (read-only for this workflow)
4. Validated consumer root and access mode
5. Selected `[module]-shared-to-consumer` skill, or a note that it is missing
   and blocks routing
6. Required Common References actually opened, listed by path (from this
   router's `# Required Common References` section)
7. Complexity Gate assessment: which component types are present (Manager,
   HUD/UI script, Config/CSV, Persistence, Event, Public API/contract,
   independent serialized asset), whether sensitive state is present
   (persistence, reconnect, runtime cache, or network/server sync), and the
   resulting `simple` or `complex - mandatory phase plan` verdict
8. Force keyword used, if any
9. Any Stop Condition triggered and how it was resolved

Do not proceed to SharedLibs inspection, Stage A, or printing a Phase Plan
until this file exists with every field filled in.
