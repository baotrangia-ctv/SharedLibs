# Repository-First, Clone-First Framework Update

## Scope and Safety

This update changes only SharedLibs inheritance rules, routers, skill templates,
current workflow skills, reusable reviews, shared references, report templates,
`AGENTS.md`, and this audit report. It does not change configured project paths,
source projects, consumer projects, or inherited feature implementations. No feature
was re-inherited.

## 1. Global Rules Created or Updated

| Path | Old behavior | New behavior | Reason |
| --- | --- | --- | --- |
| `.codex/rules/repository-first-source-of-truth.md` | No dedicated global evidence priority or complete label vocabulary | Repository scripts and serialized assets are primary, followed by dependencies, reports, then MCP | Makes filesystem evidence authoritative and uniform |
| `.codex/rules/serialized-asset-preservation.md` | Readable assets were not governed by a common identity and unknown-data policy | Preserves structure, identity, references, bindings, and unknown data by default | Prevents silent asset loss and invented replacements |
| `.codex/rules/clone-first-refactor-second.md` | Generic target design could precede faithful source capture | Defines Stage A faithful clone and Stage B behavior-preserving refactor | Prevents premature abstraction |
| `.codex/rules/dependency-closure.md` | Minimal file count was emphasized without a global transitive-closure rule | Requires the smallest complete dependency closure and explicit classifications | Prevents broken references and bulk copying |
| `.codex/rules/behavior-preservation.md` | Source-specific behavior could be separated without one common decision record | Requires a documented keep, replace, abstract, optional, defer, or remove decision | Prevents silent behavior deletion |
| `.codex/rules/runtime-verification-separation.md` | Filesystem completion and live verification were not independently defined | Separates serialized clone status from live runtime status | Allows honest completion without false runtime claims |
| `.codex/rules/studio-mcp-inheritance-policy.md` | Allowed a generic HUD fallback and used five behavior-oriented blockers | Uses MCP last and permits an MCP stop only when all six strict conditions are true | Makes MCP optional and evidence-driven |
| `.codex/rules/ui-completeness.md` | A minimal generic HUD was the default when Studio hierarchy was unavailable | Available readable UI is cloned; a minimal fallback is allowed only when no serialized source asset exists | Preserves source assets rather than approximating them |
| `.codex/rules/feature-completeness.md` | Focused on behavioral layers and accepted generic UI fallback | Includes serialized assets, dependencies, six surface statuses, and Stage A completion | Makes completeness work for all artifact types |
| `.codex/rules/minimal-source-generation.md` | Could interpret minimal as fewer source files | Defines minimal as the smallest complete dependency closure | Prevents fidelity loss |
| `.codex/rules/config-preservation.md` | Allowed validation-only hardcoding and early removal of product rows | Preserves Stage A schema, parsing, validation, defaults, and required rows before Stage B classification | Keeps config behavior faithful |
| `.codex/rules/layer-based-file-placement.md` | Listed only skill-local references | Adds `.codex/references/inheritance/` for framework-wide progressive references | Avoids duplicated policy |

Adapter-Last, Demo-Last, utility reuse, active-implementation selection, static
definition organization, and layer placement remain active.

## 2. Routers Updated

| Path | Old behavior | New behavior | Reason |
| --- | --- | --- | --- |
| `.codex/skills/source-to-shared-router/SKILL.md` | Routed discovery directly toward minimal generic implementation and conditional Studio fallback | Routes repository discovery, active-version selection, dependency closure, Stage A clone, fidelity reviews, Stage B refactor, reports, then optional runtime verification | Applies one clone-first sequence to every module |
| `.codex/skills/shared-to-consumer-router/SKILL.md` | Focused on contract mapping and consumer adaptation without serialized fidelity gates | Requires repository inspection, faithful asset and API transfer, dependency closure, consumer-only adaptation, and separate runtime status | Applies the same evidence discipline downstream |

Both routers keep project validation and source read-only boundaries. Neither router
contains feature-specific behavior.

