# Project Daedalus Architecture

## Mission

Daedalus provides an automation and intelligence layer around existing technical projects and personal development workflows. It connects sources, transforms information, maintains structured records, and produces useful outputs without replacing purpose-built operational systems.

## Architectural Boundary

**Daedalus owns:**

- Workflow orchestration
- Information ingestion and transformation
- Personal/career/certification lifecycle intelligence
- Evidence collection and reporting
- Workflow quality/reliability testing
- Automation versioning and controlled recovery
- Cross-project summaries and dashboards

**Daedalus does not own:**

- SIEM/security telemetry storage
- Adversary simulation
- Network monitoring/discovery platforms
- Kubernetes observability
- Core backup infrastructure
- Firewall/network control planes
- Autonomous software development agents

Those systems may expose data or controlled interfaces to Daedalus later.

## Current n8n Deployment Baseline

The initial Daedalus orchestration engine is a self-hosted n8n deployment running as a Docker Compose workload on the existing COC server.

Security and reliability controls implemented for the baseline include:

- n8n application traffic is bound to host loopback rather than directly exposed on the LAN.
- HTTPS access is provided through the existing Caddy reverse proxy.
- Host firewall rules restrict the HTTPS service to approved LAN and VPN networks.
- n8n persistent application state is stored in a named Docker volume.
- The existing n8n encryption key is explicitly preserved through a protected local environment file; the key itself is never committed to Git.
- Unverified/community packages are disabled.
- The n8n public API is disabled for the current deployment because it is not required by the initial workflows.
- High-risk nodes such as command execution and local-file trigger functionality remain excluded.
- A dedicated SQLite backup process uses SQLite's online backup mechanism rather than copying a live database file directly.
- Every generated database backup is subjected to `PRAGMA integrity_check` before it is accepted.
- Backup files are permission-restricted and retained locally for seven days.
- A systemd timer executes the n8n database backup daily at 05:00 America/Toronto, independent of the server's UTC system timezone.
- The server's existing broader backup system subsequently protects the n8n configuration directory and generated database backups as part of the home-directory backup scope.

The deployment was verified with a running container, successful HTTPS response through Caddy, successful manual and systemd-triggered SQLite backups, database integrity checks, and n8n's built-in security audit.

Private hostnames, addresses, encryption material, credentials, and other environment-specific secrets are intentionally omitted from this public documentation.

## Implemented Module 01 — Cyber Intelligence Daily

DAE-002-01 is the first completed production workflow on the Daedalus platform. It runs daily at 07:00 America/Toronto and can also be executed manually for controlled testing.

The workflow:

- Ingests six public security RSS feeds plus the NIST NVD and CISA KEV APIs.
- Normalizes source-specific records into a shared intelligence schema.
- Filters records to the relevant collection window.
- Merges eight branches and removes duplicates within the current batch and across previous executions.
- Applies deterministic cybersecurity priority scoring and records explainable score reasons.
- Sorts results, selects the ten highest-ranked stories, and prepares concise report content.
- Generates and delivers a responsive HTML intelligence briefing through SMTP.
- Uses source retries and a separate Error Trigger workflow for failure notification.

The public workflow export is inactive by default and excludes credential bindings, personal email addresses, private error-workflow references, instance identifiers, and pinned execution data.

## Logical Layers

### 1. Source Layer
RSS/Atom feeds, public APIs, GitHub, manually entered records, approved project outputs, and future integrations.

### 2. Orchestration Layer
n8n schedules workflows, invokes APIs, validates input, routes records, applies transformations, and coordinates downstream processing.

### 3. Intelligence Layer
Deterministic scoring and optional AI-assisted classification/summarization. AI output must not silently become authoritative where correctness matters.

### 4. Data Layer
Structured records for articles, certifications, evidence, learning performance, market observations, workflow test results, and architecture decisions.

### 5. Presentation Layer
Email reports, documentation, GitHub artifacts, and ultimately the Daedalus Command Center.

### 6. Governance Layer
Secrets management, auditability, regression tests, human approval, version control, error handling, and recovery.

## Future Daedalus ↔ Hephaestus Boundary

Daedalus may identify an engineering task or failed workflow and create a controlled request for the separate AI software-engineering platform. The development system may prepare a change, tests, and pull request. Daedalus can record the result, but it should not grant coding agents unrestricted production control.

## Data Classification

- **Public:** sanitized documentation, diagrams, example payloads, safe workflow exports.
- **Internal:** non-sensitive operational records not intended for publication.
- **Sensitive:** certification IDs, personal career records, private system details.
- **Secret:** passwords, API keys, tokens, private keys, n8n encryption material.

Only Public data belongs in this repository.
