# DAE-002-01 — Cyber Intelligence Daily

**Status:** Complete  
**Platform:** n8n  
**Schedule:** Daily at 07:00 America/Toronto

This workflow collects recent cybersecurity intelligence, normalizes each source into a common schema, removes duplicates, applies deterministic priority scoring, selects the ten highest-ranked stories, and delivers a portfolio-quality HTML email report.

## Implemented Sources

- SANS Internet Storm Center
- BleepingComputer
- Microsoft Security Blog
- Cisco Talos
- Palo Alto Networks Unit 42
- Cloudflare
- NIST National Vulnerability Database
- CISA Known Exploited Vulnerabilities Catalog

## Implemented Pipeline

1. Manual or scheduled trigger
2. RSS/API ingestion with retry handling
3. Source-specific normalization
4. Recent-item filtering
5. Eight-way append merge
6. Current-batch and cross-execution deduplication
7. Deterministic cybersecurity priority scoring
8. Descending sort and Top 10 selection
9. Ranked story preparation
10. Sanitized HTML report generation
11. Gmail SMTP delivery
12. Companion error-workflow notification

## Import and Configuration

1. Import `DAE-002-01-cyber-intelligence-daily.sanitized.json` into n8n.
2. Create or select an SMTP credential for the final email node.
3. Replace `YOUR_GMAIL_ADDRESS@example.com` with the intended sender and recipient address.
4. Create a separate Error Trigger workflow and select it under the main workflow's error-workflow setting.
5. Confirm the workflow timezone is `America/Toronto` and review the 07:00 schedule.
6. Run the workflow manually, verify the report, then publish/activate it.

Credentials and the companion error-workflow reference are intentionally absent from the public export.

## Validation Snapshot

The completed v1 build processed 123 normalized records from eight sources and selected ten ranked stories during validation. Scheduled and manual execution paths, HTML report generation, SMTP delivery, source retry behavior, cross-execution deduplication, and the companion failure-alert workflow were configured and tested. Historical trend analysis and expanded regression coverage remain optional future enhancements.

## Public-Safety Notes

The committed export is inactive by default. It contains no credential bindings, personal email address, workflow or instance identifiers, private hostnames, IP addresses, secrets, tokens, encryption keys, pinned execution data, or private error-workflow ID.
