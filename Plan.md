# Shared Modules Rules and Skills Plan

## 1. Updated Objective

### Mandatory Objective

This plan defines a simplified, reusable Codex architecture for two inheritance directions:

```text
StealAPet
    ->
SharedLibs
```

and:

```text
SharedLibs
    ->
Consumer Project
```

The plan preserves these existing goals and requirements:

- Source-to-shared inheritance
- Shared-to-consumer inheritance
- Generic reusable module implementation
- Runnable demo
- Business-logic abstraction
- `Request -> Check -> Process`
- Portability manifest
- Consumer inheritance support
- Automatic skill routing
- Progressive reference loading
- Review reports
- Token-efficiency requirements

### Mandatory Change in This Revision

This revision reduces skill fragmentation.

The default per-module model is no longer many module-specific analysis, implementation, review, and consumer-kit skills.

Instead, each module should normally create only:

- one module-specific source-to-shared workflow skill
- one module-specific shared-to-consumer workflow skill

Example:

```text
activities-source-to-shared
activities-shared-to-consumer
```

Reusable cross-module review skills remain global.

### Mandatory Safety Principle

Project selection must not rely on automatic filesystem discovery.

Project paths must come from a user-managed configuration file:

```text
.codex/project-paths.json
```

Codex must validate configured paths before reading or modifying module files.

### Planning Task Constraint

This task only revises the plan.

It does not implement repository files, create skills, generate reports, or modify code outside this planning document.

## 2. Simplified Skill Architecture

### Global Routers

Mandatory global routers:

- `source-to-shared-router`
- `shared-to-consumer-router`

### Module-Specific Workflow Skills

Each module normally creates only two module-specific workflow skills:

- `[module]-source-to-shared`
- `[module]-shared-to-consumer`

Examples:

- `activities-source-to-shared`
- `activities-shared-to-consumer`
- `mail-source-to-shared`
- `mail-shared-to-consumer`

### Reusable Review Skills

Cross-module review work should be handled by reusable global skills instead of duplicated module-specific review skills.

At minimum:

- `review-data-lifecycle`
- `review-request-check-process`
- `review-production-readiness`

### Mandatory Constraint

Do not retain the old eight-skill-per-module default.

Do not combine all modules into one universal implementation skill.

Do not create separate module-specific analysis, inheritance, review, and consumer-kit skills unless a documented complexity reason justifies the split.

## 3. Global Router Design

### Global Routers

Mandatory router skills:

```text
.codex/skills/
  source-to-shared-router/
    SKILL.md

  shared-to-consumer-router/
    SKILL.md
```

### Router Responsibilities

Each global router must:

1. Read path configuration requirements
2. Determine whether the request is:
   - source-to-shared inheritance
   - shared-to-consumer integration
   - analysis only
   - implementation
   - review
   - documentation
3. Select the correct single module workflow skill
4. Select only the reusable review skills that apply
5. Define execution order
6. Avoid creating or loading unnecessary module-specific routers

### Mandatory Default

Module-specific routers should not be created by default.

A module-specific router may be created only when:

- the module supports several fundamentally different workflows
- the module has many independent subfeatures
- routing cannot be handled clearly by the global router
- the reason is documented

### Source-to-Shared Routing Example

User prompt:

```text
Inherit Activities from Steal A Pet into the shared project.
```

Expected routing:

```text
source-to-shared-router
    ->
activities-source-to-shared
    ->
review-request-check-process
    ->
review-data-lifecycle
```

### Shared-to-Consumer Routing Example

User prompt:

```text
Add the shared Activities module to this game and connect it to the existing wallet and player database.
```

Expected routing:

```text
shared-to-consumer-router
    ->
activities-shared-to-consumer
    ->
review-request-check-process
    ->
review-data-lifecycle
    ->
review-production-readiness
```

## 4. Module-Specific Source-to-Shared Skill Design

### Naming Convention

Each inherited module must normally have one combined source-to-shared skill:

```text
[module]-source-to-shared
```

Example:

```text
activities-source-to-shared
```

### Role

This is a module-specific workflow skill.

It coordinates the full source-to-shared workflow for one module.

### Mandatory Workflow

The source-to-shared workflow skill must coordinate:

