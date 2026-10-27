# Workman's Books

**Software Requirements Specification · Version 2.0 approved baseline + customer Q1–127 and logical reconciliation Findings 1–150 addenda · 27 October 2026 · Physical schema and implementation approval pending**

Consolidated requirements baseline approved by the owner through the Section 19–27 review on 16 October 2026. This revision retains the approved Version 2.0 business requirements and adds the owner-approved logical-design decisions through Finding 150. The 144 logical table names are an approved working inventory, **not** a completed physical schema or authorization to implement. Technical architecture and implementation remain subject to separate review and approval.

## 1. Purpose, scope, and decision status

Create a Windows-oriented business management application for Workman’s Books covering rare-book and related-item inventory, retail sales, auctions, customer and consignor relationships, fulfillment, accounting, and reporting. The application should preserve established cataloging and auction workflows while eliminating duplicate entry where practical.

| Approved business requirements | Items described in Sections 2–15 reflect decisions already made during planning. |
| Proposed architecture | React/TypeScript user interface; Node.js/TypeScript services; centralized MySQL/MariaDB subject to hosting feasibility; Dropbox for media/documents. |
| Approved design progress | 150 logical reconciliation findings and a working inventory of 144 logical tables; detailed table definitions and full logical-schema sign-off remain pending. |
| Not yet approved | Complete logical/physical schema, provider choice, infrastructure configuration, implementation sequencing, and deployment. |
| Operating principle | Review and approve schema and architecture before coding or modifying GoDaddy/database resources. |

## 2. Application experience and navigation

- Collapsible left sidebar: Dashboard, Inventory, Auctions, Customers, Sales & Invoices, Consignments, Accounting, Reports, Settings. Remember expanded/collapsed preference.
- Multi-tab workspace for records; opening an existing record activates its tab. Warn about unsaved edits on closing/navigation. Restore previous tabs when practical.
- Global search for inventory, customers, invoices, and auction lots; results open in tabs.
- Dashboard: active inventory, active auctions, unpaid invoices, pending settlements, drafts, items requiring attention, and recent activity. Cards link to filtered views. Allow show/hide, drag-to-reorder, saved layout, and restore defaults.
- Persistent compact status bar: central database, Dropbox, local draft count, pending iCollector updates, and attention items.
- Central Message & Status Center: searchable history; unresolved items shown by default; filters, timestamps, severity, links, and resolution state. Business messages centrally stored; computer-specific messages stored locally. Transient successes, noticeable warnings, prominent blocking errors.
- Audit trail for meaningful business changes; dismissing a message never deletes its underlying business record.

## 3. Inventory and cataloging

- One inventory record per distinct physical saleable item, including each constituent item of a multi-item auction lot. Immutable permanent inventory number allocated only after successful explicit save. Support legacy identifiers. Example new format: SMIJO01-26-0003.
- Record item type/category, title, creator/author/editor, publisher, publication year/date, bibliographic detail, subject, description, condition, binding/cover, size, provenance/pedigree, weight, cost, retail price, status, box, source, owner, and related photographs as applicable.
- Item types include books, auction catalogs, fixed-price lists, magazines/journals/newsletters and articles, maps, posters, newspapers, coin photographs, postcards, VHS, and DVDs. Type-specific fields without forcing irrelevant fields onto every record.
- Statuses include ACTIVE, ON_HOLD, AUCTION_LOT, SOLD; unavailable items cannot silently be offered for sale or added to a new auction. Sold records remain permanently searchable.
- Store source/original consignor and current owner separately; maintain ownership transfer history and distinguish OWNED versus CONSIGNED.
- Each item has its own weight, normalized in ounces with pounds/ounces display. Physical box numbers can be reused once empty; maintain box moves/history and a thumbnail-based box browser.
- Advanced inventory search: keyword default, expandable field filters, sortable results, optional thumbnails, saved searches, and remembered search state.
- Bulk edits from selected search results, including box, category, subjects, price, and eligible auction assignments; show preview, validation, confirmation, and audit; protect identifiers and ownership.
- Excel/CSV export: all filtered results or selected rows, customizable columns, reusable templates; separate from iCollector-specific export.
- Excel/CSV import: new-versus-update mode, mapping, validation, duplicate checks, previews, error reporting, and audit; protect permanent identifiers and ownership; provide import template.

### Version 2.0 cataloging and configuration requirements

- Maintain a configurable `inventory_item_types` dictionary with immutable type codes, singular/plural labels, display order, active state, and relevant iCollector/website category mappings. Types may be added or deactivated without rewriting historical records; changes to an existing item's type after save require safeguarded, confirmed, audited editing.
- Shared inventory text fields: full multiline title; cover/binding details; condition details; size text; pages text; full description; optional concise post-description suitable for online display. Publication-specific or rare bibliographic details may remain in the general description rather than requiring separate fields.
- Books: multiple ordered contributors with roles (author, editor, translator, etc.), including people and organizations; multiple publishers with publication-specific locations; a human-readable publication year/date text and optional numeric sort year; multiple optional ISBNs, including format and primary designation, searchable with or without hyphens. Contributor and publisher relationships may also apply to other inventory types where appropriate.
- Shared publisher/dealer/auction-firm master: allow multiple classifications, individual-person sort names and firm sort names, with distinct historical names as separate records and optional predecessor/successor links. Do not merge historical identities automatically.
- Distinguish CATALOG and FPL types. Catalogs/FPLs support printed date text and optional sortable date; FPLs additionally support a natural-sort list number. A proposed title may be generated from issuing firm and date, but remains editable. Sale numbers and specialized details may be kept in description.
- Periodicals: reusable periodical title master, optional relationships for title changes, volume and issue text, printed date text, and optional sort date. A physically bound annual volume can remain one inventory item.
- Maps, posters, postcards, coin photographs, VHS, DVDs, and other supported types reuse shared physical and descriptive fields where practical. Newspapers may use flexible date text and a sortable date.
- Inventory number: immutable human-readable identifier distinct from immutable internal ID. New format `<source customer code>-<two-digit acquisition year>-<four-or-more-digit sequence>`; sequence runs across acquisitions from the same source in the same acquisition year and restarts each year, allocated atomically only on explicit successful Save. Legacy identifiers remain unchanged; never reuse assigned numbers.
- Duplicate handling: warn about possible duplicates without blocking legitimate distinct copies; deactivate erroneous duplicates and link to the correct record with reason and audit trail.
- Copy Item creates a local unsaved draft copying editable bibliographic fields, contributors, publishers, subjects and order, descriptions, condition, size, pages, regular retail price, and weight. Do not copy inventory number, photos, acquisition/source/ownership, storage box, cost, invoice, auction/sale status, or transaction history. Require selection of new acquisition, source, owner, and storage location before save.
- Configurable required fields by inventory type and workflow stage (Save, Website Publish, Auction Preparation). Storage box/location is required by default. Protect immutable integrity requirements; allow reasoned, audited administrative exceptions only for configurable requirements. Preserve drafts and show focused validation feedback.

