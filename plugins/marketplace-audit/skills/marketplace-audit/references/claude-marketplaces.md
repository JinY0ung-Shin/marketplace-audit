# Claude marketplaces

Reviewed: 2026-09-11. English audit-oriented summary, not a full document mirror.
Source: [Claude marketplaces](https://code.claude.com/docs/en/plugin-marketplaces). Source URLs are provenance only; do not fetch during an offline audit.

A marketplace distributes a catalog of plugins; it does not define their runtime responsibilities. The usual catalog location is `.claude-plugin/marketplace.json`. Its required top-level fields are `name`, `owner`, and `plugins`; entries identify a plugin with `name` and `source`. Local sources resolve within the marketplace checkout.

Keep packaged dependencies inside the installed plugin. An external sibling file that exists in a development checkout may disappear when the plugin is cached. Distinguish source availability from runtime compatibility.

Run `claude plugin validate <marketplace-path>` when supported. Marketplace validation and component validation have different coverage: also validate individual plugin directories. Record warnings and skipped files. Installed-version behavior takes precedence over this summary.

For disconnected distribution, transfer the complete repository and add its local directory using `/plugin marketplace add /absolute/path/to/marketplace-audit`. Install with `/plugin install marketplace-audit@marketplace-audit`. GitHub access is unnecessary for this local catalog; dependencies and the model runtime may still require connectivity.