```text
Validate configured project paths
    ->
Analyze source module dependencies
    ->
Trace source feature flow
    ->
Separate generic and Steal A Pet-specific logic
    ->
Design the generic module
    ->
Implement the generic module
    ->
Create a runnable demo
    ->
Run applicable reusable reviews
    ->
Generate documentation
    ->
Generate portability manifest
    ->
Generate the downstream consumer integration package
    ->
Produce reports
```

### Example Structure

```text
.codex/skills/activities-source-to-shared/
├── SKILL.md
└── references/
    ├── dependency-analysis.md
    ├── business-abstraction.md
    ├── demo-requirements.md
    ├── module-contract-template.md
    └── consumer-kit-template.md
```

### Mandatory Constraint

Do not split this workflow into multiple Activities-specific skills unless a clear technical need is documented.

### Demo-Only Behavior

This workflow may generate:

- mock reward handlers
- notification-only rewards
- mock persistence
- minimal example configs

### Production Integration Behavior

This workflow must clearly document:

- where demo components are used
- what must be replaced in production
- which extension points consumer projects must implement

## 5. Module-Specific Shared-to-Consumer Skill Design

### Naming Convention

Each completed shared module must normally have one downstream consumer skill:

```text
[module]-shared-to-consumer
```

Example:

```text
activities-shared-to-consumer
```

### Role

This is a module-specific workflow skill.

It coordinates downstream consumer integration without reading Steal A Pet source.

### Mandatory Workflow

The shared-to-consumer skill must coordinate:

```text
Validate configured project paths
    ->
Read module portability manifest
    ->
Read public contracts and extension points
    ->
Analyze the consumer project
    ->
Map shared contracts to consumer systems
    ->
Adapt consumer business logic
    ->
Replace demo handlers
    ->
Integrate persistence
    ->
Integrate UI
    ->
Preserve Request -> Check -> Process
    ->
Run applicable reusable reviews
    ->
Validate production readiness
    ->
Generate integration and rollback reports
```

### Example Structure

```text
.codex/skills/activities-shared-to-consumer/
├── SKILL.md
└── references/
    ├── integration-contract.md
    ├── business-adaptation.md
    ├── demo-replacement.md
    ├── consumer-validation.md
    └── rollback-checklist.md
```

### Mandatory Data Boundary

The downstream skill must operate without reading the original Steal A Pet source.

It may use only:

- the completed SharedLibs module
- the portability manifest
- public contracts
- module references
- consumer project source
- consumer requirements

### Production Integration Behavior

This workflow is where:

- demo handlers are replaced
- real persistence is connected
- consumer business logic is introduced
- release readiness is validated

## 6. Reusable Review Skill Design

### Reusable Review Skills

These are global reusable review skills, not module-specific workflow skills.

At minimum:

- `review-data-lifecycle`
- `review-request-check-process`
- `review-production-readiness`

### `review-data-lifecycle`

Use when a module:

- loads or saves player data
- maintains per-player runtime cache
- registers database readiness
- handles reconnect
- handles player quit or server shutdown
- grants persistent or one-time rewards
- changes progression data

It should conditionally read references such as:

- `load-save-lifecycle.md`
- `cache-invariants.md`
- `reconnect-cases.md`
- `rollback-cases.md`
- `known-incidents.md`

### `review-request-check-process`

Use when a module exposes user actions or public Manager operations.

It must validate:

- HUD calls `Request`, not `Process`
- `Request` calls `Check`
- `Check` is read-only
- `Process` owns mutation
- failure does not cause partial mutation
- result handling is structured
- one-time actions are idempotent or protected against duplicate processing

### `review-production-readiness`

Use when:

- demo handlers are replaced
- real rewards or currency are granted
- real persistence is connected
- existing database schema is modified
- integration is intended for release
- consumer business logic is introduced

It must check:

- no demo-only components remain silently active
- required adapters exist
- rollback is documented
- known limitations are documented
- integration behavior matches consumer requirements

### Mandatory Constraint

Do not create module-specific review skills when a reusable global review skill is sufficient.

## 7. `SKILL.md` Responsibilities

### Mandatory `SKILL.md` Contents

Each `SKILL.md` must remain compact and act as a workflow controller.

It must contain:

1. Purpose
2. Trigger conditions
3. Required inputs
4. Expected outputs
5. Path validation requirement
6. Main workflow
7. Code-tracing order
8. Conditions for invoking reusable review skills
9. Conditions for loading each reference
10. Files allowed to inspect
11. Files allowed to modify
12. Required evidence
13. Stop conditions
14. Report output format

### `SKILL.md` Workflows

`SKILL.md` files contain workflow instructions, not long checklists.

### Mandatory Constraint

Do not place long checklists directly in `SKILL.md`.

Long checklists belong in:

```text
references/
```

## 8. Progressive Reference-Loading Strategy

### Mandatory Strategy

References must be loaded conditionally.

Examples:

```text
Read references/dependency-analysis.md before designing the generic module.
```

```text
Read references/demo-requirements.md when the feature includes UI,
configuration, user actions, persistence, or external integrations.
```

```text
Invoke review-data-lifecycle and read its lifecycle references when the
module loads, saves, caches, reconnects, or modifies persistent player data.
```

```text
Read references/consumer-kit-template.md only after the generic module
and its runnable demo pass validation.
```

### Expected Loading Flow

```text
AGENTS.md
    ->
Global router
    ->
One module workflow skill
    ->
Applicable reusable review skills
    ->
Only relevant references
    ->
Repository source files
```

### Mandatory Constraint

Codex must not load all references by default.

## 9. Required Project Structure

### Mandatory Structure

```text
ProjectRoot/
├── AGENTS.md
├── .codex/
│   ├── project-paths.json
│   └── skills/
│       ├── source-to-shared-router/
│       ├── shared-to-consumer-router/
│       ├── [module]-source-to-shared/
│       ├── [module]-shared-to-consumer/
│       ├── review-data-lifecycle/
│       ├── review-request-check-process/
│       └── review-production-readiness/
└── reports/
```

### Roles

- Global routers
- One source-to-shared skill per module
- One shared-to-consumer skill per module
- Reusable cross-module review skills
- Long references loaded only when relevant
- Generated reports stored outside skill folders

## 10. Project Path Configuration

### User-Managed Local Path Configuration

Remove automatic filesystem discovery as the default project-selection behavior.

The user must configure project paths manually in:

```text
ProjectRoot/.codex/project-paths.json
```

### Recommended Schema

```json
{
  "projects": {
    "steal_a_pet": {
      "path": "../StealAPet",
      "access": "read-only"
    },
    "shared_libs": {
      "path": ".",
      "access": "read-write"
    },
    "consumer_project": {
      "path": "",
      "access": "read-write"
    }
  }
}
```

### Allowed Path Types

The path may be:

- repository-relative
- absolute local path

Relative paths are recommended when the repositories have a stable sibling layout.

### Mandatory Constraint

The configuration file is user-managed.

Codex may create a template only if the user explicitly asks to initialize the Codex configuration.

Codex must not invent or silently change project paths.

## 11. Path-Validation Workflow

### Mandatory First Step

Path validation must be the first step of every inheritance task.

### Source-to-Shared Required Paths

```text
projects.steal_a_pet.path
projects.shared_libs.path
```

### Shared-to-Consumer Required Paths

```text
projects.shared_libs.path
projects.consumer_project.path
```

### Mandatory Validation Steps

Before reading or modifying module files, Codex must:

1. Read `.codex/project-paths.json`
2. Verify that all required entries exist
3. Resolve relative paths from the directory containing the config file
4. Normalize path separators
5. Verify that each directory exists
6. Verify expected repository markers
7. Verify that source and target paths are different
8. Verify source and target access policies
9. Stop before writing if validation fails

## 12. Repository Marker Validation

### Mandatory Principle

Do not trust a configured folder only because the path exists.

### Suggested Steal A Pet Markers

Use a combination of repository evidence such as:

```text
Assets/Scripts/Manager/
Assets/Scripts/Configs/
Assets/Scripts/Utils/
Assets/Scripts/SharedLibs/
```

For a requested module, verify its source file when possible.

Example for Activities:

```text
Assets/Scripts/Manager/ActivitiesManager.fcg
```

### Suggested SharedLibs Markers

Use evidence such as:

```text
AGENTS.md
.codex/skills/
Assets/Scripts/Managers/
Assets/Scripts/HUDs/
Assets/Scripts/Configs/
Assets/Scripts/Utils/
```

Some folders may not exist before initial setup.

During initial setup, the target may instead be validated by:

- a valid project root
- a repository marker
- explicit target configuration
- permission to create the required SharedLibs structure

### Suggested Consumer Project Markers

Consumer project validation should use:

- existing repository markers
- existing asset or script roots
- explicit configured target
- consumer architecture evidence

Do not require the consumer project to already use the SharedLibs folder structure before integration.

## 13. Invalid-Path Behavior

### Missing Configuration File

If `.codex/project-paths.json` does not exist, Codex must stop and report:

```text
Project path configuration was not found.

Expected configuration:
.codex/project-paths.json

No project files were modified.

Create or update the configuration file before running module inheritance.
```

Codex may create a template only when the user explicitly asks it to initialize the Codex configuration.

### Invalid Configured Path

If a required path is empty, missing, inaccessible, or invalid, Codex must stop and report:

- configuration key
- configured path
- expected repository markers
- missing or mismatched markers
- configuration file to update
- confirmation that no project files were modified

Example:

```text
Configured Steal A Pet project could not be validated.

Configuration key:
projects.steal_a_pet.path

Configured path:
C:/Projects/StealAPet

Expected marker:
Assets/Scripts/Manager/

Requested module marker:
Assets/Scripts/Manager/ActivitiesManager.fcg

No project files were modified.

Update:
.codex/project-paths.json
```

### Mandatory Prohibitions

Codex must not:

- search the entire filesystem
- silently select a different repository
- fall back to a similarly named folder
- modify an unverified target
- automatically rewrite the configured path

## 14. Access and Write-Safety Rules

### Access Policies

The config should define intended access:

- `read-only`
- `read-write`

### Source Repositories

For source-to-shared inheritance:

- `steal_a_pet = read-only`
- `shared_libs = read-write`

For shared-to-consumer inheritance:

- `shared_libs = read-only`
- `consumer_project = read-write`

Codex must treat source repositories as read-only unless the user explicitly requests source changes.

### Target Repositories

Before writing, Codex must confirm that:

- the target is configured as `read-write`
- the source and target do not resolve to the same root
- files being changed belong to the intended target

### Mandatory Write-Safety Rule

Do not modify files when path validation fails.

## 15. Configuration and Version-Control Safety

### Recommended Configuration Pattern

Provide a committed template:

```text
.codex/project-paths.example.json
```

Store real user paths in:

```text
.codex/project-paths.json
```

Add the real config to `.gitignore` when it contains machine-specific absolute paths.

### Example Template

```json
{
  "projects": {
    "steal_a_pet": {
      "path": "../StealAPet",
      "access": "read-only"
    },
    "shared_libs": {
      "path": ".",
      "access": "read-write"
    },
    "consumer_project": {
      "path": "",
      "access": "read-write"
    }
  }
}
```

### Mandatory Constraint

Do not place machine-specific absolute paths inside:

- `AGENTS.md`
- `SKILL.md`
- portability manifests
- module documentation
- generated reusable references

Generated reports may mention resolved paths only when needed for execution evidence, but repository-relative paths should be preferred.

## 16. `AGENTS.md` Responsibilities

### Mandatory Responsibilities

Keep `AGENTS.md` concise.

It should contain:

- available global routers
- available module workflow skills
- available reusable review skills
- short routing descriptions
- rules for combining module skills with review skills
- instruction that project paths come from `.codex/project-paths.json`

### Mandatory Prohibitions

It must not contain:

- actual machine-specific paths
- long checklists
- full workflows
- full module documentation
- incident histories
- detailed path-validation procedures

### Routing Metadata

`AGENTS.md` is routing metadata.

Detailed path-validation behavior belongs in relevant `SKILL.md` files or shared references.

## 17. Source-to-Shared Workflow

### Source Repositories

- `StealAPet` is the source repository
- `SharedLibs` is the target repository

### Mandatory Workflow

```text
Read .codex/project-paths.json
    ->
Validate steal_a_pet and shared_libs roots
    ->
source-to-shared-router
    ->
Select [module]-source-to-shared
    ->
Run applicable reusable reviews
    ->
Generate reports
```