- **Changing a saved inventory item type:** This is an ordinary authorized edit, not restricted to administrators solely because of the type change. Before committing, preview affected fields and any incompatibility; preserve data wherever possible, block silent loss, require confirmation, and audit the change.

## 4. Local drafts and save behavior

- Autosave unsaved work locally on the Windows computer approximately 30 seconds after edits; do not synchronize drafts to the cloud.
- Support multiple indefinite drafts until explicitly saved or discarded, including pending photo selections and changes; recover after unexpected restart.
- Draft list shows identifying title/type, modified time, photo indicators; count appears in status bar/dashboard.
- Do not create incomplete central inventory records or allocate a permanent inventory number before a successful explicit Save.
- Before navigating away or closing a modified record, offer Save, Discard, or Continue Editing.
- Treat database and Dropbox partial failures explicitly; never claim full success if record or media storage is incomplete.

## 5. Images and documents

- Unlimited JPEG/JPG/PNG photographs per item; multi-select picker and drag/drop, immediate thumbnails, add later. First image defaults to primary; reorder via drag/drop.
- Correct EXIF orientation; manual left/right rotation, freeform crop, preview/reset. Do not add brightness, contrast, or artistic filters.
- Keep original item images in Dropbox associated with immutable inventory number, not physical box folder; never automatically move or delete photos when an item sells. Replacing an image replaces the current version, rather than keeping visible photo versions.
- Generate optimized website thumbnails/copies while preserving originals except when the user explicitly replaces an image.
- Auction lots may override included photos and their order independently of inventory image order.
- For iCollector, export a flat folder of sequential <lot>-<sequence>.jpg files; convert PNG to high-quality JPEG, preserve source pixel dimensions, avoid automatic resizing, and flag any actual upload constraints.
- After changes to a lot already uploaded to iCollector, create a manual “iCollector Photo Update Needed” or relevant update flag until confirmed.
- Preserve the existing Dropbox Website/ tree and historic auction/document folders. Maintain versioned auction catalogs and dated backups.

## 6. Auction structure, preparation, and numbering

- An auction contains one or more sessions and provisional lots. Auction lots may be created before numbering; one or many inventory items linked to each lot. Allow adding a missing item later.
- Multi-item groups count as one lot for session-size planning. One outside consignor may be mixed with Workman’s Books-owned items; never combine inventory from two different outside consignors.
- Auction preview can publish eligible cataloged items before lot numbers, opening bids, estimates, or bidding links exist; visibility controlled at auction and individual lot level.
- Finalize lot numbers once the full auction is ready, after sorting and manual review. Number consecutively across all sessions. Do not silently renumber after iCollector upload.
- Default category sequence: BOOKS; CATALOGS/FPLs; MAGAZINES/JOURNALS/NEWSLETTERS; MAPS; POSTERS; NEWSPAPERS; COIN PHOTOS; POSTCARDS; VHS; DVDs.
- Sort books by author surname then publication date; catalogs/FPLs by firm then sale date; serial publications by title then date; maps/posters/newspapers/postcards/VHS/DVD by publisher then date; coin photos by sale title. Allow custom category sequence, drag/drop lot overrides, and restore auto-sort.
- Aim for ~720 lots per session as a soft target while keeping categories together. Warn rather than force a split when a category exceeds target. Sessions occur on consecutive calendar days by default.
- Session close time defaults to 10:00 AM America/New_York (DST aware), individually overridable; final session close date governs auction deadlines.
- After final numbering and upload confirmation, make lot numbers, starting bids, estimates, and iCollector bidding links visible as appropriate.

### Version 2.0 auction pricing, reserve, and completion requirements

- **Auction reserves:** Reserve price is an optional **lot-level** field, blank by default. Do not automatically convert an item-level consignor minimum to a reserve or sum minima into a lot reserve. Starting bid is generally the practical minimum in the current Workman's Books auction workflow. If a starting bid appears to conflict with an agreed consignor minimum, display a **non-blocking warning** and record acknowledgment; do not silently alter the bid. Any actual consignor agreement or contractual restriction must be reviewed separately and cannot be assumed waived by acknowledging a software warning.
- **Auction pricing defaults:** Starting bid, low estimate, and high estimate start **blank**; all three are required for auction finalization. Reserve remains optional.
- **Post-auction promotional eligibility:** Auction assignment suspends retail availability and promotional eligibility. An unsold item is **not** automatically republished or re-enrolled; during manual retail republishing, offer to restore a still-active campaign price only with owner approval.

- New lot pricing fields default blank: starting bid, low estimate, high estimate, and optional confidential reserve. Starting bid and both estimates are required **at finalization**, not while saving provisional lots. Validate high estimate >= low estimate. If low estimate < starting bid, show an acknowledged non-blocking warning.
- Support bulk lot pricing for selected lots, updating only selected fields, with preview, confirmation, consignor-minimum warnings, and audit. _Copy Previous Lot Pricing_ remains a **possible future convenience**, not a committed requirement.
- Audit all changes to starting bid, estimates, and reserve with old/new values, user, date, and optional reason. Reserve is visible only to authorized administrators and excluded from public catalog/website/export descriptions; verify external iCollector reserve capabilities before relying on external enforcement.
- After auction finalization, permit edits to lot title, description, pricing, and auction-lot image selection/order without renumbering. Log changes and mark previously uploaded iCollector listings as requiring manual updates. Image exports regenerate sequential `<lot>-<sequence>.jpg` files; preserve underlying inventory photos separately.
- Completed auction catalogs, pricing, and images become read-only except authorized corrections. Payment collection, shipment, refunds, and settlements continue independently. Administrative Reopen Auction requires a reason, audit event, and explicit subsequent re-completion; affected issued financial documents are flagged for review rather than silently rewritten.
- Mark Auction Completed is a **manual** action after review. Completion checklist distinguishes blocking missing/unreviewed lot results from acknowledged noncritical warnings, including inventory status and financial discrepancies. Buyer payment, shipping, and consignor settlement need not be finished before auction completion.
- Approved auction results may generate buyer invoices **before** the auction is marked Completed.

- **Persistent iCollector Update Needed status:** Any change affecting an already uploaded lot sets an outstanding update flag (including title, description, price, photos, or other exported data). The flag persists across sessions, appears in the Message & Status Center, and is cleared only by an explicit user confirmation after the external listing is updated. Audit the confirmer and timestamp.

## 7. Auction lot descriptions and weights

