---
name: setup-jointl
description: Connect and troubleshoot the hosted Jointl MCP when this plugin is installed or activated.
---

# Set up Jointl

Connect through the bundled remote MCP server at `https://api.join.tl/mcp`. Jointl user connections use OAuth; do not request an API key or access token from the user.

## Connect

1. Confirm that the user has an active Jointl account and belongs to the intended workspace.
2. Start the Jointl connector and follow its MCP OAuth discovery metadata.
3. Open the Jointl authorization page and sign in when required.
4. Verify the displayed Jointl member, workspace, role, and requested scopes.
5. Allow the connection.
6. Call the Jointl workspace-access tool before starting a domain workflow.

Jointl enforces the connected member's current role, company scope, record permissions, and Third-Party Apps permission on every request. Report missing or revoked access as an authorization boundary. Do not retry through a broader search or alternate domain.

## Writes and confirmation

Supported writes use a prepare, preview, explicit approval, and confirm sequence. A prepared action does not change Jointl business data. Call the confirmation tool only after the user approves the exact preview, and report completion only when the confirmation result states that the action completed.

## Reconnect and revoke

Use the client's reconnect flow when authentication is stale or expired. To end Jointl access immediately, revoke the OAuth grant under **API & Apps** in Jointl. Removing a connector in Claude or ChatGPT does not by itself guarantee that the Jointl grant was revoked.
