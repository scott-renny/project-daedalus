# Security Policy

Project Daedalus is a public portfolio repository for a self-hosted automation platform. Public documentation and sanitized workflow definitions must never expose operational secrets or sensitive personal/infrastructure information.

## Never Commit

- API keys, access tokens, passwords, session cookies, private keys, or recovery codes
- n8n credential exports or encryption keys
- Private certification credential IDs or private verification data
- Personal email contents or other private communications
- Internal IP addresses, hostnames, VPN configuration, or unnecessary network topology details
- Private employment/application information
- Sensitive logs or production execution payloads
- Unredacted environment files

## Repository Conventions

- Use environment-variable placeholders for secrets.
- Use example/synthetic data in public samples.
- Sanitize n8n workflow exports before committing them.
- Review generated documentation before publication.
- Keep consequential actions behind explicit controls or human approval where appropriate.
- Grant integrations only the permissions required for their task.

## Automation Safety

Daedalus follows a tiered approach to automated actions:

1. **Observe** — read and report only.
2. **Low-risk automation** — deterministic actions with limited impact.
3. **Controlled remediation** — approved actions with validation and rollback considerations.
4. **Human approval required** — consequential, externally visible, destructive, or security-sensitive actions.
5. **Never autonomous** — actions that should not be delegated without direct human control.

## Reporting Security Problems

Do not disclose real credentials or sensitive infrastructure details in a public GitHub issue. Security-sensitive findings should be handled privately and secrets should be rotated if exposure is suspected.
