---
name: agent-operations
description: Manage MCPBundles autonomous agents. Use when creating agents,
  reviewing run history, or debugging agent failures.
---
# Agent Operations

## Create

`upsert_agent(name, agents_md_content, heartbeat_md_content, mcp_source={"type":"bundle","bundle_slug":"..."}, ai_provider, model_name, heartbeat_interval_minutes, is_active, max_tool_calls_per_run)`

## Skills

`upsert_agent_skill(agent_id, skill_name, skills_md_content)` — add composable instructions to an agent's prompt. `delete_agent_skill(id)` to remove.

## Monitor

- `list_agents` — all agents with status and last heartbeat.
- `list_agent_runs(agent_id="...")` — run history with status, duration, tool calls, tokens, errors.
- `trigger_agent_run(agent_id="...")` — manual run, returns run ID.

## Debug failures

1. `list_agent_runs(agent_id="...", status="error", limit=5)` — find failed runs.
2. `list_agent_runs(id="...")` — full run details and error output.
3. `check_readiness(bundle_slug="...")` — is the MCP source bundle ready?
4. `list_executions(heartbeat_run_id="...")` — tool executions from that run.

## Lifecycle

Pause: `upsert_agent(id, is_active=false)`. Resume: `is_active=true`. Delete: `delete_agent(id)`.
