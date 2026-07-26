# Preserve-First, Stage-Based Inheritance Update

## Scope and Safety

This framework-only update changes SharedLibs rules, shared references, routers,
templates, current workflow skills, reusable reviews, `AGENTS.md`, and reports. It
does not change configured paths, source projects, consumer projects, or inherited
feature implementations. No feature was re-inherited.

## 1. Rules Updated

| Path | Old behavior | New behavior | Reason |
| --- | --- | --- | --- |
| `.codex/rules/preserve-first-bindings.md` | No explicit preserve-before-remap rule | Preserves structurally safe custom values before copy, adaptation, isolation, or MCP | Unknown meaning is not invalidity |
| `.codex/rules/repository-definition-search.md` | Repository search was general | Requires identifier-level definition and usage search | Prevents premature editor-only classification |
| `.codex/rules/stage-based-completion.md` | Completion was mostly whole-task | Requires independent stage statuses and safe continuation | One blocked stage must not erase safe work |
| `.codex/rules/standalone-portability.md` | Portability was mixed with clone completion | Separates faithful clone from standalone operation | Allows source-compatible intermediate output |
| `.codex/rules/serialized-asset-preservation.md` | Preserved unknown data generally | Explicitly preserves unknown enums, components, properties, and bindings unless invalidity is proven | Covers remaining HUD binding gates |
| `.codex/rules/clone-first-refactor-second.md` | Stage A preceded refactor | Adds Faithful Clone Mode and source-compatible status | Prevents forced early portability |
| `.codex/rules/studio-mcp-inheritance-policy.md` | Used general MCP-last blockers | Uses exact blocker evidence and excludes unknown values, local files, utilities, partial portability, and runtime gaps | Removes unconditional Studio dependency |
| `.codex/rules/feature-completeness.md` | Used whole-surface completeness categories | Uses per-stage statuses and independent surface results | Prevents presentation gaps failing all behavior |
| `.codex/rules/runtime-verification-separation.md` | Separated clone from runtime | Separates clone, portability, and runtime | Establishes three independent dimensions |
| `.codex/rules/utility-reuse.md` | Focused on data helper reuse | Adds source-wide utility dependency analysis and smallest-surface handling | Utility references no longer block a feature |
| `.codex/rules/config-preservation.md` | Referred generally to strict MCP stop conditions | Uses exact blocker evidence and stage-only blocking for registration gaps | Keeps config behavior aligned |
| `.codex/rules/layer-based-file-placement.md` | Used a concrete feature folder in a global example | Uses `Assets/Scripts/[Module]/` | Keeps common rules module-agnostic |

Existing Adapter-Last, Demo-Last, active implementation, layer placement, config,
static-definition, and utility-reuse principles remain active.

## 2. Routers Updated

| Path | Old behavior | New behavior | Reason |
| --- | --- | --- | --- |
| `.codex/skills/source-to-shared-router/SKILL.md` | Clone and dependency review preceded a mostly whole Stage B gate | Searches definitions, decides preserve/copy/adapt/isolate, completes safe stages, creates a faithful clone, assesses portability, and uses MCP for exact blockers | Applies preserve-first to every source module |
| `.codex/skills/shared-to-consumer-router/SKILL.md` | Required portability artifacts, adapted after transfer, and required configured SharedLibs read-only mode | Preserves consumer-compatible values, searches consumer definitions, completes safe stages, and treats SharedLibs as workflow read-only even when configured read-write | Applies the same policy downstream without conflicting with configuration |

Both routers keep validated source roots read-only and remain module-agnostic.

## 3. Module Templates Updated

| Path | Old behavior | New behavior | Reason |
| --- | --- | --- | --- |
| `.codex/skills/source-to-shared-router/references/module-source-to-shared-template.md` | Required clone, refactor, and runtime separation | Adds all six new references, Faithful Clone Mode, stage completion, portability review, and exact blockers | Future source skills inherit the policy |
| `.codex/skills/shared-to-consumer-router/references/module-shared-to-consumer-template.md` | Preserved assets and dependency closure | Adds definition search, preserve-first decisions, partial stage completion, and portability reporting | Future consumer skills inherit the policy |
| `.codex/skills/source-to-shared-router/references/feature-surface-inventory-template.md` | Tracked clone and generic surface status | Adds binding classification, stage status, and portability impact | Inventories unknowns without calling them invalid |
| `.codex/skills/source-to-shared-router/references/inheritance-report-template.md` | Contained 30 clone/runtime fields | Retains those fields and adds 19 stage, utility, texture, custom-definition, blocker, and portability fields | Preserves prior evidence while adding new policy |
| `.codex/skills/shared-to-consumer-router/references/consumer-integration-report-template.md` | Contained 30 integration fields | Adds the same 19 stage and portability fields | Keeps both directions consistent |