- Produce single-item and multi-item lot descriptions from linked inventory records; permit manual edits and custom commentary.
- Multi-item description style: introductory heading, numbered (1), (2), etc. bibliographic entries with semicolon-separated details, concluding commentary, lot weight, and subject(s). Preserve the owner’s established cataloging style.
- If source inventory changes, refresh uncustomized lot fields; preserve customized descriptions and flag them for review instead of overwriting.
- Single-item lot weight defaults to its item weight, editable. For multi-item lots, physically measured combined lot weight is authoritative; sum of individual weights may be displayed as reference only.
- Store lot-level starting bid, low/high estimates, selected photos, category, sequence, and change history.

## 8. iCollector and auction publication

- Generate the established iCollector CSV with columns A lot number, B title, C description, D starting bid, E blank, F low estimate, G high estimate, H category ID. Validate before export.
- Generate lot-numbered JPEG photo folder independently from CSV. No unverified assumption of an iCollector API or automatic two-way sync.
- Track manual iCollector updates required when previously uploaded titles, descriptions, images, or other fields change. User confirms resolution.
- Stage imported auction results and validate lot matches, buyer/customer mapping, premiums, and sale status before committing.
- Produce Word catalog and PDF variants with/without covers using the existing layout as a reference, with versioned output and manual publication controls.

## 9. Auction results, relisting, and historical records

- Maintain permanent auction/session/lot history for each inventory item, including bids/estimates, outcome, hammer price, and links to prior lots.
- After an unsold auction, release eligible items to ACTIVE inventory internally with their existing retail price; do not automatically republish them to the website or restore promotional enrollment. Manual retail republishing is required, and a missing retail price blocks public purchase.
- Allow one-click relisting of an unsold single item or entire previous multi-item lot into a new auction when all items remain available. Copy description, title, bids/estimates, photo selection/order, and source link; allocate new lot number only at finalization.
- When only some members of a previous group remain available, offer “Relist Available Items,” explicitly flag count, descriptions, group weight, bids/estimates, and allocations for review.
- Default to most recent auction lot as the relisting source; preserve earlier auction history. Do not automatically discount bids, estimates, or retail prices.

## 10. Customers, consignors, and ownership

- One customer master can act as buyer, seller, consignor, or source; unique customer code, multiple emails/phones, billing/shipping addresses, payment preferences, resale certificates, and notes.
- Maintain want lists and matching suggestions, including approximately 90-day follow-up workflow.
- Consignor agreements and commission rates are associated with consignor records and relevant settlement terms; preserve historical terms for completed sales.
- Track owned-versus-consigned allocation within mixed auction lots, original source, current ownership, and transfers.

## 11. Hammer allocation and consignor settlements

- Default allocation of multi-item hammer proceeds is equal by inventory item; user may adjust percentages and must total 100%.
- For mixed lots, compute outside consignor commissions only on that consignor’s allocated hammer share. Workman’s Books-owned share incurs no consignor commission.
- Established commission example: 40% on first $100 of consignor-allocated hammer, then 25% on the remainder; actual per-consignor agreement may vary.
- Use deterministic decimal currency rounding, preserve allocations and rate snapshots, and generate auditable consignor settlements.
- Support approximately 30-day post-auction settlement batches, review, payment recording, and settlement history.

## 12. Retail sales, invoices, and fulfillment

- Support website, eBay, and auction sales without losing channel/source attribution or overselling inventory.
- Import and stage iCollector results; match buyers to customer records (email when appropriate), require review for ambiguous matches.
- Invoice with buyer premium, applicable tax, shipping, and $3 packing charge per purchased auction lot unless picked up; allow policy-driven adjustments.
- Calculate Florida sales tax based on applicable destination/pickup location and current rules; do not hardcode tax rates.
- Obtain shipping quotes from Stamps.com/USPS integration subject to API verification; include item weight and packaging weight.
- Create invoice PDFs and email individually via Gmail integration subject to authorization; payment links via Square or PayPal as supported. Record payments manually when needed.
- Require full payment before pull/pack/ship; produce box-based pull sheets; handle missing items/refunds; create labels and store tracking; support overdue reminders and applicable late policies.

### Retail prices, promotional campaigns, and website synchronization

- Maintain regular asking price separately from auction starting bid and promotional price. Log retail price changes with old/new value, actor, timestamp, and optional reason.
- Support bulk fixed-amount, percentage, and fixed-price changes with preview, confirmation, validation, history, and website sync. Normal minimum retail price defaults to $5, and suggested bulk rounding defaults to nearest $5; both configurable. Explicit authorized **blowout** mode may set prices below $5, such as $1/$2/$3, bypassing normal rounding and minimum with confirmation.
- Website initial publishing, unpublishing, and post-auction republishing require deliberate user actions. Changes to an already published item's price, photos, or description synchronize after database save; failures create retryable status messages. Assigning an item to an auction immediately unpublishes it. Unsold items remain unpublished pending review.
- Named promotions may contain many inventory items, with campaign name, notes, schedule, discount method, item-level effective promotional prices, status, and permanent history. Support percentage, dollar reduction, and fixed promotional price, with bulk preview and confirmation. An item may not participate in overlapping active/scheduled promotions; show conflicts and permit explicitly replacing or rescheduling them.
- Promotion scheduling uses `America/New_York`. A start date begins at 12:00 AM Eastern; an end date remains effective through the end of that local calendar date, restoring the regular price at the following midnight. Handle DST transitions. Website display includes a struck-through regular price and prominent sale price; optional savings amount/percentage.
- Preserve the regular retail asking price throughout promotions. Auction assignment suspends participation; if unsold and manually approved for retail republishing while the original campaign remains active, offer to resume the promotional price for the remaining term. Do not resume automatically.
- Promotional sales reports include participating and sold counts, regular retail value, actual merchandise revenue, discount totals, sell-through, unsold inventory, transaction drill-down, and CSV/Excel export. Snapshot campaign attribution at sale time for historical accuracy.
- Consigned items may be included in promotions only with explicit approval; show the impact on consignor proceeds. Optional per-item consignor minimum selling price constrains ordinary retail pricing, discounts, and blowout promotions; revisions require authorization and audit. Keep the consignor minimum distinct from auction starting bid and optional lot reserve.

### Invoice email delivery and reminders

- Designated outbound email account: `workmansbooks@gmail.com` (consumer Gmail). Proposed integration: Gmail API with OAuth 2.0 and least-privilege send permission; verify Google project consent/verification and sending limits during implementation planning. Do not store Gmail passwords.
- Support individual invoice review/send and batch review/send of approved invoices, each with attached generated PDF. Persist recipient, subject, body snapshot, send timestamp, Gmail message ID when available, and delivery-submission status. Only mark sent after API acknowledgment; retry failed sends without duplicating successful ones.
- Editable invoice email subject/body templates with buyer, auction, invoice, balance, and payment-instruction placeholders; per-message override and batch personalization. Editable business signature (name, contact details, website, optional logo) under Settings. Buyer replies go to the regular Gmail inbox; inbound email integration is not required.
- Overdue invoice reminder threshold defaults to seven days and is configurable. Allow manually approved individual or batch reminder emails with separate template, current outstanding balance, prior reminder count/date, and reminder history. Permit multiple reminders, with configurable minimum-interval warning that may be acknowledged. Never automatically email reminders without approval; cease overdue notices when fully paid.

