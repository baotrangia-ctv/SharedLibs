# Inventory active-API review

The current source Storage flow is the latest active flow: database callbacks,
store/retrieve Request-Check-Process actions, balance claim, capacity refresh,
and income loop. Active call sites were found in the source HUD, trigger, base,
passive, rebirth, tracking, visuals, and event-log managers.

The source `InventoryManager` is a separate active feature, not an alternate
Storage implementation. It owns `pMutagens`, `pWeatherGens`, and `pEventPets`;
it was excluded by the user request. No old Storage version had active call
sites requiring retention. Unused source helpers and commented passive
serialization were omitted.

Result: `Latest active implementation selected; no compatibility-only Storage API
required.`
