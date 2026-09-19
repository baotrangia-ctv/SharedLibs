# Intake Record Template (00-intake.md)

Every source-to-shared inheritance must create this record at
`reports/inheritance/[module]/00-intake.md` before touching any file outside
`reports/`. Include:

1. Module name(s) covered by this request
2. Confirmed route: `source-to-shared-router` (source project -> SharedLibs)
3. Validated source root and access mode
4. Validated SharedLibs root and access mode
5. Selected `[module]-source-to-shared` skill, or a note that it must be
   created from templates
6. Required Common References actually opened, listed by path (from this
   router's `# Required Common References` section)
7. User-specified exclusions (named sub-features to leave out of this module)
8. Dependency-closure check result for each exclusion: does the excluded
   feature share a Manager, config, utility, or serialized asset with the
   included scope? List every shared touch point found, or state none found
9. Any Stop Condition triggered and how it was resolved

Do not proceed to repository-first discovery or Stage A cloning until this
file exists with every field filled in.
