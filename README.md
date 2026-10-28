# Workman's Books Inventory & Auction Management

A planned business management application for **Workman's Books**, supporting the cataloging and sale of rare, vintage, and out-of-print books and related collectibles through retail sales and auctions.

> **Project status — Requirements v2.0 approved; customer Questions 1–127 and application-wide logical Findings 1–250 owner-confirmed (28 October 2026); 144 working logical tables; detailed ERD/physical schema pending.** The Software Requirements Specification (SRS) **Version 2.0** is the approved business-requirements baseline. Logical schema reconciliation is paused at Finding 250; detailed table/ERD design and architecture validation remain pending. **The application has not yet been implemented.** Features described below are planned, not available for use.

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
- Continuity checkpoint through Finding 250: `Workmans_Books_Continuity_Checkpoint_Through_Finding_250_2026-10-28.docx` (included in this documentation package)

The SRS records approved business requirements, proposed architecture, open dependencies, and the approval gates for subsequent work. Git history preserves previous document revisions.

## Development roadmap

1. **Requirements definition — Complete:** Review and approval of SRS Version 2.0.
2. **Customer design decision consolidation — Complete:** All Questions 1–127 owner-confirmed; Question 96 Option A approved. Master Decision Log and SRS addendum reconciled. This does not approve a database schema.
3. **Logical schema reconciliation — Paused at Finding 250:** Owner approved 250 findings and 144 working logical table names; Finding 251 is next after checkpoint acknowledgment.
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
- The 144-table working inventory and Findings 61–250 registers are documented in the SRS addendum; three tables were added after Finding 100: `consignor_repayments`, `financial_report_versions`, `financial_report_files`.
- No SQL tables, integrations or application functionality have been implemented by these documentation updates.

## Repository status

This repository currently serves as the project planning and design workspace. Setup, build, run, and deployment instructions will be added when working application code exists.

## License

No license is stated here. Refer to a repository `LICENSE` file if one is added.

## Historical Finding 200 continuity addendum — approved logical decisions 151–200

**Historical status at Finding 200:** All Findings 151–200 approved as Option A, no additional logical tables. At that checkpoint: **200 approved findings / 144 logical tables**. The current stop is Finding 250; resume with Finding 251 only after checkpoint acknowledgment. The Version 2.0 SRS baseline and customer Q1–127 decisions remain intact. No SQL, implementation or physical-schema sign-off.