## 3. Module Templates Updated

| Path | Old behavior | New behavior | Reason |
| --- | --- | --- | --- |
| `.codex/skills/source-to-shared-router/references/module-source-to-shared-template.md` | Designed a minimal target and generic HUD before a formal clone gate | Requires discovery, active selection, dependency closure, Stage A clone reviews, then Stage B | Ensures future module skills inherit the common sequence |
| `.codex/skills/shared-to-consumer-router/references/module-shared-to-consumer-template.md` | Required layer and integration mapping only | Adds faithful serialized transfer, dependency closure, MCP-last, and separate runtime reporting | Ensures future consumer skills preserve shared artifacts |
| `.codex/skills/source-to-shared-router/references/feature-surface-inventory-template.md` | Used old evidence labels and generic-HUD fallback | Adds active, clone, surface, dependency, and target classifications using shared labels | Supports auditable Stage A decisions |

## 4. Existing Module Skills Updated to Use Common References

All current source-to-shared and shared-to-consumer workflow skills now load common
references from `.codex/references/inheritance/`. Their module-specific checks remain
local, but they cannot override repository-first discovery, Stage A clone fidelity,
dependency closure, MCP-last stop conditions, or separate runtime reporting.

Module references that previously allowed a default minimal HUD or used old evidence
labels now defer to the shared serialized-asset and repository-first policies.

## 5. Reusable Review Skills Created or Updated

| Skill | Result |
| --- | --- |
| `review-serialized-asset-fidelity` | Compares all readable serialized asset types, ID handling, properties, bindings, unknown data, and references without mutating assets |
| `review-asset-dependency-closure` | Traces local and engine dependencies transitively, identifies missing artifacts, and rejects incomplete or bulk copies |
| `review-clone-fidelity` | Gates Stage B on latest-active behavior, API, config, CSV, lifecycle, event, asset, and dependency fidelity |
| `review-feature-completeness` | Covers all generic surfaces and assigns one of six required completion statuses |

Required review destinations are:

- `reports/reviews/[module]/serialized-asset-fidelity-review.md`
- `reports/reviews/[module]/asset-dependency-closure-review.md`
- `reports/reviews/[module]/clone-fidelity-review.md`

## 6. Shared References Created

| Reference | Responsibility |
| --- | --- |
| `.codex/references/inheritance/repository-first.md` | Evidence priority and labels |
| `.codex/references/inheritance/clone-first-workflow.md` | Stage A and Stage B workflow and artifact classifications |
| `.codex/references/inheritance/serialized-assets.md` | Serialized inspection, identity, references, and unknown-data preservation |
| `.codex/references/inheritance/dependency-closure.md` | Transitive dependency classifications and handling |
| `.codex/references/inheritance/mcp-last.md` | Valid MCP uses and six strict stop conditions |
| `.codex/references/inheritance/clone-fidelity.md` | Clone comparison checks and statuses |
| `.codex/references/inheritance/runtime-verification.md` | Independent serialized and runtime completion statuses |

Detailed guidance is centralized here so routers and module skills remain concise and
load only relevant references.

## 7. Conflicting MCP Assumptions Removed

Active inheritance instructions no longer request MCP before repository inspection,
require Studio because UI or complex serialized data exists, or treat a closed Studio
session as a blocker. MCP is considered only after scripts, serialized assets,
dependencies, reports, and documentation have been exhausted. An MCP-related stop
requires all six strict conditions.

## 8. Minimal Replacement Behavior Removed

The former default generic-HUD fallback was removed from routing, module templates,
current source workflows, feature inventories, UI review checklists, and
completeness rules. When a readable source asset exists, it must be copied or
faithfully reconstructed. A minimal replacement is a final fallback only when no
serialized source asset exists and repository evidence supports a safe runnable
fallback.

## 9. Clone-First Workflow Introduced

