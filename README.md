# Workman's Books Inventory & Auction Management

A planned business management application for **Workman's Books**, supporting the cataloging and sale of rare, vintage, and out-of-print books and related collectibles through retail sales and auctions.

> **Project status — Requirements approved; design in progress.** The Software Requirements Specification (SRS) **Version 2.0** is the approved business-requirements baseline. Database architecture and schema design are the next phase. **The application has not yet been implemented.** Features described below are planned, not available for use.

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

## Documentation

The authoritative requirements document is:

- [Software Requirements Specification — Version 2.0](docs/requirements/SOFTWARE_REQUIREMENTS.md)

The SRS records approved business requirements, proposed architecture, open dependencies, and the approval gates for subsequent work. Git history preserves previous document revisions.

## Proposed technology architecture

| Area                | Proposed approach            | Status                                                  |
| ------------------- | ---------------------------- | ------------------------------------------------------- |
| User interface      | React and TypeScript         | Proposed; deployment form not finalized                 |
| Backend             | Node.js and TypeScript       | Proposed                                                |
| Central database    | MySQL or MariaDB             | Proposed; hosting and secure access to be verified      |
| Media and documents | Dropbox                      | Proposed; integration and recovery design pending       |
| Primary usage       | Windows-oriented application | Browser, packaged desktop, or hybrid approach undecided |

External services under consideration include **Gmail API**, **iCollector**, **Stamps.com**, **PayPal**, **Square**, and the Workman's Books retail website. API support, permissions, costs, and provider policies must be validated before implementation. Proposed payment surcharges are **not approved for activation** until applicable legal, network, tax, and provider requirements have been checked.

## Planned repository organization

```text
Workmans-Books-Inventory-UI/
├── README.md
├── CHANGELOG.md                 # When development begins
├── docs/
│   ├── requirements/
│   │   └── SOFTWARE_REQUIREMENTS.md
│   ├── architecture/             # Future architecture and schema documents
│   └── decisions/                # Future architecture decision records
├── frontend/                     # Future application code
├── backend/                      # Future service code
└── .gitignore                    # Create when tooling is selected
```

Only `README.md` and `docs/requirements/SOFTWARE_REQUIREMENTS.md` are provided at this stage. The other paths show a suggested future structure; they do not imply working code exists.

## Development roadmap

1. **Requirements definition — Complete:** Review and approval of SRS Version 2.0.
2. **Conceptual database design — Next:** Define business entities and relationships, beginning with Customers and Inventory.
3. **Schema review and approval — Pending:** Produce an overall entity-relationship diagram (ERD), smaller domain-specific ERDs, and a table-by-table schema reference with keys, fields, constraints, and business rules.
4. **Technical architecture validation — Pending:** Verify hosting, authentication, security, integrations, backup/recovery, and deployment approach.
5. **Implementation — Not started:** Build database and application components only after explicit design approval.
6. **Testing and deployment — Not started:** Validate workflows, data migration, security, integration behavior, and operational recovery.

## Design and implementation guardrails

- Do not create or modify production database tables, external services, or application features solely because a requirement appears in the SRS.
- Review and approve the database schema before implementation.
- Preserve financial transaction history and meaningful audit records; prefer explicit corrections over destructive edits.
- Keep proposed technical choices separate from approved business behavior until feasibility and compliance are verified.
- Use version-controlled documentation to record approved changes and open decisions.

## Repository status

This repository currently serves as the project planning and design workspace. Setup, build, run, and deployment instructions will be added when working application code exists.

## License

No license has been selected. All rights are reserved unless and until the owner chooses a license.