- **Finding 151 — Option A, no new tables:** Vendor refunds and credits; preserve original expense, source, cash refunds vs future-use credits and reconciliation.
- **Finding 152 — Option A, no new tables:** Vendor prepayments and deposits; distinguish advance assets/credits from recognized expense, reconcile applications and refunds.
- **Finding 153 — Option A, no new tables:** Business fixed assets and disposals using existing records; acquisition, depreciation/accountant review, sale/disposal and audit.
- **Finding 154 — Option A, no new tables:** Expense reclassification with authorized corrections and original transaction preservation.
- **Finding 155 — Option A, no new tables:** Unpaid vendor bills tracked separately from paid expenses; cash-basis recognition remains accountant-reviewed.
- **Finding 156 — Option A, no new tables:** Recurring expenses and expected obligations via existing records; reminders, prevent duplicate actual charges.
- **Finding 157 — Option A, no new tables:** Vendors represented through customer roles and existing customer records; role separation and audit.
- **Finding 158 — Option A, no new tables:** Manual vendor statement reconciliation, missing/duplicate charges and resolution history.
- **Finding 159 — Option A, no new tables:** Duplicate vendor invoice detection and authorized exception resolution.
- **Finding 160 — Option A, no new tables:** Expense approval workflow, permission separation and documented authorization.
- **Finding 161 — Option A, no new tables:** Budgets using existing expense/settings/reporting records; compare planned versus actual without accounting entries.
- **Finding 162 — Option A, no new tables:** Receipt and supporting-document requirements based on expense category, exceptions and audit.
- **Finding 163 — Option A, no new tables:** Dropbox-managed expense attachments with version history and initial integrity verification.
- **Finding 164 — Option A, no new tables:** Expense-document retention indefinitely by default, controlled disposal and legal/audit holds.
- **Finding 165 — Option A, no new tables:** Accountant expense-document ZIP exports with controlled access, completeness and audit.
- **Finding 166 — Option A, no new tables:** Accountant-recommended adjustments linked to original transaction; noncash vs cash, closed-year protection, reversals.
- **Finding 167 — Option A, no new tables:** Vehicle mileage and expenses; historical rates, business/personal use, reimbursement vs deduction, no double count.
- **Finding 168 — Option A, no new tables:** Mixed-purpose trips with business/personal segment mileage and documented shared-cost allocations.
- **Finding 169 — Option A, no new tables:** Travel expenses and reimbursements; payer, partial reimbursements, substantiation and separate tax treatment.
- **Finding 170 — Option A, no new tables:** Travel advances, documented substantiation, repayments and unresolved balances.
- **Finding 171 — Option A, no new tables:** Canceled or partly completed travel; cancellation fees, deposits, credits, refunds and advance reconciliation.
- **Finding 172 — Option A, no new tables:** Optional travel per diem; historical rates, eligibility, approvals and duplicate-claim prevention.
- **Finding 173 — Option A, no new tables:** Meals and entertainment classification; attendees/purpose, receipts, deduction fraction vs actual cost.
- **Finding 174 — Option A, no new tables:** Inventory gifts, promotional giveaways and other non-sale dispositions; ownership, cost and approval.
- **Finding 175 — Option A, no new tables:** Damaged/lost/stolen/destroyed inventory; repair/write-off, consignor rights, insurance and audit.
- **Finding 176 — Option A, no new tables:** Inventory restoration/conservation; service expenses, before/after condition and owner authorization.
- **Finding 177 — Option A, no new tables:** Condition and grading history; source/assessor, revisions, publication snapshots and audit.
- **Finding 178 — Option A, no new tables:** Authenticity, provenance and attribution; claims vs verified evidence, conflicts and inventory-linked documents.
- **Finding 179 — Option A, no new tables:** Inventory research notes and bibliographic evidence; identifiable notes/sources and historical versions.
- **Finding 180 — Option A, no new tables:** Cataloging review and publication approval; approvals tied to content version and repeat review cycles.
- **Finding 181 — Option A, no new tables:** Temporary inventory reservations; history, expiration, conflict prevention and release.
- **Finding 182 — Option A, no new tables:** Consignor returns and withdrawals; requests, approvals, custody handover and historical evidence.
- **Finding 183 — Option A, no new tables:** Inventory storage transfers, temporary movements and location history including non-box locations.
- **Finding 184 — Option A, no new tables:** Physical inventory counts; sessions, expected snapshots, observed results, discrepancies and approvals.
- **Finding 185 — Option A, no new tables:** Temporary external inventory custody; custodian, permissions, handover, due date and inspection.
- **Finding 186 — Option A, no new tables:** Inventory image versions and independent channel selections; immutable published image sets.
- **Finding 187 — Option A, no new tables:** Multi-volume sets and components; structured component quantities, completeness and fulfillment.
- **Finding 188 — Option A, no new tables:** Inventory splits/combinations; source-result lineage, cost allocation, ownership and sale prevention.
- **Finding 189 — Option A, no new tables:** Channel-specific asking prices; effective periods, pricing history and realized-price separation.
- **Finding 190 — Option A, no new tables:** Market/insurance valuations; source, methodology, date, evidence and nonaccounting treatment.
- **Finding 191 — Option A, no new tables:** Inventory insurance claims; affected items, claims, partial recoveries and consignor allocations.
- **Finding 192 — Option A, no new tables:** Inventory purchase offers/counteroffers; negotiation history, offer status and resulting sale linkage.
- **Finding 193 — Option A, no new tables:** Layaway/installment sales; agreements, installment schedules, payments, inventory commitment, fulfillment restrictions and refunds.
- **Finding 194 — Option A, no new tables:** Fixed-price returns/exchanges; authorization, physical receipt, inspection, refunds, restocking and consignor rights.
- **Finding 195 — Option A, no new tables:** Payment disputes/chargebacks; processor references, evidence, deadlines, fees, reversals and partial recoveries.
- **Finding 196 — Option A, no new tables:** Customer credit types, issue sources, partial redemption, refundability, restrictions and lawful expiration.
- **Finding 197 — Option A, no new tables:** Customer account statements; authoritative transactions, opening/closing balances, available credits separately and reconciliation.
- **Finding 198 — Option A, no new tables:** Sales tax refund adjustments; original item/jurisdiction/rate, partial refunds, filing-period review and no excess refund.
- **Finding 199 — Option A, no new tables:** Returned-to-sender shipments; carrier status vs physical custody, inspection, linked reshipments and disposition.
- **Finding 200 — Option A, no new tables:** Lost/damaged/misdelivered carrier claims; shipment/item links, evidence, customer remedies, partial recoveries and consignor protections.

