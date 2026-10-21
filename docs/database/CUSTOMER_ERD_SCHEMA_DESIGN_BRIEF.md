# Workman’s Books — Customer ERD & Schema Design Brief

**Status:** Draft planning brief, 20 October 2026. No ERD, SQL schema, hosting or implementation approved.
**Sources:** Owner-confirmed Customer Database Master Decision Log Q1–127 and SRS v2.0 baseline with customer addendum.

## Candidate logical entities for the first customer-domain ERD

| Group | Candidate tables / entities | Decisions |
| --- | --- | --- |
| Identity | `customers`, `customer_former_names`, `customer_external_ids` | Q5–8, Q18, Q28–30, Q54–57 |
| Roles | `customer_roles`, `customer_role_assignments` | Q1, Q58–62 |
| Contact methods | `customer_emails`, `customer_phones`, `customer_addresses` | Q2–4, Q63–76 |
| Business contacts | `customer_contacts`, `contact_purposes`, `contact_purpose_assignments` | Q5, Q77–81 |
| Notes & follow-ups | `customer_notes`, `customer_note_categories`, note-document links, note-reminder links, reminders | Q9, Q20, Q82–88 |
| Tags | `customer_tag_categories`, `customer_tags`, `customer_tag_assignments` | Q17, Q89–92 |
| Relationships | `customer_relationship_types`, `customer_relationships` | Q10, Q93–96 |
| Certificates | `customer_tax_exemptions`, certificate documents/versions, exemption usage records | Q11, Q97–127 |
| Documents & audit | `customer_documents`, document metadata/links, centralized audit events | Q13, Q21, Q86, Q99, Q117–127 |
| Communication & activity | communication preferences, contact history, customer activity references | Q12, Q15, Q19 |
| Imports & drafts | customer import batches/rows, customer drafts, edit leases | Q35–49 |

Names above are **candidate logical names**, not finalized physical table names. Additional joins and supporting entities may be required. Transactions/invoices, users, and reminders cross domain boundaries and will be referenced, not invented in isolation.

## Relationships to draw first

1. `customers` 1-to-many role assignments, addresses, emails, phones, notes, tags, documents, tax certificates, and business contacts.
2. Business contacts 1-to-many contact-purpose assignments; contact emails/phones may optionally reference a contact belonging to the **same** customer.
3. Customer relationships connect two customer rows, with a configurable relationship type and reverse display label; one stored relationship visible from both directions.
4. Notes link many-to-many with documents and reminders without duplicating underlying Dropbox files or reminder records.
5. Certificate documents and version metadata reference Dropbox storage IDs; certificate usage links to finalized invoice tax snapshots, not mutable certificate state.

## Critical constraints to specify and test

- Immutable seven-character `customer_code` separate from numeric `customer_id`; never reuse retired codes.
- Only one active assignment per customer/role and customer/tag; permit multiple historical assignment records.
- Only one active relationship per **normalized unordered customer pair + equivalent relationship type**; reverse directional definitions must be considered; permit distinct types and ended history.
- Exactly one primary active business contact at most; one active primary email, one active invoice email, one active primary phone per relevant scope; distinguish business-wide and contact-level scope.
- Preserve billing/shipping address snapshots, including optional `care_of`; never rewrite past invoices when current addresses change.
- Inactive records retained, no destructive cascading deletion of financial, communication, or certificate history.
- Certificates cannot become approved while required validation or document upload remains incomplete; log all overrides and approval changes.
- Preserve finalized invoices and immutable exemption usage; adjustments are linked new records.
- Document filename collisions do not overwrite; failed Dropbox uploads have secure staged retries, and successful uploads are verified.

## Open implementation-level decisions (not a reopening of Q1–127)

1. Define `CustomerNumber` for `CustomerNumber_TAX_CERT_Year.extension` and whether it is an existing external/customer numbering field.
2. Select DB engine/version and enforce active-only uniqueness using constraints supported by that engine; specify race-condition handling.
3. Choose canonical normalized email/phone/address strategy and contact-level uniqueness scope.
4. Specify precise jurisdiction/tax eligibility and invoice snapshot fields, including administrator override authority.
5. Define Dropbox API security, stable file IDs, document retention, retry limits, database backup/restore, and cross-system reconciliation.
6. Define RBAC and audit event schema, retention, data migration, and import rollback.
7. Decide whether to design domain-specific ERDs before a combined overview, then submit draft ERDs, table dictionary, keys, constraints, and migration plan for owner approval.

**Approval gate:** Do not create physical database tables or alter external services until the owner approves the proposed schema and technical architecture.
