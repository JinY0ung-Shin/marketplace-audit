# Boundary judgments and counterexamples

## Decision procedure

1. Identify result ownership and ownership of methods and service contracts.
2. Check whether the same rule can be independently changed in multiple locations.
3. Consider changes to procedures, APIs, and assigned responsibilities separately. Explain the resulting edit scope and potential inconsistency.
4. Look for reasons supporting the current placement: permission/context isolation, transactions, performance, or reuse.
5. Report a defect or recommendation only when concrete evidence supports it over the current design.

## Important counterexamples

| Observation | Why it is not automatically a defect | Additional evidence indicating a problem |
| --- | --- | --- |
| An agent contains a procedure | A short procedure unique to one role can be appropriate | Independent copies drift or conflict |
| A skill performs multiple steps | Skills can include workflows and scripts | Work requiring isolated permissions/state shares a context |
| A skill runs in a fork | Execution placement and knowledge ownership are separate axes | Unnecessary isolation causes missing inputs or lost results |
| An MCP tool combines APIs | Atomicity, consistency, latency, and domain contracts may justify aggregation | Overlapping judgment or unclear ownership causes conflicts or retry side effects |
| An MCP service uses an LLM | An agent-as-tool service may have an explicit contract | Hidden judgment scope, errors, or completion conditions conflict with the caller |
| An MCP server provides prompts | Prompts and resources are supported protocol concepts | The same business rule has independent copies in prompts and skills |
| A skill includes local calculation code | Service deployment may be unnecessary without broader reuse | Calculations are regenerated from prose on each request and become inconsistent |
| Multiple plugins use one MCP server | Sharing a common service is normal | Duplicate server processes or incompatible contracts/versions are assumed |
| Components share a name | Namespace/scope may resolve them | Actual host resolution causes shadowing or misrouting |
| The dependency graph has a cycle | It may represent documentation links or bounded review iterations | An executable cycle lacks stopping or call-budget conditions |
| JSON differs from a documentation example | Runtime versions or extensions may differ | The installed schema or runtime rejects it |

## Examples

- If agent and skill instructions specify different minimum sample sizes for the same comparison group, report a confirmed rule-ownership conflict with both locations. Do not choose the correct value without business evidence.
- `get_investigation_bundle(lot_id)` can be a valid contract that aggregates history. Do not automatically recommend splitting it into CRUD operations.
- Descriptions that all say “use for data analysis” create routing risk. Without traces, do not claim observed misrouting. Suggest distinguishing inputs, deliverables, and boundary requests.
- A skill instruction to obtain approval before writing is a workflow rule. Whether a server permits unauthorized writes requires separate evidence. Prose alone also does not demonstrate server security.
- MCP configuration alone can establish endpoint and environment-variable references, but server-side authentication, schemas, and retry guarantees remain unverified.