### Required final schema validation

- Validate structured independent identifiers and relationships for layaway agreements/installments, return events, disputes, offers, reservations, physical counts, external custody, carrier claims and shipment returns; generic audit entries alone are not sufficient.
- Verify financial flows are individually traceable: partial refunds, tax adjustments, credit applications, chargeback reversals, insurance/carrier recoveries, travel advances, vendor credits, consignor allocations and customer account statements.
- Validate inventory custody, location and sale-availability state across transfers, counts, reservations, layaway, returns, split/merge, consignment withdrawals and shipment incidents.
- Confirm version-specific review approvals, research/evidence sources, provenance documentation, image selections, valuation histories, and published catalog snapshots.
- Preserve transaction originals, immutable finalized financial/report records, authorization, historical evidence, corrections, and audit trails. No SQL or implementation until full logical schema sign-off.
- Accountant/legal review remains necessary for cash basis, tax filing adjustments, expenses, credit expiration, chargebacks, carrier recoveries and consignor settlements.

## Finding 250 continuity addendum — approved logical decisions 201–250 (28 October 2026)

**Current status:** Findings **1–250 approved**; Findings **201–250 all Option A**, **no additional tables**; **144 working logical tables**. Reconciliation paused at Finding 250. Resume with Finding 251 only after checkpoint acknowledgment. No physical schema, SQL, implementation, or production changes authorized.

