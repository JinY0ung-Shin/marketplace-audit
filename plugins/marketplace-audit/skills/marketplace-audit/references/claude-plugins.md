# Claude plugins

Reviewed: 2026-09-11. English audit-oriented summary, not a full document mirror.
Source: [Claude plugins](https://code.claude.com/docs/en/plugins). Source URLs are provenance only; do not fetch during an offline audit.

A plugin packages related extensions for installation and distribution. Its manifest belongs in `.claude-plugin/plugin.json`; component directories such as `skills/`, `agents/`, and `hooks/` belong at the plugin root, not inside `.claude-plugin/`.

Skills are addressed using the plugin namespace. Packaging related components together does not make their responsibilities identical. A plugin may contain only a skill; an agent, hook, or MCP server is not mandatory.

Use explicit version metadata for releases and update it when distributing changed behavior. Validate the plugin directory using a compatible locally installed CLI. A successful manifest check does not demonstrate correct task execution.

Inspect both conventional directories and configured component paths. Runtime-specific discovery, caching, supported fields, and reload behavior require matching local documentation or implementation evidence. Do not impose another host’s manifest conventions on a Claude plugin.
