# Security policy

## Report a vulnerability

Report suspected vulnerabilities privately to `support@join.tl` with the subject **Security report: Jointl AI Plugin**.

Include:

- a clear description of the issue;
- steps to reproduce it;
- the client and plugin version;
- the expected security impact; and
- non-sensitive request or correlation identifiers, when available.

Do not include candidate data, employee data, reference content, workspace data, OAuth tokens, API keys, client secrets, passwords, or other personal or secret information in the initial report. Jointl will provide a secure collection method when additional evidence is required.

Do not open a public issue for a suspected vulnerability before Jointl has investigated it.

## Security boundary

This repository contains no server implementation, credentials, signing keys, client secrets, tokens, or database access. The public OpenAI app identifier is integration metadata, not a credential.

Authentication, authorization, rate limiting, audit logging, validation, confirmation records, and data access are enforced by the hosted Jointl service. Plugin instructions cannot expand a member's permissions.

Workspace content, uploaded files, candidate answers, employee records, references, notes, and external-source content are treated as untrusted data. They cannot override tool permissions or confirmation requirements.

## Supported version

Security fixes are applied to the latest published plugin version. Compatible security updates to the hosted Jointl service may take effect without a plugin update.