- **Finding 201 — Option A, no new tables:** Carrier shipping label voids, replacements and refunds; retain original label, refund status, replacement link and audit.
- **Finding 202 — Option A, no new tables:** Combined shipping across buyer invoices and auctions; allocate charges and package contents without duplicating fulfillment or revenue.
- **Finding 203 — Option A, no new tables:** Local pickup and delivery; appointments, custody handover, proof of release, partial pickup and audit.
- **Finding 204 — Option A, no new tables:** Customer shipping preferences; default versus transaction-specific instructions, consent and history.
- **Finding 205 — Option A, no new tables:** Shipping address verification and corrections; preserve original invoice address and verified shipment destination.
- **Finding 206 — Option A, no new tables:** Packed weights, dimensions and carrier adjustments; preserve measured figures, label quotes, adjustments and reconciliation.
- **Finding 207 — Option A, no new tables:** Shipping supplies inventory; purchases, stock movements, package consumption and expense classification.
- **Finding 208 — Option A, no new tables:** Shipment tracking and delivery evidence; carrier events, delivery confirmation, exceptions and customer notifications.
- **Finding 209 — Option A, no new tables:** International customs documentation; declared values, contents, approvals, export restrictions and immutable shipment evidence.
- **Finding 210 — Option A, no new tables:** Shipping insurance coverage; declared value, carrier/policy coverage, premiums, claims and limits.
- **Finding 211 — Option A, no new tables:** Shipment holds and release; reasons, authorizations, partial holds, release prerequisites and history.
- **Finding 212 — Option A, no new tables:** Carrier pickup/drop-off manifests; grouped packages, tender evidence, scan discrepancies and reconciliation.
- **Finding 213 — Option A, no new tables:** Shipping quotes and approvals; estimates versus final charges, customer approval and expiry.
- **Finding 214 — Option A, no new tables:** Split shipments and outstanding items; invoice-item/package allocation, partial dispatch, backorders and final fulfillment.
- **Finding 215 — Option A, no new tables:** Customer shipping charges versus actual carrier/handling expense; reconcile variances without rewriting issued invoices.
- **Finding 216 — Option A, no new tables:** Pre-fulfillment cancellations; preserve sale, payment, inventory, refund and consignor effects with approval.
- **Finding 217 — Option A, no new tables:** Buyer nonpayment and default; notices, deadlines, authorized cancellations, inventory/consignor effects and audit.
- **Finding 218 — Option A, no new tables:** Post-sale auction catalog corrections; preserve published versions, corrected text and buyer/consignor notification.
- **Finding 219 — Option A, no new tables:** Published auction lot withdrawals; approvals, reasons, external update flags, inventory and financial safeguards.
- **Finding 220 — Option A, no new tables:** Reoffering unsold, withdrawn or defaulted inventory; retain prior sale/lot history and availability checks.
- **Finding 221 — Option A, no new tables:** Draft auction lot consolidation and division; preserve item allocations, identifiers and numbering protections.
- **Finding 222 — Option A, no new tables:** Auction reserve versus consignor minimum; independent contractual minimum and lot reserve, with reviewed conflicts.
- **Finding 223 — Option A, no new tables:** Unsold auction lot post-auction dispositions; manual ownership/location/retail-release decisions and audit.
- **Finding 224 — Option A, no new tables:** External auction results import and reconciliation; stage source results, match lots, resolve conflicts and preserve provenance.
- **Finding 225 — Option A, no new tables:** External bidder identity matching; verify ambiguous identities and preserve external identifiers without auto-merge.
- **Finding 226 — Option A, no new tables:** Auction bidder disputes and sale-result challenges; case evidence, holds, resolution and immutable original result.
- **Finding 227 — Option A, no new tables:** Buyer premiums and fees; versioned auction policies, line-item calculations, exceptions and audit.
- **Finding 228 — Option A, no new tables:** Auction-specific bidder registration and approval; eligibility, conditions, verification, restrictions and history.
- **Finding 229 — Option A, no new tables:** Bidder deposits and guarantees; receipt, application, refund, forfeiture, outstanding liability and reconciliation.
- **Finding 230 — Option A, no new tables:** Buyer payment deadlines and extensions; policy, authorized exceptions, notices and history.
- **Finding 231 — Option A, no new tables:** Buyer overpayments and unapplied funds; separate customer liabilities, applications, refunds and no double counting.
- **Finding 232 — Option A, no new tables:** Payment processor fees and net bank deposits; gross receipts, fees, settlement timing and bank reconciliation.
- **Finding 233 — Option A, no new tables:** Buyer invoice consolidation and separation across auction sessions; preserve source sales, line allocations and audit.
- **Finding 234 — Option A, no new tables:** Auction buyer invoice delivery and acknowledgment; per-attempt recipient/channel/version, failures, confirmation versus acceptance.
- **Finding 235 — Option A, no new tables:** Buyer invoice corrections and replacement documents; immutable original, supersession, payment/tax/consignor consequences.
- **Finding 236 — Option A, no new tables:** Buyer invoice write-offs and uncollectible balances; authorization, partial write-offs, later recovery and accountant treatment.
- **Finding 237 — Option A, no new tables:** Consignor settlement disputes and corrections; independent disputes, holds, evidence, supplemental payments and recoveries.
- **Finding 238 — Option A, no new tables:** Consignor payout failures, voids and replacements; original and linked attempts, verified outcomes, no duplicate payment.
- **Finding 239 — Option A, no new tables:** Consignor payout preferences and instructions; verified destinations, sensitive-data controls, changes and one-time overrides.
- **Finding 240 — Option A, no new tables:** Consignor settlement statement delivery and acknowledgment; exact version, attempts, receipt versus acceptance and audit.
- **Finding 241 — Option A, no new tables:** Consignor payout scheduling and partial disbursements; eligible/scheduled/issued/paid distinctions, holds and rescheduling.
- **Finding 242 — Option A, no new tables:** Consignor advances against future auction proceeds; independent advances, disbursement, multi-auction recovery and balances.
- **Finding 243 — Option A, no new tables:** Consignor reimbursable expenses; actual expense versus charge, shared allocations, partial waiver and no double allocation.
- **Finding 244 — Option A, no new tables:** Multi-auction consignor balance reconciliation; independent settlements, cross-auction allocations, recoveries and historical balances.
- **Finding 245 — Option A, no new tables:** Consignor settlement periods and closing controls; review checks, individual closing, exceptions, immutable finalized amounts, controlled reopening and accounting periods.
- **Finding 246 — Option A, no new tables:** Consignor settlement reports and historical reconciliation snapshots; as-of balances, parameters, immutable report versions, restatements and access controls.
- **Finding 247 — Option A, no new tables:** Consignor death/incapacity and legal representative authority; verified scope, holds, competing claims, ownership continuity and authorized release.
- **Finding 248 — Option A, no new tables:** Consignment agreement renewals, amendments and termination; versioned effective terms, item/sale applicability, surviving obligations and signed evidence.
- **Finding 249 — Option A, no new tables:** Unclaimed consignor-owned inventory after termination; notices, custody, partial returns, disputes, lawful disposition and retained ownership.
- **Finding 250 — Option A, no new tables:** Consignor inventory condition changes during custody; intake evidence, independent observations, photos, investigation, consignor notice and catalog corrections.

