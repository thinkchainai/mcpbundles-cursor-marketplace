---
name: agent-operations
description: Manage MCPBundles autonomous agents — create, configure, monitor,
  and debug agents that run on schedules or on-demand. Use when the user wants
  to set up automated workflows, review agent run history, or troubleshoot
  agent failures.
---
# Agent Operations

## Creating an agent

Use `upsert_agent` to create a new agent. Required: `name`. Key fields:

- `agents_md_content`: The agent's instructions (what it should do, how it should behave).
- `heartbeat_md_content`: The checklist the agent evaluates on each run.
- `mcp_source`: The MCP bundle the agent uses for tool access. Format: `{"type": "bundle", "bundle_slug": "..."}`.
- `ai_provider` / `model_name`: The AI model to use (e.g., `"anthropic"` / `"claude-sonnet-4-20250514"`).
- `heartbeat_interval_minutes`: How often the agent runs (e.g., `60` for hourly).
- `is_active`: Set to `true` to enable scheduled runs.
- `max_tool_calls_per_run` / `max_total_tokens_per_run`: Execution limits.

## Adding skills to agents

Use `upsert_agent_skill` to add reusable instruction sets:

- `agent_id`: The agent to add the skill to.
- `skill_name`: A descriptive name.
- `skills_md_content`: Markdown instructions injected into the agent's prompt alongside its definition.

Skills are composable — an agent can have multiple skills that each add specialized knowledge.

## Monitoring agents

- **`list_agents`**: See all agents, their status, and last heartbeat time. Filter by `is_active`, `status`, or `search`.
- **`list_agent_runs(agent_id="...")`**: See an agent's execution history — status, duration, tool calls made, token usage, and errors.
- **`list_agent_runs(id="...")`**: Get a single run's full details including the summary and any error output.
- **`trigger_agent_run(agent_id="...")`**: Manually trigger a run right now, regardless of schedule. Returns the run ID for monitoring.

## Debugging agent failures

1. Call `list_agent_runs(agent_id="...", status="error", limit=5)` to find failed runs.
2. Get the full run details with `list_agent_runs(id="...")` — look at the run summary and error fields.
3. Check if the agent's MCP source bundle is ready with `check_readiness(bundle_slug="...")`.
4. Review the tool executions from that run with `list_executions(heartbeat_run_id="...")`.

## Lifecycle management

- **Pause**: `upsert_agent(id="...", is_active=false)` to stop scheduled runs.
- **Resume**: `upsert_agent(id="...", is_active=true)`.
- **Delete**: `delete_agent(id="...")` permanently removes the agent and all run history.
- **Remove a skill**: `delete_agent_skill(id="...")`.