## 4. Review Skills Updated

| Path | Old behavior | New behavior | Reason |
| --- | --- | --- | --- |
| `.codex/skills/review-serialized-asset-fidelity/SKILL.md` | Compared assets and failed missing targets | Searches definitions, verifies preserve-first handling, resolves utilities/assets, and distinguishes preserved unknowns from structural invalidity | Avoids automatic remapping |
| `.codex/skills/review-asset-dependency-closure/SKILL.md` | Used generic dependency statuses | Distinguishes copy, reuse, source-specific, extractable, engine-owned, missing, MCP, and runtime dependencies | Supports local texture and utility closure |
| `.codex/skills/review-clone-fidelity/SKILL.md` | Failed material unresolved items | Passes structurally preserved unknowns and source-compatible clones while reporting portability separately | Clone fidelity no longer means standalone |
| `.codex/skills/review-feature-completeness/SKILL.md` | Assigned broad surface completion | Reports 14 explicit surfaces independently and combines with portability review | One unresolved surface no longer fails all |
| `.codex/skills/review-feature-completeness/references/feature-surface-checklist.md` | Used prior completeness categories | Uses six stage statuses and independent surfaces | Aligns checklist with stage completion |
| `.codex/skills/review-feature-completeness/references/hud-and-ui-checklist.md` | Required asset fidelity and ID handling | Adds repository definition search and utility/texture closure | Covers remaining HUD dependencies |
| `.codex/skills/review-folder-architecture/SKILL.md` | Could stop broadly for opaque editor-owned registration | Requires concrete structural-invalidity evidence and defers only the affected move | Removes a remaining vague editor-owned gate |

## 5. New Standalone Portability Review

`.codex/skills/review-standalone-portability/SKILL.md` evaluates remaining
source-project utilities, services, custom components, enums, consumer integration
points, target equivalents, and runtime dependencies. It reports:

- `Standalone`
- `Standalone with optional integrations`
- `Source-compatible only`
- `Consumer adaptation required`
- `Blocked by exact dependency`
- `Runtime verification pending`

It never changes clone-fidelity status merely because portability is partial.

## 6. Shared References Added

| Path | Responsibility |
| --- | --- |
| `.codex/references/inheritance/preserve-first-bindings.md` | Preserve/copy/adapt/isolate/MCP decision order and binding classifications |
| `.codex/references/inheritance/repository-definition-search.md` | Source and shared definition-search evidence |
| `.codex/references/inheritance/faithful-clone-mode.md` | Source-compatible intermediate clone semantics |
| `.codex/references/inheritance/stage-based-completion.md` | Nine stages and six completion statuses |
| `.codex/references/inheritance/standalone-portability.md` | Clone-versus-portability questions and statuses |
| `.codex/references/inheritance/explicit-mcp-blockers.md` | Six full-stop conditions and exact blocker fields |

Updated shared references:

| Path | Old behavior | New behavior |
| --- | --- | --- |
| `.codex/references/inheritance/serialized-assets.md` | Preserved unresolved data generally | Delegates custom bindings to Preserve-First |
| `.codex/references/inheritance/dependency-closure.md` | Traced transitive dependencies | Adds utility and texture workflows and stage-only blocking |
| `.codex/references/inheritance/clone-first-workflow.md` | Defined Stage A and Stage B | Adds Faithful Clone Mode and separate portability |
| `.codex/references/inheritance/mcp-last.md` | Listed six generic stop conditions | Delegates to exact blocker evidence and safe-stage continuation |
| `.codex/references/inheritance/clone-fidelity.md` | Expected dependency closure to be resolved | Allows inventoried, structurally preserved portability gaps | Keeps fidelity separate from portability |
| `.codex/references/inheritance/runtime-verification.md` | Separated clone from runtime | Separates clone, portability, and runtime | Prevents status conflation |

The required portability status `Runtime verification pending` now explicitly means
that the portability assessment awaits live evidence; it does not replace or encode
the separate runtime result. Report field 37 now records runtime evidence and pending
checks instead of duplicating the runtime status at field 27.