### Final structural validation carried forward

- Shipping and fulfillment (201–215): independently identifiable label voids/replacements, cross-invoice package allocation, pickup handovers, quote approvals, customs documents, manifests, insurance, holds, split shipments and carrier cost reconciliation.
- Auction and buyer financials (216–236): independently identifiable defaults, disputes, deposits, bidder registrations, fee policy versions, overpayments, processor deposit reconciliation, invoice version/delivery attempts, and partial write-offs/recoveries.
- Consignor payouts and obligations (237–244): independently identifiable settlement disputes, payout attempt/replacement chains, verified payee instructions, statement deliveries, payout schedules, advances, expense allocations, and multi-auction reconciliation; prevent duplicate recognition.
- Settlement close and reports (245–246): independent closing events, checks, exceptions, reopening history, accounting-period integrity, historical as-of reconstruction, immutable issued reports and restatement lineage.
- Consignor authority and agreement terms (247–248): independently verified representatives and scoped authority, effective/revoked legal status, signed agreement versions and exact item/sale term references.
- Unclaimed inventory and condition (249–250): independently identifiable return cases, notices, partial releases, legal disposition authority, intake and later condition observations, photographs, custody context and responsibility determinations.
- Cross-cutting: existing general-purpose audit, message, note, document, and adjustment records are not automatically sufficient to represent independently identifiable business entities. Resolve any structural gaps before final logical-schema approval; accountant/legal review remains required where applicable.

**Continuity source:** `Workmans_Books_Continuity_Checkpoint_Through_Finding_250_2026-10-28.docx`; the original Version 2.0 requirements and customer Q1–127 decisions remain unchanged.