### Responsibilities of `[module]-source-to-shared`

This skill must:

- analyze the source module
- trace dependencies
- trace feature flow
- separate generic and Steal A Pet-specific logic
- implement the generic shared module
- create a runnable demo
- generate documentation
- generate portability manifest
- generate downstream consumer integration references
- preserve `Request -> Check -> Process`
- produce inheritance and review reports

## 18. Shared-to-Consumer Workflow

### Source and Target Repositories

- `SharedLibs` is the source repository
- `Consumer Project` is the target repository

### Mandatory Workflow

```text
Read .codex/project-paths.json
    ->
Validate shared_libs and consumer_project roots
    ->
shared-to-consumer-router
    ->
Select [module]-shared-to-consumer
    ->
Run applicable reusable reviews
    ->
Generate integration and rollback reports
```

### Responsibilities of `[module]-shared-to-consumer`

This skill must:

- read the portability manifest
- read public contracts and extension points
- analyze the consumer project
- map shared contracts to consumer systems
- adapt consumer business logic
- replace demo handlers
- integrate persistence
- integrate UI
- preserve `Request -> Check -> Process`
- validate production readiness
- generate consumer integration and rollback reports

### Mandatory Constraint

Do not access Steal A Pet during shared-to-consumer integration.

## 19. Activities Example

### Source-to-Shared

User prompt:

```text
Inherit Activities from Steal A Pet into the shared project.
```

Codex workflow:

```text
Read .codex/project-paths.json
    ->
Validate steal_a_pet and shared_libs roots
    ->
source-to-shared-router
    ->
activities-source-to-shared
    ->
review-request-check-process
    ->
review-data-lifecycle
```

The `activities-source-to-shared` skill must:

- analyze `ActivitiesManager`
- trace related HUD, Config, Utils, database, and Manager dependencies
- separate generic and Steal A Pet-specific logic
- implement the generic Activities module
- create one daily-login demo
- use notification-only or mock rewards
- generate the portability manifest
- generate Activities downstream integration references
- produce inheritance and review reports

### Shared-to-Consumer

User configures:

```json
{
  "projects": {
    "shared_libs": {
      "path": "../SharedLibs",
      "access": "read-only"
    },
    "consumer_project": {
      "path": "../GameB",
      "access": "read-write"
    }
  }
}
```

User prompt:

```text
Add the shared Activities feature to this game and connect it to the existing wallet and player database.
```

Codex workflow:

```text
Read .codex/project-paths.json
    ->
Validate shared_libs and consumer_project roots
    ->
shared-to-consumer-router
    ->
activities-shared-to-consumer
    ->
review-request-check-process
    ->
review-data-lifecycle
    ->
review-production-readiness
```

### Demo-Only Behavior

The shared Activities demo may:

- use notification-only rewards
- use mock handlers
- use minimal mock config

### Production Integration Behavior

The consumer workflow must replace demo reward handlers and connect to real wallet and database systems before release.

## 20. Reports

### Mandatory Reports Location

Generated reports must be stored under:

```text
ProjectRoot/reports/
```

### Mandatory Distinction

Generated reports are outputs, not instructions.

Do not place generated reports inside:

- `.codex/skills`
- `AGENTS.md`
- `SKILL.md`
- reusable references

### Recommended Report Layout

```text
reports/
  inheritance/
    [module-name]/
      source-analysis.md
      inheritance-report.md
      portability-report.md

  reviews/
    [module-name]/
      request-check-process-review.md
      lifecycle-review.md
      production-readiness-review.md

  consumer-integrations/
    [consumer-project]/
      [module-name]/
        integration-report.md
        validation-report.md
        rollback-plan.md
```

## 21. Updated Module Completion Definition

### Mandatory Completion Rule

A module is not complete until Codex has created or updated, in a future implementation task:

1. Generic module implementation
2. Runnable demo
3. Mock or example config
4. Documentation
5. Portability manifest
6. One module-specific source-to-shared skill
7. One module-specific shared-to-consumer skill
8. Required entries in both global routers
9. Required entries in `AGENTS.md`
10. Relevant reusable review integration
11. Conditional references
12. Inheritance reports
13. Review reports
14. Consumer integration templates
15. Validation that all skill and reference links resolve