Stage A captures the latest active implementation, behavior, public contracts,
serialized assets, lifecycle, and dependency closure. Stage B begins only after clone
fidelity review and may then reuse utilities, isolate source dependencies, remove
confirmed obsolete artifacts, and organize files by SharedLibs layer. Every Stage B
behavior change requires compatibility and consumer-responsibility notes.

## 10. Serialized Asset Handling Introduced

Readable JSON and structured-text assets are authoritative evidence. The framework
preserves hierarchy, ordering, names, IDs or documented remapping, properties,
components, events, enums, bindings, localization, and resource references. Unknown
data remains preserved when safe and can be removed only with evidence and a recorded
reason.

## 11. Dependency Closure Handling Introduced

Every active local reference receives one shared dependency classification. Reviews
follow references transitively, distinguish local and engine-owned resources, search
for relocated dependencies, and reject both incomplete root-only copies and unrelated
directory copies.

## 12. Runtime Verification Separation Introduced

Reports now contain independent serialized clone and runtime verification statuses.
Repository inheritance may report:

```text
Serialized clone completed.
Runtime Studio verification was not performed.
```

No compile, load, render, event, action, persistence, or runtime-success claim is
allowed without its corresponding live validation.

## 13. AGENTS.md Changes

`AGENTS.md` registers all three new reusable reviews and routes them by trigger. It
states repository-before-MCP, clone-before-genericization, dependency closure,
serialized asset preservation, no simplified replacements when source assets exist,
and separate runtime status. Detailed checklists remain in common references.

Managed Craftland Studio sections were not edited.

## 14. Validation Scenario Results

| Scenario | Static framework result | Evidence |
| --- | --- | --- |
| A: Complete serialized asset | Pass: no MCP prerequisite; clone, asset fidelity, closure, then refactor | repository-first, serialized-assets, clone-first, and both routers |
| B: Unknown custom data | Pass: preserve when safe, trace, classify, use MCP only if safety requires it | serialized-assets and serialized-fidelity review |
| C: Missing local dependency | Pass: report, search validated roots, continue independent work, no silent replacement | dependency-closure reference and review |
| D: No serialized asset | Pass: exhaust scripts, metadata, config, reports; use MCP if strict conditions apply; minimal fallback last | UI completeness, MCP-last, and source template |
| E: Studio closed | Pass: repository work continues, serialized completion may succeed, runtime remains pending | MCP-last and runtime-verification references |
| F: Old and new APIs | Pass: trace active call sites, clone latest active, retain compatibility only with evidence | active implementation rule and clone-fidelity review |
| G: Source-specific behavior | Pass: preserve in Stage A, classify, then isolate behind the smallest extension point | clone-first and behavior-preservation rules |

This validation is a framework dry run. No module inheritance or live Studio runtime
test was performed.

Validation also confirmed:

- all 15 repository skills have valid `name` and `description` frontmatter and names
  matching their directories;
- the common evidence reference contains all 11 required labels;
- the inheritance report template contains exactly 30 numbered sections;
- all six MCP stop conditions are present;
- managed `AGENTS.md` sections are unchanged;
- no configured path, `Assets/`, or engine-project directory was modified;
- no stale legacy evidence labels or default generic-HUD instruction remains.

## 15. Remaining Framework Limitations

- The framework can validate readable serialized fidelity without Studio, but live
  import, registration, rendering, and runtime behavior still require supported
  editor or build tooling when those checks are requested.
- Managed Craftland asset rules remain authoritative for direct semantic editing or
  registration of opaque editor-owned assets. This framework update does not alter
  those managed sections.
- The new skills were scaffolded as repository skills without generated
  `agents/openai.yaml` metadata because the current repository convention contains
  only `SKILL.md` and references for project skills.
- The bundled `quick_validate.py` could not run because this environment exposes only
  the Windows Store Python alias and no Python interpreter. An equivalent PowerShell
  structural validator passed all 15 repository skills.
- Scenario validation proves routing and instruction behavior, not any individual
  feature's clone fidelity.
