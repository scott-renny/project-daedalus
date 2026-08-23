# Certification Lifecycle Manager

**Work item:** DAE-003  
**Status:** Complete  
**Platform:** n8n and PostgreSQL

The Certification Lifecycle Manager tracks certification dates, vendor renewal rules, continuing-education progress, renewal windows, and reminder delivery without placing private certification records in this repository.

## Implemented Workflows

- `DAE-003-00 — Certification Lifecycle Validation` — manual-only synthetic test, calculation, claim-reset, and cleanup workflow
- `DAE-003-01 — Certification Lifecycle Monitor` — scheduled lifecycle calculation, actionable-record selection, reminder claiming, HTML email delivery, and delivery-status recording
- `DAE-003-02 — Certification Record Manager` — authenticated form, input validation, and idempotent record/rule upsert
- `DAE-003-03 — Certification Lifecycle Error Alerts` — companion workflow for production failure notification

## Operational Controls

- PostgreSQL is reachable only through the private container network and is not published on a host port.
- The n8n runtime uses a dedicated, non-superuser database role without database- or role-creation privileges.
- Form access requires authentication; submitted values are validated before database writes.
- Reminder claims provide idempotency so repeated runs do not send the same reminder twice.
- Delivery outcomes are recorded as sent or failed for auditability.
- Daily database backups are integrity-checked through an automated restore verification and retained with restrictive permissions.
- Production failures are routed to a separate email-alert workflow.
- Validation uses synthetic records and a targeted cleanup step; production records are never committed.

## Validation Completed

- Confirmed the database schema and runtime-role permissions.
- Confirmed private network reachability from n8n and absence of a published database port.
- Exercised on-track and urgent renewal calculations with synthetic records.
- Verified continuing-education credit aggregation and remaining-credit calculations.
- Verified one-time reminder claiming, HTML email delivery, and sent-status recording.
- Verified authenticated form submission, validation, database upsert, and completion response.
- Verified the scheduled monitor and companion error workflow configuration.
- Removed all synthetic certification, activity, rule, and reminder records after testing.
- Confirmed that only the intended real record remained in operational storage.

## Public Repository Boundary

This repository documents architecture, behavior, controls, and public-safe schemas. It intentionally excludes database credentials, SMTP credentials, internal addresses, private URLs, account identifiers, certificate numbers, verification codes, real lifecycle records, and production workflow exports that have not completed a separate sanitization review.

