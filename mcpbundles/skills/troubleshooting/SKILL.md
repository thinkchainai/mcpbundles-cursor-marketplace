---
name: troubleshooting
description: Debug MCPBundles tool failures, credential issues, and connectivity
  problems. Use when a tool call fails, returns unexpected errors, or the user
  reports that an integration isn't working.
---
# Troubleshooting

## Diagnostic workflow

When a tool call fails, follow this sequence:

1. **Check credentials** — call `check_readiness(bundle_slug="...")` to see if the provider's credentials are configured and valid.

2. **Validate connectivity** — call `validate_bundle(bundle_slug="...")` to make a real API call against the provider. This tests whether the credentials actually work end-to-end.

3. **Review execution history** — call `list_executions(bundle_slug="...", status="error", limit=5)` to see recent failures. Each execution includes the tool name, status, duration, and error details.

4. **Inspect a specific execution** — call `list_executions(id="...")` with the execution ID to get full details including input parameters and error response.

5. **Check credential details** — call `list_credentials(provider_slug="...")` to see the credential's verification status, when it was last used, and what scopes are granted. Secrets are never exposed.

## Common failure patterns

- **401/403 errors**: Credentials expired or insufficient scopes. The user needs to re-authenticate the provider in their MCPBundles workspace.
- **404 errors**: The resource ID or identifier passed to the tool doesn't exist. Double-check the parameter values.
- **429 errors**: Rate limit hit. Wait and retry, or reduce the frequency of calls.
- **Tool not found**: The bundle may not be enabled, or the tool slug may be wrong. Use `search_tools` to find the correct tool name.
- **Empty results from `list_bundles`**: No bundles are enabled. The user needs to set up integrations at mcpbundles.com.

## Credential status meanings

- **verified**: Credentials are confirmed working.
- **unverified**: Credentials were added but haven't been tested yet.
- **failed**: Last verification attempt failed — credentials may be expired or revoked.
- **expired**: OAuth token has expired and needs refresh or re-authorization.
