# MCPBundles — Cursor Marketplace Plugins

Connect Cursor to **500+ services** through [MCPBundles](https://mcpbundles.com) — hosted MCP servers with built-in authentication, team credential management, and full operational visibility.

## What is MCPBundles?

MCPBundles is a hosted platform that turns third-party APIs into AI-ready MCP tools. Instead of wiring up auth, managing tokens, and writing glue code, you get pre-built MCP servers for services like HubSpot, Stripe, Gmail, Slack, Postgres, and hundreds more.

**Key capabilities:**

- **500+ pre-built integrations** — CRM, payments, email, databases, analytics, project management, and more
- **MCP UI Apps** — rich interactive UIs rendered directly in the AI conversation (dashboards, forms, charts)
- **Programmatic tool execution** — call any tool via API for automation pipelines, scheduled jobs, and agent workflows
- **Team & workspace credential management** — centralized OAuth and API key management with per-user and per-workspace scoping
- **Agent runs & operations** — track agent executions, tool call history, durations, and error states
- **Tool execution visibility & audit trail** — full observability into what tools ran, who triggered them, and what happened

## Quick Start

1. **Install the plugin** from the Cursor Marketplace
2. **Sign in** — Cursor handles OAuth automatically, opening a browser to authorize your MCPBundles account

Once authorized, your Cursor agent can call tools across all the services you've connected in your MCPBundles workspace.

## Available Services

HubSpot · Stripe · Gmail · Google Sheets · Google Drive · Google Calendar · Slack · Postgres · MySQL · MongoDB · GitHub · Jira · Linear · Notion · Airtable · Intercom · Zendesk · Figma · Datadog · PostHog · Sentry · and [500+ more](https://mcpbundles.com/providers).

## Configuration

The plugin adds an MCP server that connects to your MCPBundles hub via OAuth:

```json
{
  "mcpServers": {
    "mcpbundles": {
      "url": "https://mcp.mcpbundles.com/hub/"
    }
  }
}
```

Cursor discovers the OAuth endpoints automatically via `/.well-known/oauth-authorization-server` and performs PKCE authorization on first connect.

## Links

- [MCPBundles](https://mcpbundles.com)
