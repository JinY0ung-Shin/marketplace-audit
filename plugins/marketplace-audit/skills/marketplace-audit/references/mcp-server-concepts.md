# MCP server concepts

Reviewed: 2026-09-11. English audit-oriented summary, not a full document mirror.
Source: [MCP server concepts](https://modelcontextprotocol.io/docs/2026-07-28/learn/server-concepts). Source URLs are provenance only; do not fetch during an offline audit.

MCP servers expose tools, resources, and prompts. Tools provide callable operations, resources expose contextual data, and prompts supply reusable interaction templates. MCP therefore includes more than API execution.

A server definition or connection URL is not evidence of the tool schemas actually exposed or the server’s implementation. Inspect available contracts and results separately. Tool operations can retrieve information or change external state; distinguish these behaviors when reviewing a workflow.

Prompts can overlap conceptually with skill instructions. The audit should identify which component owns a business rule rather than declaring every server prompt inappropriate.

The protocol’s abstractions do not determine a project’s business responsibility boundaries. Aggregated operations or agent-backed tools may be appropriate if their inputs, outputs, errors, and responsibilities are explicit. Verify implementation-level guarantees with actual code, configuration, or execution evidence rather than inferring them from naming.
