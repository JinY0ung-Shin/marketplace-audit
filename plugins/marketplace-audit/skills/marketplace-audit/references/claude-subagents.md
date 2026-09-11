# Claude subagents

Reviewed: 2026-09-11. English audit-oriented summary, not a full document mirror.
Source: [Claude subagents](https://code.claude.com/docs/en/sub-agents). Source URLs are provenance only; do not fetch during an offline audit.

Subagents provide specialized execution contexts. Their definitions describe when to delegate and what instructions govern their work; configuration can select tools and models. Separate contexts help isolate intermediate work and return results to the caller.

A custom subagent definition combines frontmatter and instructions. Audit the declared task, available capabilities, expected inputs, and returned result. Compare those declarations with actual runtime configuration when available.

Use a distinct agent when independent execution context or capability selection serves the task. Reusable procedural knowledge can remain in skills. Do not infer a universal inheritance or skill-loading rule from a reference to another component; confirm the installed runtime’s behavior.

Delegation descriptions affect selection but do not demonstrate successful routing. Assess whether the parent receives enough evidence to continue and whether any repeated delegation has clear stopping conditions. These architectural checks require task-specific evidence beyond valid metadata.
