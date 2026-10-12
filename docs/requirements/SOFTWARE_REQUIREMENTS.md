# Workman's Books

**Software Requirements Specification · Version 1.0 · 12 October 2026**

Working draft for owner review — consolidated from our requirements discussions. No implementation, hosting changes, or database modifications are authorized by this document.

## 1. Purpose, scope, and decision status

Create a Windows-oriented business management application for Workman’s Books covering rare-book and related-item inventory, retail sales, auctions, customer and consignor relationships, fulfillment, accounting, and reporting. The application should preserve established cataloging and auction workflows while eliminating duplicate entry where practical.

| Approved business requirements | Items described in Sections 2–15 reflect decisions already made during planning. |
| Proposed architecture | React/TypeScript user interface; Node.js/TypeScript services; centralized MySQL/MariaDB subject to hosting feasibility; Dropbox for media/documents. |
| Not yet approved | Final conceptual/logical database schema, provider choice, infrastructure configuration, implementation sequencing, and deployment. |
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
- After an unsold auction, release items to ACTIVE inventory with their existing retail price; if missing, prompt and block public purchase until set.
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
## 16. Proposed conceptual data areas — not an approved schema

| Master records | customers; addresses/contact methods; inventory_items; item-specific details; boxes; ownership history; inventory_images |
| Auction records | auctions; auction_sessions; auction_lots; auction_lot_items; auction_lot_images; catalog versions; iCollector sync state; auction results |
| Commerce/finance | sales/orders; invoices; invoice lines; payments; shipments; refunds; allocations; consignor settlements; expenses; mileage |
| Operations | audit events; business messages; export/import batches; user preferences; saved searches/templates; integration status |
| Local-only storage | Draft content and attachments, local technical notifications, workspace recovery |

These are conceptual groupings, not a commitment to exact table names or a completed entity-relationship design.

## 17. Dependencies, validation, and unresolved decisions

- Verify GoDaddy hosting supports the required database version, secure remote connections, transaction behavior, backup/restore, performance, and deployment model; consider alternative hosting if not.
- Confirm whether a browser-hosted UI, packaged Windows desktop shell, or hybrid best supports local drafts, filesystem/photo operations, and integration security.
- Inspect actual legacy spreadsheets, VBA iCollector export, catalog templates, inventory records, and Dropbox folder conventions before specifying migration mappings or final exports.
- Validate Stamps.com, Gmail, Square/PayPal, iCollector, and website/eBay interfaces and any access limitations before promising automation.
- Specify user roles, permissions, authentication, data protection, retention, and disaster recovery in technical design.
- Finalize inventory number generation/legacy migration, category dictionaries, type-specific fields, customer matching rules, tax handling, rounding, and report definitions in schema review.
- Set nonfunctional targets (expected inventory size, concurrency, search latency, backup frequency, availability, and maximum import sizes) after measuring actual business needs.
## 18. Proposed approval and delivery sequence

1. Review and correct this requirements specification; freeze a reviewed baseline.

2. Inspect source files and existing workflows; document field mappings and exceptions.

3. Draft conceptual entity-relationship model and business invariants; review with owner.

4. Validate hosting and integration feasibility; approve architecture and security plan.

5. Produce logical schema, migration plan, UI flows, and acceptance criteria.

6. Only after explicit approval: implement in staged milestones, test with representative data, and rehearse restore/migration.

## Appendix A. Examples and important rules

### Mixed ownership example

A $100 hammer lot contains one Workman’s Books-owned item and two items from one outside consignor. Default equal item allocation gives an approximately one-third owned share and two-thirds consigned share. Using the owner’s illustrative $66.70 consignor allocation, a 40% commission is $26.68 and consignor proceeds are $40.02; final cents must be reconciled deterministically to the actual $100 hammer total. The owned share is not charged a consignor commission.

### Auction preview rule

Before finalization: preview descriptions and photos may be visible, but not nonexistent lot numbers, starting bids, estimates, or bidding links. After finalization/upload confirmation: publish those fields as appropriate.

### Design guardrail

This is a requirements baseline for review, not a finished design. Any contradictions or unverified assumptions discovered during source-file inspection must be brought back for explicit resolution rather than silently implemented.
