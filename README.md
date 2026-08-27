# Jointl AI Plugin

Use Jointl from Claude, ChatGPT, and Codex to search authorized workspace data, review People Intelligence evidence, create Flows, and prepare permitted actions.

Jointl connects through the hosted Model Context Protocol (MCP) server at `https://mcp.join.tl` and applies your existing Jointl permissions to every request.

## What you can do

- Find companies, Flows, Checks, employees, Talent Pool profiles, and Autopilots you are allowed to access.
- Summarize candidate evidence from pre-screening, assessments, Tests, references, employment confirmations, integrity signals, and verifications.
- Review employee evidence from Performance, Team Pulse, Glow Moments, and Exit Intelligence.
- Design Hiring Review, Performance, and Exit Intelligence Flows.
- Validate spreadsheet data for bulk Check and employee imports.
- Prepare supported notes, status changes, Autopilots, archives, restores, and deletions for your approval.

## Get started

1. Install Jointl from the plugin or connector directory in Claude, ChatGPT, or Codex.
2. Select **Connect** and sign in to your Jointl account.
3. Review the Jointl workspace, member, role, and requested access before allowing the connection.
4. Start with a request such as:

   - `Design and create a complete Jointl Flow for this role.`
   - `Run the relevant checks for these people.`
   - `Find this person in Jointl and summarize the supporting evidence.`
   - `Identify the top 3 people and provide a deep, evidence-backed comparison.`
   - `Find the most relevant people for this role and explain why they match.`

When a client asks for a remote MCP server URL, use:

```text
https://mcp.join.tl
```

Jointl user connections use OAuth. Do not enter a Jointl API key into Claude, ChatGPT, or Codex.

## Access and approvals

Jointl evaluates every request against your current:

- workspace membership and role;
- company and record access;
- sharing and resource permissions; and
- Third-Party Apps permission.

Permission changes in Jointl apply to subsequent requests. Restricted records and fields remain unavailable to the plugin.

Supported writes are prepared as a preview before they change Jointl data. Consequential and destructive actions require your explicit approval of that preview.

## Evidence and decisions

Jointl provides factual decision support. Candidate and employee summaries distinguish scores, narrative evidence, confirmations, verification signals, missing coverage, and uncertainty. Jointl does not make hiring, promotion, compensation, discipline, termination, housing, lending, admission, or other eligibility decisions for you.

## Disconnect Jointl

Revoke the OAuth connection under **API & Apps** in Jointl to end its access immediately. Remove the plugin or connector separately in Claude, ChatGPT, or Codex when you no longer want it installed.

## Privacy, security, and support

- [Privacy Policy](https://join.tl/legal/privacy-policy)
- [Terms of Service](https://join.tl/legal/terms-of-service)
- [Security policy](SECURITY.md)
- [Support](SUPPORT.md)
- Email: `support@join.tl`

## Open-source package

This repository contains the public plugin manifests, workflow skills, setup instructions, and artwork. It does not contain Jointl's hosted API, MCP server implementation, application source, databases, authorization logic, credentials, or proprietary business logic.

The files in this repository are available under the [MIT License](LICENSE). Jointl's hosted services and private source are outside that license. See [NOTICE.md](NOTICE.md) for details.
