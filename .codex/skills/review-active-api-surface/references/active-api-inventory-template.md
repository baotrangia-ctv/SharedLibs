# Active API Inventory Template

Create an API inventory before implementation:

| API | Version | Call Sites | Status | Inheritance Decision |
| --- | ------- | ---------- | ------ | -------------------- |
| `Feature()` | v1 | none or legacy | Deprecated | Omit |
| `FeatureV2()` | v2 | active HUD and Manager | Latest active | Inherit |
| `LegacySave()` | legacy | migration only | Compatibility-only | Isolate if required |

Allowed statuses:

- Active
- Latest active
- Compatibility-only
- Deprecated
- Unused
- Demo-only
- Needs verification
