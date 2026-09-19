# Inventory utility-reuse review

| Helper | Source behavior | Target decision | Rationale |
|---|---|---|---|
| `DataUtils.JsonStringToListKeyValueV2` | Parse top-level structured objects | Reuse existing utility | Signature and delimiter behavior match target |
| `DataUtils.StringToListIntV2` | Parse comma-separated weather IDs | Reuse existing utility | Preserves source weather encoding |
| `DataUtils.ListIntToStringUseComma` | Serialize weather IDs | Reuse existing utility | Preserves comma encoding |
| `DataUtils.ListKeyValueToJsonString` | Serialize pet records | Reuse existing utility | Preserves source record format |
| `BigNumberHandler` conversion/arithmetic | list-based arbitrary-size numbers | Copy source utility | No target equivalent existed; balance correctness depends on it |

No feature-specific parser wrapper or duplicate generic utility was added.
