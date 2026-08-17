# Certification Lifecycle Data Model

**Work item:** DAE-003  
**Status:** Schema foundation complete; automation in development

This directory defines the storage-independent contract for the Certification Lifecycle Manager. Operational storage can change without changing what each record means.

## Entities

- `certification.schema.json` — one planned or earned certification
- `renewal-rule.schema.json` — vendor requirements and authoritative provenance
- `ce-activity.schema.json` — continuing-education activity and approval state
- `reminder-history.schema.json` — notification scheduling, idempotency, and delivery history
- `examples/synthetic-lifecycle-records.json` — non-personal example records

## Relationships

- A certification optionally references one renewal rule through `renewal_rule_id`.
- Continuing-education activities reference a certification through `certification_id`.
- Reminder-history records reference a certification through `certification_id`.
- Approved CE progress is calculated from activity records rather than manually duplicated on the certification.

## Validation Rules

- Identifiers are stable lowercase slugs and must not contain credential numbers.
- Status values are controlled enumerations.
- Dates use ISO 8601.
- Certifications marked as expiring require an expiration date.
- Renewal rules require an HTTPS authoritative source and verification timestamp.
- Unknown values use `null`; they are not represented by empty strings or invented defaults.
- Derived values such as days remaining and approved-credit totals are calculated by workflows.

## Privacy Boundary

Public-safe fields include vendor, certification name, general status, sanitized summaries, and non-sensitive progress totals.

Private operational fields include exact dates where desired, notes, evidence references, receipts, verification URLs, and supporting documents.

Credential numbers, verification codes, account data, document contents, passwords, API keys, tokens, and recovery codes are not part of this model and must never be committed.

The schemas define structure only. Real personal records remain outside the public repository.
