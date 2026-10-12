# Workmans-Books-Inventory-UI

Business management software project for **Workman’s Books**, covering inventory and cataloging, photographs, auctions, consignments, customers, sales and invoices, shipping, accounting, and reporting.

> **Project status: Requirements and architecture planning.** The software is not yet implemented. No production database, Dropbox content, or other business system has been modified as part of this planning work.

## Requirements

The current working specification is:

**[Software Requirements Specification — Version 1.0](docs/requirements/SOFTWARE_REQUIREMENTS.md)**

The specification records business requirements discussed with the owner and identifies technical decisions that still need validation. It is a **working draft for review**, not authorization to begin implementation.

## Proposed technology direction

The following is a *proposal*, not a finalized or deployed stack:

| Area | Proposed direction | Status |
| --- | --- | --- |
| User interface | React + TypeScript | Proposed |
| Backend | Node.js + TypeScript | Proposed |
| Database | Central relational database; MySQL/MariaDB under consideration | Hosting and schema unverified |
| Document and photo storage | Dropbox integration | Authentication and storage workflows to validate |
| Development | GitHub repository, VS Code | Planned |
| Desktop experience | Windows-oriented; browser, desktop shell, or hybrid | Undecided |

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

## Next steps

1. Review the specification and correct omissions or ambiguities.
2. Examine existing spreadsheets, macros, catalog templates, and business workflows to confirm field mappings.
3. Draft and review the **conceptual database schema** and business rules.
4. Validate hosting, application packaging, security, and third-party integrations.
5. Agree on logical schema, migration approach, and acceptance criteria.
6. **Begin implementation only after explicit approval.**

## Working with requirements

- Treat [`SOFTWARE_REQUIREMENTS.md`](docs/requirements/SOFTWARE_REQUIREMENTS.md) as the GitHub-maintained source of truth.
- Make proposed changes through commits or pull requests so decisions are traceable.
- Keep any Word/PDF copies synchronized with the Markdown specification when distributing updated versions.
- Do not commit credentials, API keys, customer records, or private business data.

## License

No license has been selected. All rights are reserved unless and until the owner chooses a license.