### Mandatory Constraint

Do not require separate module-specific analysis, implementation, review, and consumer-kit skills unless a documented complexity reason justifies the split.

## 22. Validation Checklist

### Skill Architecture Validation

- only two module-specific workflow skills exist by default per module
- module-specific routers are not created unless justified
- reusable review skills are used where possible

### Path Configuration Validation

- `.codex/project-paths.json` exists or the task stops safely
- required config keys exist
- relative paths are resolved from the config directory
- source and target roots differ
- access policies are valid

### Repository Validation

- expected repository markers exist
- requested module markers exist when applicable
- source repository is treated as read-only
- target repository is confirmed as read-write

### Safety Validation

- no file modifications occur if path validation fails
- no automatic filesystem-wide search is performed
- no configured path is silently rewritten
- no source repository is modified unintentionally

### Workflow Validation

- source-to-shared workflow uses the global router plus one module workflow skill
- shared-to-consumer workflow uses the global router plus one module workflow skill
- applicable reusable review skills are invoked
- shared-to-consumer flow does not access Steal A Pet

### Completion Validation

- demo exists
- portability manifest exists
- `AGENTS.md` entries exist
- both global routers reference valid module skills
- reports are generated in `reports/`
- all skill and reference links resolve

## 23. Recommended Directory Structure

```text
ProjectRoot/
├── AGENTS.md
├── .codex/
│   ├── project-paths.json
│   ├── project-paths.example.json
│   └── skills/
│       ├── source-to-shared-router/
│       │   └── SKILL.md
│       ├── shared-to-consumer-router/
│       │   └── SKILL.md
│       ├── activities-source-to-shared/
│       │   ├── SKILL.md
│       │   └── references/
│       ├── activities-shared-to-consumer/
│       │   ├── SKILL.md
│       │   └── references/
│       ├── mail-source-to-shared/
│       │   ├── SKILL.md
│       │   └── references/
│       ├── mail-shared-to-consumer/
│       │   ├── SKILL.md
│       │   └── references/
│       ├── review-data-lifecycle/
│       │   ├── SKILL.md
│       │   └── references/
│       ├── review-request-check-process/
│       │   ├── SKILL.md
│       │   └── references/
│       └── review-production-readiness/
│           ├── SKILL.md
│           └── references/
└── reports/
    ├── inheritance/
    ├── reviews/
    └── consumer-integrations/
```

### Distinctions

- Global routers:
  - `source-to-shared-router`
  - `shared-to-consumer-router`
- Module-specific workflow skills:
  - `[module]-source-to-shared`
  - `[module]-shared-to-consumer`
- Reusable review skills:
  - `review-data-lifecycle`
  - `review-request-check-process`
  - `review-production-readiness`
- Conditional references:
  - inside each skill's `references/`

## 24. Token-Efficiency Review

### Mandatory Principles

- keep `AGENTS.md` concise
- keep each `SKILL.md` compact
- avoid eight-skill-per-module expansion
- reuse global review skills
- store long checklists in `references/`
- load references only when conditions apply
- avoid loading unrelated module references
- avoid loading reports as permanent instructions

### Expected Progressive Flow

```text
AGENTS.md
    ->
Global router
    ->
One module workflow skill
    ->
Applicable reusable review skills
    ->
Only relevant references
    ->
Repository source files
```

### Mandatory Constraint

Do not put every checklist into one large Markdown file.

Do not create unnecessary routing complexity through overly fragmented module skills.

## 25. Open Questions

- Should path validation logic live only inside each `SKILL.md`, or should there also be one reusable path-validation reference shared by routers and module workflow skills?
- Should the portability manifest have a single shared schema across all modules, or allow module-specific extensions on top of a core contract?
- Should `review-production-readiness` also validate portability-manifest completeness, or should that remain part of the module workflow skill?
- For simple non-persistent modules, should `review-data-lifecycle` be entirely skipped by default, or run in a reduced mode that confirms no hidden lifecycle coupling exists?
- When a consumer project has a very different folder layout, what minimum set of consumer markers should be considered sufficient for safe validation without overfitting to one architecture?
