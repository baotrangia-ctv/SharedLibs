# Rollback Cases Checklist

Use this reference only when the feature changes persistence schemas, adapters, integration behavior, or rollout shape.

Review:

- Feature disable path
- Module removal path
- Config rollback
- Shared module version rollback
- Persistence schema rollback
- Adapter rollback
- Consumer integration rollback
- Old and new implementation coexistence
- Partial deployment safety

Call out missing rollback notes when production state may be affected.
