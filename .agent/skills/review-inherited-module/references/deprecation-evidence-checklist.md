# Deprecation Evidence Checklist

Use this reference when classifying APIs as deprecated, unused, or compatibility-only.

Verify with evidence:

- no active call sites
- not referenced by current HUD flow
- not referenced by current Manager flow
- not registered by active events
- not required by config-driven flow
- not required by migration or compatibility behavior

Do not classify an API as deprecated only from its name.
