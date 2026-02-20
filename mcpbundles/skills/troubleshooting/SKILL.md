---
name: troubleshooting
description: Debug MCPBundles tool failures and credential issues. Use when a
  tool call fails or an integration isn't working.
---
# Troubleshooting

When a tool call fails:

1. `check_readiness(bundle_slug="...")` — are credentials configured?
2. `validate_bundle(bundle_slug="...")` — real API connectivity test.
3. `list_executions(bundle_slug="...", status="error", limit=5)` — recent failures with error details.
4. `list_executions(id="...")` — full details for a specific execution.
5. `list_credentials(provider_slug="...")` — credential verification status and granted scopes.

**Error patterns**: 401/403 = expired credentials or insufficient scopes, re-authenticate in MCPBundles. 404 = bad resource ID. 429 = rate limited, wait and retry. Tool not found = wrong slug or bundle not enabled, use `search_tools`.

**Credential statuses**: verified = working. unverified = untested. failed = last check failed. expired = needs re-auth.
