# Claude skills

Reviewed: 2026-09-11. English audit-oriented summary, not a full document mirror.
Source: [Claude skills](https://code.claude.com/docs/en/skills). Source URLs are provenance only; do not fetch during an offline audit.

A skill supplies reusable instructions or knowledge through `SKILL.md`, with YAML frontmatter and a Markdown body. Its description helps selection; the body is loaded when used. Supporting references and scripts can accompany the entrypoint.

A skill can contain a multistep workflow. It need not become an agent merely because it performs several operations. Claude-specific options can control invocation and execute a skill in a separate subagent context, including `context: fork`. These extensions are not automatically portable to other hosts.

Plugin skills use namespaced invocation. Similar names alone do not prove a collision: inspect the actual namespace and scope behavior.

Keep references available within the distributed skill. Load only relevant references rather than every document for every task. Evaluate whether invocation descriptions distinguish neighboring skills and whether supporting files preserve the intended procedure. Separate declaration-level review from observed selection behavior.
