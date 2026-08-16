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