Feature completeness applies stage statuses only to Manager through Custom enums.
Standalone portability and Runtime verification use their own independent status
vocabularies.

Runtime verification remains a common workflow stage, but its stage status describes
progress only. The live runtime result is reported separately with the
runtime-verification vocabulary.

## 7. Conflicting Hard Gates Removed

| Path | Conflict removed | Replacement |
| --- | --- | --- |
| `.codex/skills/mails-source-to-shared/SKILL.md` | Stage A unresolved dependencies could prevent Stage B and complete output | Loads common preserve-first references, completes safe stages, and reports portability |
| `.codex/skills/mails-shared-to-consumer/SKILL.md` | Portability package was an unconditional input and transfer gate | Treats it as available evidence and continues safe analysis/integration stages |
| `AGENTS.md` | Did not route preserve-first, partial stages, or standalone review | Registers the new review and concise global policies |

Removed framework assumptions include: unfamiliar custom values require remapping,
local textures require Studio, source-wide utilities block a feature, standalone
portability is required in the first pass, runtime validation determines clone
fidelity, and one blocked optional dependency prevents all output.

## 8. Preserve-First Behavior

The framework now searches definitions and usages, preserves structurally safe values,
copies or adapts repository definitions when needed, isolates source-specific
behavior through the smallest integration point, and considers MCP only after those
options fail. `Meaning unknown but structurally preservable` is a valid outcome.
Structural invalidity requires concrete evidence.

## 9. Stage-Based Completion Behavior

Source discovery, active API analysis, Manager, config/CSV, lifecycle, serialized
assets, dependency closure, shared refactor, and runtime verification receive
independent statuses. A faithful clone may be `Source-compatible` and `Not yet
standalone`; completed safe files and stages remain valid outputs.

## 10. Exact MCP Blocker Requirements

Every unavailable-MCP blocker must enumerate its identifier, source and target paths,
dependency type, searches, definition result, preservation and filesystem-adaptation
decisions, structural-invalidity evidence, MCP resolution, affected stage, and
whether other stages continue. The entire task blocks only when all six conditions in
`explicit-mcp-blockers.md` are true.

## 11. Validation Scenario Results

| Scenario | Framework result |
| --- | --- |
| A: Repository utility | Inspect APIs and dependencies; reuse, copy, extract, or isolate; continue independent stages |
| B: Local textures | Resolve and copy the smallest repository closure without MCP |
| C: Unknown custom enum | Search definitions and usages, preserve when safe, and report unknown meaning |
| D: Defined custom component | Copy or adapt its definition and preserve properties without MCP |
| E: Missing component definition | Determine required/optional, preserve or isolate when safe, and block only an invalid affected stage |
| F: Source-compatible, not standalone | Faithful clone and clone fidelity may pass while portability remains partial |
| G: Studio closed | Continue repository-safe stages, enumerate exact blockers, and leave runtime pending |

This is a framework dry run. No feature inheritance or live Studio runtime
verification was performed.

Validation also confirmed:

- all 16 repository skills have valid frontmatter and directory-matching names;
- all six new shared references exist and all referenced common paths resolve;
- both common report templates contain 49 numbered fields;
- the Preserve-First, stage, portability, asset-fidelity, and six exact MCP blocker
  vocabularies are complete;
- a forward test preserved an unknown numeric enum, copied a repository-defined
  custom component, selected only the used utility APIs, resolved local textures
  without MCP, passed clone fidelity as source-compatible, and reported dependency
  and refactor stages as `Partially complete`;
- an independent router and review dry run found no remaining contradictions and
  passed scenarios A through G;
- managed `AGENTS.md` blocks are unchanged;
- no configured path, inherited implementation, `Assets/`, or engine-project
  directory was modified.

## 12. Remaining Framework Limitations

- Live import, registration, rendering, and runtime behavior still require supported
  Studio or build tooling when those checks are requested.
- Preserve-first does not permit copying data proven structurally unsafe.
- Managed Studio blocks remain unchanged and continue governing semantic asset edits,
  registration, opaque formats, and live validation.
- `init_skill.py` and `quick_validate.py` cannot run because the environment exposes
  only the Windows Store Python alias without an interpreter. The new skill is
  scaffolded manually using the repository's existing `SKILL.md` convention and will
  be checked with an equivalent structural validator.