### Payment methods, surcharges, customer credits, and refunds

- Record multiple partial payments per invoice with amount, date, payment method, reference, and actor. Compute unpaid/partially paid/paid-in-full status and current outstanding balance. Release/ship goods only after required full payment.
- Record the full buyer payment amount separately from actual payment-processor fees (expense) and net deposit. Payment method master is configurable (initial values PayPal, Square/credit card, check, cash, bank transfer, other); deactivation must not alter historical transactions.
- Customer master supports optional default preferred payment method, suggested on new invoices and overrideable. The actual method used may differ from the preferred or originally requested method, including when a credit-card payment link was sent but a check arrives. Recalculate unpaid amounts and any legally permitted surcharge; preserve original requests and payment history. Payment-history-based suggestions are approved and require explicit acceptance; never change the preference automatically.
- Requested surcharge policy: 3% for credit-card payments and 4% for PayPal; zero by default for check/cash/bank transfer. Preferred calculation base is the **full pre-surcharge invoice balance**, including merchandise, buyer premium, packing, shipping, and sales tax, excluding the surcharge itself. Display separately, recalculate when method or balance changes, and permit authorized waiver/adjustment. **Do not activate these rules until verified against Florida law, card-network rules, PayPal/Square agreements, and applicable tax/accounting treatment.** Some payment methods or funding sources may prohibit the surcharge or require a different cap or calculation basis. Configure policy per payment method and funding type as necessary.
- Overpayments create customer credits, not extra merchandise revenue. Customer credits do not automatically expire, subject to applicable law. Display available credit on subsequent invoice creation; application to invoices requires explicit approval. Track partial applications and balances.
- Record manual full/partial refunds of customer credit by selected method (PayPal, Square, check, cash, etc.), transaction reference, date, actor, and confirmation preview. Initial application **records** refunds but does not initiate them through processors. Never refund more than available credit.
- Correct erroneous payments using audited **void-and-replace**, never destructive overwrite. Require reason, preserve original record, recalculate balances and credits, and flag downstream documents for review. A void in the app does not reverse external payment settlement.
- Financial ledger must distinguish invoice charges, surcharge revenue or offset, processor fees, cash receipts, credit liabilities, refund outflows, and consignor proceeds. Accounting classification and tax treatment require validation before implementation.

- **Invoice email recipient override:** In both individual and batch Send Email previews, the recipient address is editable per send. By default, an override changes only that outbound message; updating the customer contact record requires a separate explicit choice. Audit the actual recipient address used.
- **Payment preference suggestions:** When recent payment history consistently differs from the saved customer default (for example, three consecutive payments by check rather than PayPal), suggest—but never automatically apply—an update to the default payment method. The owner may accept or dismiss; audit accepted changes. The suggestion threshold is configurable.
- **Scheduled promotion execution:** Activation and expiration must run through a reliable backend scheduler, even when no user is logged in or the application is closed. Log and surface scheduling or synchronization failures in the Message & Status Center. Confirm the hosting environment supports this.

## 13. Accounting, reporting, and retention

- Track sales income, commissions, fees, expenses, mileage, payments, refunds, settlements, and relevant audit trails.
- Provide inventory, sales, auction, consignor, receivables, and financial reports; allow Excel/CSV exports.
- Support year-end exports aligned with the owner’s existing tax workbook workflow, without assuming full accounting software replacement.
- Retain sold records, historical auctions, photos, and financial records indefinitely unless an explicit retention policy is approved.
- Back up database and documents to dated Dropbox backup locations, but do not use Dropbox as the live transactional database.

## 14. Optional AI assistance

- Quick Summary: draft text only from saved bibliographic data and notes.
- Research-Assisted Summary: optionally use external research and show visible sources for checking; do not treat unverified claims as facts.
- Suggest lot descriptions, subject terms, grammar edits, and concluding commentary; user approves text before saving.
- Do not automatically overwrite custom descriptions or store a separate permanent archive of research notes/sources.
- Make AI optional, disableable, and cost-controlled; core cataloging must work without AI.

## 15. Data integrity, security, and operations

- Central relational database with referential integrity, immutable business identifiers, explicit transactions, and audit history.
- Local drafts must not be confused with saved central records. Prevent double selling, duplicate inventory numbers, cross-consignor lot violations, and incomplete financial allocations.
- Use authenticated, least-privilege access to database and Dropbox/Gmail/payment/shipping services; secrets never embedded in exported files or source code.
- Define backup, restore testing, migration, and failure recovery before production use.
- Make partial failures actionable in the Message & Status Center; preserve failed operations for safe retry without accidental duplication.

### Initial access-control roles

- Provide individual accounts and **Administrator** and **Staff** roles in the initial schema, even if only one account is active at launch. Administrator has full control; Staff is restricted from sensitive administrative/financial actions such as refunds, auction reopening, and financial corrections unless specifically authorized. Enforce permissions on the backend and audit significant actions. Final permission matrix remains subject to design review.

## 16. Conceptual data areas — historical candidates, reconciled against the approved working inventory

| Master records | customers; addresses/contact methods; inventory_items; item-specific details; boxes; ownership history; inventory_images |
| Auction records | auctions; auction_sessions; auction_lots; auction_lot_items; auction_lot_images; catalog versions; iCollector sync state; auction results |
| Commerce/finance | sales/orders; invoices; invoice lines; payments; shipments; refunds; allocations; consignor settlements; expenses; mileage |
| Operations | audit events; business messages; export/import batches; user preferences; saved searches/templates; integration status |
| Local-only storage | Draft content and attachments, local technical notifications, workspace recovery |

These are historical conceptual groupings. The approved working inventory of 144 logical table names is documented in the addendum below; it supersedes candidate names where they conflict. A completed ERD, physical definitions, and schema-wide sign-off are still pending.

### Additional conceptual entity candidates

The following are **historical candidate** entities/relationships for schema review, not approved physical table definitions. Refer to the Findings 1–150 addendum for the current working inventory:

| Domain                 | Candidate entities or extensions                                                                                                                                                                                                                                             |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Inventory metadata     | inventory_item_types, inventory_items, contributors, item_contributors, publishers, publisher_relationships, item_publishers/publication_publishers, book_isbns, periodical_titles, periodical_title_relationships, periodical_issue_details, inventory_required_field_rules |
| Pricing and promotions | inventory_price_history, promotions, promotion_items, promotion_exclusions/events, promotional_sale_attribution, consignor_minimum_history                                                                                                                                   |
| Auctions               | auction_lot_pricing_history, auction_lot_reserve, auction_completion_checklist/events, auction_reopen_events, iCollector update flags, auction_lot_image history                                                                                                             |
| Messaging              | email_templates, email_signatures, outbound_email_messages, email_send_attempts, invoice_reminders                                                                                                                                                                           |
| Payments and credit    | payment_methods, customer_payment_preferences, invoice_payments, payment_voids, payment_processor_fees, invoice_surcharges, customer_credit_ledger, credit_applications, credit_refunds                                                                                      |
| Cross-cutting          | audit_events, authorized_exceptions, workflow_validation_results, external_sync_status                                                                                                                                                                                       |

Prefer normalized relationships, durable immutable transaction snapshots, clear ownership boundaries, idempotent external sync, and auditable financial corrections. Determine exact entities and cardinalities in the conceptual schema review rather than assuming one table per feature.

- **Schema deliverables:** Produce an overall visual entity-relationship diagram (ERD), smaller ERDs by business area, and a detailed table-by-table reference documenting fields, types, primary/foreign keys, relationships, constraints, and business rules. These are design deliverables requiring owner approval, not yet approved physical tables.

## Customer database design decisions — October 2026 review addendum

**Review status:** All 127 customer decisions confirmed by owner on 20 October 2026. This addendum supplements, but does not replace, the approved 16 October 2026 SRS v2.0 baseline. The companion `docs/decisions/CUSTOMER_DATABASE_MASTER_DECISION_LOG.md` records customer design Questions 1–127, their source and review status. The uploaded Q1–96 transcript is the source for the earlier decisions; Q97–127 were recorded in the continuation. Q96 was unanswered in the uploaded Word source and subsequently approved by the owner as Option A.

### Customer identity and structure

- One customer may hold multiple independent roles (buyer, consignor, inventory source); support individual and business customers, business contact persons, multiple addresses, emails and phone numbers.
- Use an internal numeric `customer_id` primary key distinct from a permanent unique `customer_code`. Assign code only on successful save; never change or reuse it.
- **Final approved code convention:** five uppercase letters plus a two-digit decimal suffix `01`–`99` (`^[A-Z]{5}(0[1-9]|[1-9][0-9])$`). Generate prefix from surname then given name for individuals, first five letters of business name for organizations, pad short prefixes with `X`; middle names excluded. Allow edits before initial save. Examples: `SMIJO01`, `LIJOH01`, `LIBOX01`, `WORKM01`. These final decisions supersede earlier interim suggestions in the transcript.
- Support duplicate detection without automatic merging; administrator-only confirmed merges preserve transaction history, identifiers and audit records. Support inactive records, searchable previous names and aliases, relationships, roles, tags, notes, contact history, reminders, external IDs, communications preferences and customer documents.
- Customer profile uses a left-side section menu; searchable/filterable customer list with configurable columns, imports and exports; account summary and activity timeline derive from associated records without duplicating financial facts. Optional profile image/logo deferred.

### Tax-exemption and Dropbox certificate workflow

- Maintain separate customer tax-exemption records with jurisdiction, type, certificate number, validity dates, verification/approval status, linked renewals, history and per-invoice usage. Only approved, applicable certificates affect new/unfinalized invoices; finalized invoices retain historical calculations and use explicit audited corrections.
- Administrators manage certificates, reviews, overrides, reports, bulk imports, archival and role-specific permissions. Expiration notifications are configurable; approval, overrides and edits are audited.
- Store certificate documents in a central Dropbox folder, referenced from the database. File naming: `CustomerNumber_TAX_CERT_Year.extension`, with `_02`, `_03` suffixes for collisions. Support PDF/JPG/PNG, document versions, authorized in-app preview/download, initial integrity verification, secure temporary failed-upload retention and retry. Rely on Dropbox's document version/recovery features for these files; **database backup and disaster recovery remain a separate unresolved technical design task**. Clarify the certificate filename `CustomerNumber` mapping during schema design; do not assume it means the immutable seven-character customer code or internal numeric ID.

### Additional confirmed customer-design rules

- **Q58/Q62:** Track role assignment and removal history. Enforce only one active assignment per `(customer_id, role_id)`, allowing later reassignments as new historical rows.
- **Q63–76:** Email, phone and address information supports multiple records and history; shared contact details are allowed with duplicate warnings. Support optional address `care_of` and `address_notes`, separate billing/shipping defaults, and country-specific output formatting. Historical invoice/shipping snapshots retain actual values used.
- **Q77–81:** Business-specific contact records, optional contact-level emails/phones and multiple communication purposes; preserve former contacts as inactive, without automatically linking the same person across employers.
- **Q82–88:** Dated categorized notes with audit, soft-delete/restore, document/reminder links, plus searchable general profile notes; no administrator-only note visibility level.
- **Q89–92:** Categorized administrator-configurable customer tags, Match ANY/ALL filtering, and historical assignments with active-only uniqueness.
- **Q93–96:** Store one bidirectionally visible relationship, including reverse type names and optional effective dates. Prevent duplicate **active** relationships in either direction for the same relationship type; allow distinct relationship types and retain ended history.
- **Q97–116:** Certificates have approval/renewal/expiry/revocation states, administrator-managed reporting/imports, immutable finalized invoice usage, explicit invoice corrections, and validation before approval. Recalculate affected unfinalized invoices on rejection/revocation.
- **Q117–127:** Store versioned certificate documents in Dropbox with secure database references, admin permissions, collision-safe naming, app-driven uploads, pending-upload retry, initial verification, and authorized preview/download.

### Approval and implementation gate

- **Q96 approved:** The owner confirmed Option A on 20 October 2026. Reverse-direction duplicate active relationships are blocked, while distinct types between the same customers are allowed.
- This addendum records detailed customer design choices; it does not approve a physical schema, specific SQL DDL, Dropbox API configuration, tax-law determination, or production changes. Validate permissions, hosting, retention, backup/restore and integrations before implementation.

## 17. Dependencies, validation, and unresolved decisions

- Verify GoDaddy hosting supports the required database version, secure remote connections, transaction behavior, backup/restore, performance, and deployment model; consider alternative hosting if not.
- Confirm whether a browser-hosted UI, packaged Windows desktop shell, or hybrid best supports local drafts, filesystem/photo operations, and integration security.
- Inspect actual legacy spreadsheets, VBA iCollector export, catalog templates, inventory records, and Dropbox folder conventions before specifying migration mappings or final exports.
- Validate Stamps.com, Gmail, Square/PayPal, iCollector, and website/eBay interfaces and any access limitations before promising automation.
- Finalize detailed role permissions, authentication, data protection, retention, and disaster recovery in technical design; Administrator and Staff roles are required from the initial schema design.
- Finalize inventory number generation/legacy migration, category dictionaries, type-specific fields, customer matching rules, tax handling, rounding, and report definitions in schema review.
- Set nonfunctional targets (expected inventory size, concurrency, search latency, backup frequency, availability, and maximum import sizes) after measuring actual business needs.

