# Inventory Request-Check-Process review

| Action | Entry point | Check | Process | Result |
|---|---|---|---|---|
| Store pet | `RequestStorePet` | player flag, data readiness, capacity readiness, capacity, pet validity, interactable flag, feature flag | timestamp, normalize, append, recalculate income | Complete with consumer snapshot obligation; pre-capacity requests return `InventoryCapacityNotReady`, never `PlayerFullStorage` |
| Retrieve pet | `RequestRetrievePetBySlot` | player flag, data readiness, capacity readiness, slot, pet presence, base capacity, lock, feature flag | remove, recalculate, return pet snapshot | Complete with consumer add obligation; readiness is checked before slot/fullness evaluation |
| Claim balance | `HandleClaimBalance` | empty/missing balance guard | zero balance and return claimed amount | Complete; wallet credit is external |

Checks do not mutate persistence or the inventory list. Store/retrieve mutations
occur only after checks pass. Local pet-index duplication is rejected before
append. Consumer-side duplicate requests still require a stable pet index and a
single authoritative transfer operation.

The capacity race is resolved: `LoadInventoryDatabase` can finish persistence
loading before the consumer supplies base/bonus capacity, but it leaves
`MaxSlot` provisional and does not finalize `DatabaseReady`. Once
`SetInventoryCapacityInputs` is called, normal capacity clamping and request
checks resume.

Source UI/prompt/transaction side effects are intentionally outside the shared
Manager; consumers must surface returned status strings and record analytics if
required.
