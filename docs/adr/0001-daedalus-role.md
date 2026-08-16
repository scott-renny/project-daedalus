# ADR-0001: Define Daedalus as an Orchestration and Intelligence Platform

- **Status:** Accepted
- **Date:** 2026-08-15

## Context

The wider lab contains or plans multiple purpose-built systems for security monitoring, adversary simulation, networking, infrastructure, applications, and AI-assisted software engineering. n8n can technically duplicate parts of several of these systems, but doing so would create overlapping responsibilities, unnecessary complexity, and a weaker portfolio architecture.

## Decision

Project Daedalus will serve as the automation, orchestration, intelligence, lifecycle, evidence, and reporting layer.

It may consume data from specialist systems and invoke explicitly approved interfaces, but it will not become a replacement SIEM, network-monitoring platform, adversary-simulation engine, Kubernetes observability stack, or autonomous coding platform.

## Consequences

### Positive

- Clear system boundaries
- Less duplicated functionality
- Easier troubleshooting and ownership
- Stronger portfolio narrative
- Specialist tools remain responsible for the jobs they perform best
- Daedalus can evolve independently as an integration layer

### Trade-offs

- Some future capabilities require APIs or integration contracts between projects
- Daedalus cannot assume every system is directly controllable
- Cross-system workflows require careful authentication and least-privilege design