### Outstanding validation and reconciliation items

1. Review the actual source Excel workbooks, legacy macros, catalog templates, and current Dropbox structure before finalizing migration mapping or exports.
2. Validate GoDaddy/MySQL/MariaDB hosting feasibility, secure remote access, backup/recovery, and the chosen Windows/browser deployment model.
3. Validate Gmail API permissions and sending constraints; Stamps.com, Square/PayPal, iCollector, website/eBay integration boundaries.
4. Confirm legally and contractually permitted surcharge policies and treatment of taxes, partial payments, refunds, and mixed payment methods. Until confirmed, surcharge settings are **requested policy**, not enabled behavior.
5. Define how individual consignor minimums are reviewed for **multi-item lots** and how contractual commitments are honored when starting bids are lower. A warning alone must not imply consent to violate a consignor agreement.
6. Define the precise moment an invoice becomes immutable and the corrective document process (adjustment, credit note, or reissue), including payment-link reconciliation.
7. Specify roles/permissions, security, nonfunctional targets, transaction concurrency, import sizing, and retention/backup policies before logical schema approval.
8. Verify whether optional automation and future features warrant implementation in the first release or should remain backlog items.

## 18. Proposed approval and delivery sequence

1. Maintain this owner-approved requirements baseline and manage future changes through documented revisions.

2. Inspect source files and existing workflows; document field mappings and exceptions.

3. Draft conceptual entity-relationship model and business invariants; review with owner.

4. Validate hosting and integration feasibility; approve architecture and security plan.

5. Produce logical schema, migration plan, UI flows, and acceptance criteria.

6. Only after explicit approval: implement in staged milestones, test with representative data, and rehearse restore/migration.

### Review and implementation gate

- All nine Version 2.0 review sections (19–27) were approved by the owner on 16 October 2026. Approval applies to business requirements and the planned design process, **not** to a logical/physical database schema, architecture deployment, API credentials, or coding.
- Begin conceptual modeling with Customers and Inventory, review one area at a time, and obtain explicit approval before creating tables or changing production systems.

## Logical schema reconciliation addendum — Findings 1–150 (27 October 2026)

**Owner-approved design decisions, not an implementation authorization.** The review paused after approval of Finding 150, Option A. Findings 1–150 are approved at the decision level; 144 logical table names have been approved as a working inventory. Table-by-table columns, constraints, relationships, ERDs, physical schema, and final sign-off remain outstanding. Continue with Finding 151 only after owner acknowledgment of the checkpoint.

### Working logical table inventory

**Customer and application — 44:** `customers`, `customer_roles`, `customer_role_assignments`, `customer_name_history`, `customer_emails`, `customer_phones`, `customer_addresses`, `customer_address_purposes`, `customer_contacts`, `customer_phone_sms_consent_history`, `customer_relationships`, `customer_relationship_types`, `customer_notes`, `customer_note_categories`, `customer_note_revisions`, `customer_activity_revisions`, `customer_activity_types`, `customer_activity_log`, `customer_communication_preference_history`, `customer_communication_preferences`, `customer_interest_categories`, `customer_interests`, `customer_document_categories`, `customer_documents`, `customer_document_versions`, `customer_payment_terms`, `customer_tax_exemptions`, `customer_account_holds`, `customer_account_restriction_types`, `customer_account_restrictions`, `customer_financial_profiles`, `application_audit_log`, `customer_wants`, `customer_want_matches`, `customer_auction_eligibility_history`, `application_messages`, `customer_import_batches`, `customer_import_records`, `application_users`, `application_roles`, `application_user_roles`, `application_permissions`, `application_role_permissions`, `application_user_preferences`

**Inventory and promotional — 37:** `inventory_items`, `inventory_acquisitions`, `inventory_ownership_history`, `inventory_box_history`, `books`, `catalogs`, `magazines`, `magazine_articles`, `inventory_images`, `inventory_item_types`, `subjects`, `inventory_item_subjects`, `contributors`, `book_contributors`, `publishers`, `publication_publishers`, `publisher_relationships`, `inventory_number_sequences`, `periodical_titles`, `inventory_price_history`, `promotions`, `promotion_items`, `acquisition_payments`, `acquisition_documents`, `website_sync_events`, `inventory_required_field_rules`, `book_isbns`, `periodical_title_relationships`, `inventory_saved_searches`, `inventory_export_templates`, `inventory_import_batches`, `inventory_import_rows`, `inventory_validation_exceptions`, `inventory_import_issues`, `inventory_duplicate_links`, `inventory_consignor_minimum_history`, `inventory_commission_agreement_assignments`

**Auction — 13:** `auction_inventory_assignments`, `auctions`, `auction_sessions`, `auction_lots`, `auction_lot_items`, `auction_import_batches`, `auction_import_rows`, `auction_import_issues`, `auction_lot_changes`, `auction_catalog_versions`, `auction_launch_checklist_items`, `auction_lot_images`, `auction_lot_field_overrides`

**Invoicing and payment — 12:** `buyer_invoices`, `buyer_invoice_items`, `invoice_payments`, `invoice_payment_requests`, `payment_methods`, `customer_credit_ledger`, `credit_refunds`, `invoice_refunds`, `email_templates`, `outbound_email_messages`, `invoice_reminders`, `invoice_late_charges`

**Consignor settlement and commission — 10:** `consignor_settlements`, `consignor_settlement_lines`, `consignor_payouts`, `consignor_payout_allocations`, `consignor_invoice_offsets`, `customer_account_adjustments`, `consignor_commission_agreements`, `consignor_commission_tiers`, `consignor_adjustment_recoveries`, `consignor_repayments`

**Inventory pulling — 2:** `inventory_pull_sessions`, `inventory_pull_session_invoices`

**Auction shipping — 2:** `shipping_packages`, `shipping_package_lots`

**Fulfillment exceptions — 1:** `fulfillment_exceptions`

**Online sales — 9:** `online_sales`, `online_sale_items`, `online_sale_platform_fees`, `online_sale_fee_allocations`, `online_sale_fee_adjustments`, `online_sale_refunds`, `online_sale_payments`, `online_shipping_packages`, `online_shipping_package_items`

**Business accounting and settings — 14:** `business_expenses`, `expense_categories`, `expense_attachments`, `payment_accounts`, `business_vehicles`, `business_trips`, `business_trip_stops`, `sales_tax_filings`, `florida_sales_tax_rates`, `bookkeeping_reminders`, `accounting_years`, `application_settings`, `financial_report_versions`, `financial_report_files`

