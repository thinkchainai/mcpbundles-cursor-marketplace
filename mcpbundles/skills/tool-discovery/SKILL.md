---
name: tool-discovery
description: Discover and use MCPBundles tools effectively. Use when the user
  wants to find integrations, explore available tools, or understand what
  services are connected in their workspace.
---
# Tool Discovery

## Discovery workflow

1. **Start with `list_bundles`** to see what integrations are enabled. Each bundle groups tools for a service (e.g., HubSpot CRM, Stripe Payments). Pass `include_inactive=true` to also see bundles that need credentials.

2. **Use `search_tools` for natural language lookup.** If the user says "send an email" or "list database tables", pass their intent directly as the `query` parameter. This uses hybrid keyword + semantic search across all available tools.

3. **Use `get_tool_info` before calling complex tools.** Pass the tool's `function_name` to get full parameter documentation. Do this whenever a tool has more than 2-3 parameters or when you're unsure about required vs optional fields.

4. **Use `check_readiness` to confirm credentials are configured** before attempting tool calls. Pass a `bundle_slug` to check a specific service, or omit it to check all bundles at once.

## Best practices

- Always call `list_bundles` at the start of a session when the user asks about their integrations or what tools are available.
- When a tool call fails with an authentication error, call `check_readiness(bundle_slug="...")` before retrying.
- Use `search_tools` with action-oriented queries ("create a contact", "query sales data") rather than service names ("hubspot", "stripe").
- Tools return structured JSON. Parse the response and present the relevant fields to the user — don't dump raw JSON.
- Some tools return MCP UI Apps (interactive HTML dashboards, forms, charts). These render directly in the conversation.
