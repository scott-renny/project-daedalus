# Workflows

Sanitized n8n workflow exports and module-specific documentation live here.

## Modules

- [01 — Cyber Intelligence](01-cyber-intelligence/) — complete
- `02-portfolio-evidence/` — planned
- `03-certification-lifecycle/` — planned
- `04-adaptive-learning/` — planned
- `05-career-intelligence/` — planned
- `06-documentation-adr/` — planned
- `07-engineering-reporter/` — planned
- `08-reliability-lab/` — planned
- `09-digital-twin/` — planned
- `10-gitops-recovery/` — planned
- `11-command-center/` — planned

## Publication Rule

Never commit a workflow export directly from production without inspecting and sanitizing it. Replace credentials, tokens, private URLs, internal addresses, personal identifiers, workflow/instance IDs, and sensitive sample data with documented placeholders. Public exports should be inactive by default.