**Count:** 44 + 37 + 13 + 12 + 10 + 2 + 2 + 1 + 9 + 14 = **144**. No `customer_drafts` table: drafts persist on the local Windows device.

### Approved accounting and financial controls (Findings 101–150)

- Consignor overpayment recoveries, repayments, credit liabilities, supplemental payables, failed payouts, and reversals preserve finalized settlements and full audit trails; `consignor_repayments` was added in Finding 103.
- Accounting years can be closed and reopened only with authorized reasons. Later corrections normally affect the current open period; original event dates remain intact.
- `financial_report_versions` (Finding 118) and `financial_report_files` (Finding 121) track immutable finalized report snapshots, multi-file exports, SHA-256 checksums, protected local copies, Dropbox package synchronization, controlled delivery, version history, retention and legal holds.
- Financial report access uses granular backend-enforced permissions for viewing, generating, downloading, finalizing, delivering, and managing reports. Revocations take effect on subsequent protected actions; audit all sensitive operations.
- Finalized report delivery is blocked until all Dropbox package files are synchronized and checksum-verified. Local view/download during an outage is permitted for authorized users with matching protected local copies; external delivery remains blocked. Dropbox verification is on access or Administrator-initiated, not scheduled.
- Initial financial reporting is **cash basis, pending accountant confirmation**. Preserve receipt, payment, transaction, settlement and bank deposit dates separately. Refunds and reversals are recognized according to actual cash movement dates subject to accountant-approved classification.
- Use existing `business_expenses`, `expense_categories`, `payment_accounts`, and audit records with distinct classifications for owner contributions/withdrawals, account transfers, bank fees and interest, business loans, personal-fund reimbursements, split-funded purchases, credit card purchases and bill payments, and manual credit card statement reconciliation. Avoid double counting and do not classify principal/transfers as operating income or deductible expenses.
- Detailed processor payout-batch reconciliation, loan amortization, automated bank/credit card imports, and accrual accounting/journal generation are deferred.

### Full approved finding register (61–150)

For exact decision context, consult the continuity checkpoint and prior approved conversation. The following is a concise handoff register, not a replacement for detailed approval records.

- 61. Add application_users for authenticated actors and audit identity.
- 62. Add application_roles.
- 63. Add application_user_roles; protect last active Administrator.
- 64. Add application_permissions with backend enforcement.
- 65. Add application_role_permissions; default deny.
- 66. Add application_user_preferences; customer drafts remain local.
- 67. Add inventory_import_issues for per-row validation issues and resolution.
- 68. Add inventory_duplicate_links; authorized reversible canonical links, legitimate copies remain distinct.
- 69. Add auction_lot_field_overrides; preserve manual auction copy and iCollector update flag.
- 70. Add inventory_consignor_minimum_history; item-level commitments and evidence.
- 71. No table: minimum_basis GROSS_SALE_PRICE or NET_CONSIGNOR_PROCEEDS; verify agreement.
- 72. No table: test each consigned item in multi-item lots against allocated proceeds and minimum.
- 73. Add consignor_commission_agreements and consignor_commission_tiers; versioned terms.
- 74. No table: revised agreements affect new accepted inventory by default; existing inventory needs authorized reassignment.
- 75. Add inventory_commission_agreement_assignments; effective-dated item/channel mapping.
- 76. Add application_settings; typed global settings, controlled financial enablement.
- 77. No table: setting changes audited in application_audit_log.
- 78. No table: authorized settings apply immediately; future reminders use existing mechanism.
- 79. No table: completed sale/final settlement commission versions locked; correction by adjustment.
- 80. No table: commission terms selected when item sells, not at lot finalization.
- 81. No table: actual sale time selects commission version and is snapshotted.
- 82. No table: if actual time missing, use scheduled session closing time marked ESTIMATED in America/New_York.
- 83. No table: later discovered actual time is informational; estimated financial reference stays unless authorized contractual correction.
- 84. No table: missing/invalid hammer blocks affected result approval, invoice and settlement until verified.
- 85. No table: missing/ambiguous buyer blocks affected invoice; preserve sale/hammer; unaffected proceed and consignor policy unchanged.
- 86. No table: reimports classified unchanged/new/changed/conflicting; deduplicate and preserve source batches.
- 87. No table: conflicting sale results require authorized reconciliation; one authoritative sale per lot.
- 88. Option B, no table: verified SOLD→UNSOLD automatically updates authoritative result; flag financial corrections, no automatic refund or retail release.
- 89. No table: corrected UNSOLD item requires authorized location/ownership/disposition confirmation before availability change.
- 90. No table: verified UNSOLD→SOLD automatically adopted subject to intervening inventory conflict safeguards.
- 91. No table: verify lot-item linkage, ownership and allocations before affected financial approval/invoice/settlement.
- 92. No table: authorized audited allocation corrections; unsettled recalculation, finalized settlement adjustment; buyer invoice unchanged.
- 93. No table: evidence-supported historical ownership attribution correction; preserve acquisition and settlement history.
- 94. No table: evidence-supported commission agreement/version correction; unsettled recalculation, finalized adjustment.
- 95. No table: evidence-supported historical consignor minimum/basis correction; recheck compliance, no automatic financial changes.
- 96. Option B, no table: minimum violations resolved via existing notes/messages/audit/adjustments, no dedicated violation table.
- 97. Option B, no table: authorized settlement finalization despite unresolved minimum violation after documented acknowledgment; not waiver.
- 98. No table: preserve paid statements; underpayment supplemental payable, overpayment recoverable via future offsets or repayment.
- 99. Add consignor_adjustment_recoveries; individual partial recoveries linked to original obligation and settlement/repayment, prevent over-recovery.
- 100. Option A, no table: reverse and replace incorrect recovery entries, never edit/delete posted recovery; preserve final financial records.
- 101. A — Supplemental payable after reversed recovery has reduced an issued payout; preserve prior finalized transactions and original obligation.
- 102. A — Allocate multiple consignor overpayment obligations oldest-first by default, with authorized changes/splits and no over-allocation.
- 103. A — Add consignor_repayments; direct payments, references, allocation, clearing and reconciliation.
- 104. A — Repayment PENDING/CLEARED/REVERSED; verified reversals and linked replacements, no duplicate reversal.
- 105. A — Pending repayments reserve allocations provisionally, not completed recoveries; release on failure.
- 106. A — Partial clearance: post only cleared amount, release excess reservation, preserve discrepancy and authorized allocation.
- 107. B — Excess cleared repayment carried as consignor credit liability, usable on future payout or refundable.
- 108. A — Apply consignor credit as positive next eligible payout component, including cross-channel, without duplication.
- 109. A — Incorrect credit already paid: preserve payout, create recoverable obligation with evidence and audit.
- 110. A — Refund unused consignor credit through existing consignor_payouts, with reservation and duplicate prevention.
- 111. A — Refund PREPARED/ISSUED/CLEARED/CANCELED/FAILED states; verified failure before restoring credit.
- 112. A — Lost ordinary consignor payout check: verify stop/void, then linked replacement; preserve settlement.
- 113. A — Electronic payout failure/misdirection: verify provider outcome before replacement; completed misdirection needs loss/recovery handling.
- 114. A — Track recoveries of misdirected payouts, unrecovered balances, and authorized write-offs without changing consignor payout.
- 115. A — Recoveries after write-off recognized as linked later-period adjustment, not retroactive change.
- 116. A — Closed-year corrections normally posted in current open period; reopening requires Administrator reason and reclosure.
- 117. A — Late original transactions preserve original date, discovery/entry date and accounting period; accountant review.
- 118. A — Add financial_report_versions; report metadata, draft/finalized/superseded versions, delivery lineage.
- 119. A — Financial report snapshot/cutoff, detect source changes before finalization, immutable finalized version.
- 120. A — Finalized export SHA-256, size, name, path, verify on access and preserve original checksums.
- 121. A — Add financial_report_files; one record per report package file, purpose, format, path, size, checksum.
- 122. A — Restore missing/corrupt finalized files only from matching SHA-256 evidence, with authorization and audit.
- 123. B — Permit finalization with verified protected local files while Dropbox synchronization is pending; show separate sync status.
- 124. A — Persistent protected local archive through Windows restart; retention cleanup only after verified Dropbox archive.
- 125. B — Sync entire report package as a unit; failure means package failed, retry all, preserve local files.
- 126. A — Stable unique Dropbox path per version; reuse checksum-identical files, never overwrite conflicting content.
- 127. B — Block accountant delivery until entire Dropbox report package synchronized and SHA-256 verified.
- 128. B — Primary report delivery metadata in financial_report_versions; subsequent attempts/deliveries in application_audit_log; no delivery table.
- 129. A — Granular backend-enforced permissions for report view/generate/download/finalize/deliver/manage and supporting files.
- 130. A — Revoke permissions immediately for subsequent protected actions; revalidate exports before release, block stale links.
- 131. A — Retain completed export as controlled DRAFT if requesting user loses permission; authorized reassignment/review.
- 132. A — Retain drafts until authorized disposal, configurable inactivity reminders, controlled cleanup and audit.
- 133. A — Retain finalized/superseded reports indefinitely by default; authorized policy-based disposal, legal/audit holds.
- 134. B — Hold status/reasons in financial_report_versions and detailed audit history; clear only after all obligations resolved.
- 135. A — Detect missing/altered Dropbox files, block delivery, restore only with approval and matching SHA-256.
- 136. B — Verify Dropbox archives on access or Administrator manual check; no scheduled background verification.
- 137. A — During Dropbox outage allow authorized local view/download if SHA-256 verified; external delivery remains blocked.
- 138. B — Authorized manual retry of uncertain Gmail report sends with duplicate warning and full attempt audit.
- 139. A — Multi-year financial reports; capture year open/closed statuses, provisional labels, snapshots and cutoffs.
- 140. A — Cash-basis reporting initially, pending accountant confirmation; preserve dates, defer accrual and journal entries.
- 141. A — Refunds/reversals in actual cash movement period subject to accountant classification; link original, protect closed years.
- 142. B — Track processor collection vs bank deposit in existing records; prevent double-counting, defer payout batch table.
- 143. B — Owner contributions/withdrawals classified through business_expenses and payment_accounts, not operating income/expense.
- 144. B — Internal account transfers as linked outgoing/incoming entries using existing records, no revenue/expense duplication.
- 145. A — Bank fees via business_expenses/categories; interest income distinct, linked payment account and reconciled.
- 146. A — Basic business loan tracking via existing records; principal vs interest/fees, no loan tables or amortization.
- 147. A — Personally funded business purchases and linked partial reimbursements via existing records; no double-count.
- 148. B — Split-funded purchases as linked business_expenses records sharing purchase reference; reconcile total.
- 149. A — Credit card purchases distinct from later principal bill payments; interest/fees separate; reconcile statements.
- 150. A — Manual credit card statement reconciliation using existing records; statement balances, discrepancies, approval and audit; no new table.

