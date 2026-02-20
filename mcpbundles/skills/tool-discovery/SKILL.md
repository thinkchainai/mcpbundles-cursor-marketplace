---
name: tool-discovery
description: Discover and use MCPBundles tools. Use when finding integrations,
  exploring tools, or checking what services are connected.
---
# Tool Discovery

1. `list_bundles` — see enabled integrations. Use `include_inactive=true` for bundles needing credentials.
2. `search_tools(query="...")` — natural language search across all tools. Use action queries ("send email", "list tables"), not service names.
3. `get_tool_info(function_name="...")` — full parameter docs. Call before using tools with 3+ parameters.
4. `check_readiness(bundle_slug="...")` — confirm credentials before calling tools. Omit slug to check all.

- On auth errors, call `check_readiness` before retrying.
- Parse JSON responses and present relevant fields — never dump raw JSON.
- Some tools return MCP UI Apps (interactive dashboards, forms, charts) rendered inline.
