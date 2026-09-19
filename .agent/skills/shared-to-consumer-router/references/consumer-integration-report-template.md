# Consumer Integration Report Template

Every shared-to-consumer report must include:

1. Module
2. Source project
3. Target project
4. Repository evidence inspected
5. Active implementation selected
6. Deprecated implementations excluded
7. Source files cloned
8. Source files omitted
9. Serialized assets discovered
10. Serialized asset fidelity
11. Entity or asset ID handling
12. Serialized bindings preserved
13. Dependency closure
14. Missing dependencies
15. Config fidelity
16. CSV fidelity
17. Data lifecycle fidelity
18. Public API fidelity
19. Source-specific dependencies
20. Genericization changes
21. Utilities reused
22. Interfaces introduced
23. Adapters introduced and justification
24. Files organized by layer
25. Demo artifacts omitted
26. Serialized clone status
27. Runtime verification status
28. MCP usage
29. Remaining Studio-only verification gaps
30. Remaining consumer integration work
31. Stage completion summary
32. Safe files created
33. Safe files modified
34. Faithful clone status
35. Clone fidelity status
36. Standalone portability status
37. Runtime verification evidence and pending checks
38. Utility dependency analysis
39. Texture dependency analysis
40. Custom enum inventory
41. Custom component inventory
42. Definitions found in repository
43. Values preserved unchanged
44. Values remapped
45. Values unresolved but preserved
46. Exact MCP blockers
47. Work completed without MCP
48. Work remaining with Studio
49. Consumer adaptation requirements

For this direction, `Source project` is SharedLibs, `Target project` is the consumer,
and `Genericization changes` records consumer-specific adaptations. Use
repository-first evidence labels and include
`serialized-asset-fidelity-review.md` and
`asset-dependency-closure-review.md` when applicable.

Never represent pending live runtime verification as failed filesystem integration.
Do not report the whole integration blocked when independent safe stages complete.