### Open validation and design gates

- Confirm cash-basis treatment, tax classification, year-end adjustments, interest and refunds with the accountant; do not enable unverified financial policies.
- Verify Florida tax rules, card/PayPal surcharges, late charges, consent, retention and service-provider terms before implementation.
- Resolve precise fields and integrity constraints for using `business_expenses` for non-expense cash movements and statement-level reconciliation; preserve the approved no-new-table decisions unless the owner explicitly revisits them.
- Preserve the separate customer Q1–127 decision log. Its original Q128-on-hold reference pertains to the **customer questionnaire**, not logical reconciliation Finding 128 (approved Option B).
- No SQL, code, integrations, or production database changes are authorized.

## Appendix A. Examples and important rules

### Mixed ownership example

A $100 hammer lot contains one Workman’s Books-owned item and two items from one outside consignor. Default equal item allocation gives an approximately one-third owned share and two-thirds consigned share. Using the owner’s illustrative $66.70 consignor allocation, a 40% commission is $26.68 and consignor proceeds are $40.02; final cents must be reconciled deterministically to the actual $100 hammer total. The owned share is not charged a consignor commission.

### Auction preview rule

Before finalization: preview descriptions and photos may be visible, but not nonexistent lot numbers, starting bids, estimates, or bidding links. After finalization/upload confirmation: publish those fields as appropriate.

### Design guardrail

This is a requirements baseline for review, not a finished design. Any contradictions or unverified assumptions discovered during source-file inspection must be brought back for explicit resolution rather than silently implemented.

---

## Appendix B. Revision history and approval status

| Version                               | Date            | Status                                                     | Summary                                                                                                                                        |
| ------------------------------------- | --------------- | ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.0                                   | 12 October 2026 | Superseded baseline                                        | Initial consolidated requirements.                                                                                                             |
| 2.0                                   | 16 October 2026 | Owner-approved requirements baseline                       | Integrated approved review decisions from Sections 19–27 into relevant sections; established schema-documentation deliverables and RBAC roles. |
| 2.0 + Customer Addendum               | 20 October 2026 | Q1–127 owner-confirmed; schema pending                     | Reconciled customer decisions and Q96 approval without superseding the v2.0 baseline or approving SQL/implementation.                          |
| 2.0 + Logical Reconciliation Addendum | 27 October 2026 | Findings 1–150 owner-confirmed; 144 working logical tables | Documented decision-level approval and outstanding physical design/implementation gates.                                                       |

**Interpretation:** Explicit Version 2.0 provisions supersede conflicting Version 1.0 wording. Any remaining ambiguity must be resolved with the owner before implementation. Requested payment surcharges remain disabled pending legal, card-network, processor-contract, and tax verification.
