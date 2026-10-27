# Workman's Books Inventory & Auction Management

A planned business management application for **Workman's Books**, supporting the cataloging and sale of rare, vintage, and out-of-print books and related collectibles through retail sales and auctions.

> **Project status — Requirements v2.0 approved; customer Questions 1–127 and application-wide logical Findings 1–150 owner-confirmed (27 October 2026); 144 working logical tables; detailed ERD/physical schema pending.** The Software Requirements Specification (SRS) **Version 2.0** is the approved business-requirements baseline. Logical schema reconciliation is paused at Finding 150; detailed table/ERD design and architecture validation remain pending. **The application has not yet been implemented.** Features described below are planned, not available for use.

## Project goals

Provide a centralized, Windows-oriented workflow for inventory, customer and consignor records, auction preparation, retail sales, invoicing, fulfillment, accounting, and reporting. Reduce repeated data entry while preserving cataloging detail, financial history, and auditability.

## Planned capabilities

- **Inventory and cataloging:** Unique permanent inventory numbers; configurable item types; bibliographic descriptions, contributors, publishers, provenance, condition, location, and photographs; bulk editing; CSV/Excel import and export.
- **Retail sales:** Regular prices, configurable bulk pricing, time-limited promotions, customer invoices, and website publication/synchronization.
- **Auction management:** Multi-session auctions, provisional lots, pricing and estimates, reserves, lot numbering at finalization, iCollector exports, result entry, and controlled completion/reopening.
- **Consignments:** Ownership and source tracking, mixed-ownership allocations, commissions, settlements, and historical records.
- **Customers and payments:** Customer preferences, invoice email delivery, partial and multiple-method payments, customer credits, refunds recorded in the system, and payment audit history.
- **Shipping and fulfillment:** Packing charges, pickup handling, shipping calculations, labels, and tracking integrations where supported.
- **Accounting and reporting:** Expenses, payment reconciliation, sales and consignment reporting, and year-end summaries.
- **Operations and security:** Dashboard, Message & Status Center, audit logging, Administrator/Staff access roles, backup and recovery planning.
- **Optional assistance:** Human-reviewed AI-generated catalog descriptions and other assistance, subject to approval.

All functionality remains subject to the approved SRS and subsequent technical design decisions.

## Proposed technology architecture

| Area                | Proposed approach            | Status                                                  |
| ------------------- | ---------------------------- | ------------------------------------------------------- |
| User interface      | React and TypeScript         | Proposed; deployment form not finalized                 |
| Backend             | Node.js and TypeScript       | Proposed                                                |
| Central database    | MySQL or MariaDB             | Proposed; hosting and secure access to be verified      |
| Media and documents | Dropbox                      | Proposed; integration and recovery design pending       |
| Primary usage       | Windows-oriented application | Browser, packaged desktop, or hybrid approach undecided |

External services under consideration include **Gmail API**, **iCollector**, **Stamps.com**, **PayPal**, **Square**, and the Workman's Books retail website. API support, permissions, costs, and provider policies must be validated before implementation. Proposed payment surcharges are **not approved for activation** until applicable legal, network, tax, and provider requirements have been checked.

## Documentation

Project documentation (proposed repository paths):

- [Software Requirements Specification — Version 2.0 baseline + confirmed customer-design addendum](docs/requirements/SOFTWARE_REQUIREMENTS.md)
- [Customer Database Master Decision Log — Questions 1–127, plus application reconciliation cross-reference](docs/decisions/CUSTOMER_DATABASE_MASTER_DECISION_LOG.md)
- Continuity checkpoint through Finding 150: `Workmans_Books_Continuity_Checkpoint_Through_Finding_150_2026-10-27.docx` (store in the repo documentation area if desired; this checkpoint is provided separately)

The SRS records approved business requirements, proposed architecture, open dependencies, and the approval gates for subsequent work. Git history preserves previous document revisions.

## Development roadmap

1. **Requirements definition — Complete:** Review and approval of SRS Version 2.0.
2. **Customer design decision consolidation — Complete:** All Questions 1–127 owner-confirmed; Question 96 Option A approved. Master Decision Log and SRS addendum reconciled. This does not approve a database schema.
3. **Logical schema reconciliation — Paused at Finding 150:** Owner approved 150 findings and 144 working logical table names; Finding 151 is next after checkpoint acknowledgment.
4. **Detailed schema review and approval — Pending:** Produce an overall entity-relationship diagram (ERD), smaller domain-specific ERDs, and a table-by-table schema reference with keys, fields, constraints, and business rules.
5. **Technical architecture validation — Pending:** Verify hosting, authentication, security, integrations, backup/recovery, and deployment approach.
6. **Implementation — Not started:** Build database and application components only after explicit design approval.
7. **Testing and deployment — Not started:** Validate workflows, data migration, security, integration behavior, and operational recovery.

## Design and implementation guardrails

- Do not create or modify production database tables, external services, or application features solely because a requirement appears in the SRS.
- Review and approve the database schema before implementation.
- Preserve financial transaction history and meaningful audit records; prefer explicit corrections over destructive edits.
- Keep proposed technical choices separate from approved business behavior until feasibility and compliance are verified.
- Use version-controlled documentation to record approved changes and open decisions.

## Current design checkpoints

- Permanent customer codes: five uppercase letters plus `01`–`99`, never reused; internal numeric IDs are separate.
- Multiple roles, contact methods, relationships, history, audit and customer imports/exports are planned.
- Certificate documents use Dropbox references and version/recovery capabilities; central database backup/restore remains to be designed.
- ERD design must reconcile active-only role/tag/relationship uniqueness, historical address snapshots, certificate usage audit, and Dropbox reference integrity.
- Certificate filename `CustomerNumber` is not yet mapped to an approved database identifier; clarify before physical schema design.
- Customer Q96 is approved: block duplicate active relationships in either direction for the same relationship type, while allowing distinct types. The separate application-wide **Finding 128** is approved Option B; do not confuse it with a future customer Q128.
- Financial reports use versioned snapshots, protected local/Dropbox file archives, SHA-256 verification, granular backend permissions, controlled delivery, and retention/hold safeguards.
- Cash-basis reporting is the initial model, **pending accountant confirmation**; owner transactions, internal transfers, loans, reimbursements, split payments, and credit card reconciliation use existing records with distinct classifications.
- The 144-table working inventory and Findings 61–150 register are documented in the SRS addendum; three tables were added after Finding 100: `consignor_repayments`, `financial_report_versions`, `financial_report_files`.
- No SQL tables, integrations or application functionality have been implemented by these documentation updates.

## Repository status

This repository currently serves as the project planning and design workspace. Setup, build, run, and deployment instructions will be added when working application code exists.

## License

No license is stated here. Refer to a repository `LICENSE` file if one is added.
