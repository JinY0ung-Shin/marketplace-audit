# Offline reference pack

Reviewed: 2026-09-11. This pack contains concise, independently worded summaries of the five official documents previously linked from SKILL.md. It is not a full mirror or a complete versioned schema. Audit-specific recommendations are design heuristics, not additional platform requirements.

## Read the relevant local document

| Review concern | Local reference |
| --- | --- |
| Catalog structure, sources, local installation, validator coverage | [Claude marketplaces](claude-marketplaces.md) |
| Plugin layout and packaging | [Claude plugins](claude-plugins.md) |
| Skill selection, supporting content, fork execution | [Claude skills](claude-skills.md) |
| Delegation, execution context, capability configuration | [Claude subagents](claude-subagents.md) |
| Tools, resources, prompts, service boundaries | [MCP server concepts](mcp-server-concepts.md) |

## Offline behavior

- Treat local references as the normal documentation route. Do not open source URLs, search the web, install packages, or attempt network access merely to complete an audit.
- Prefer actual installed-version schemas, local help, vendored documentation, and implementation over this dated reference pack.
- When evidence conflicts, report the local version and mismatch. When a version-dependent fact cannot be resolved, mark that fact unverified and continue the rest of the audit.
- Do not require the user to enable internet access. Request only the specific missing local artifact if it would resolve a material finding.
- Source URLs are retained for provenance and optional maintainer refresh. Update these summaries only in a separately requested documentation maintenance task with permitted network access; record the review date and affected facts.
- This removes the audit’s external documentation dependency, not the host model’s connectivity requirements or the target system’s own dependencies.
