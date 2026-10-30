# Workman's Books — Logical Schema Coverage Audit

**Version:** 1.0 — Baseline (not yet reviewed)  
**Created:** 2026-10-30  
**Status:** Audit initialized; **0 findings structurally validated**  
**Decision baseline:** Application-wide Findings **1–300** approved; Customer Questions **Q1–127** approved  
**Working inventory:** **144 logical tables** (not SQL tables)  
**Scope:** Requirements-to-schema coverage, structural gaps, and readiness for ERD and physical design  
**Authority:** No new schema, SQL, migrations, or implementation authorized by this document.

## 1. Purpose and boundaries

This document tests whether the existing working logical inventory can **actually represent** each approved business requirement. It does **not** supersede the Master Decision Log or Software Requirements Specification. Approval of an Option A reuse proposal is **not proof** that the existing schema supports the required independent business records.

**Source-of-truth precedence:** owner-approved decision text → SRS approved requirements → checkpoint summaries → audit candidate mappings. Resolve conflicts with an explicit owner decision; do not silently edit prior approvals.

**Evidence needed for a 'Validated' result:** table(s), field(s), PK/FK relationship(s), lifecycle/state representation, history/audit strategy, permissions, deletion/retention rules, and at least one representative workflow test case. Mark 'Covered' only when a concrete logical design demonstrates coverage; mark 'Validated' after review and acceptance.

## 2. Audit statuses

- **Not Reviewed:** No structural evaluation has occurred.
- **Covered:** A proposed logical design demonstrably supports the requirement; pending owner validation.
- **Gap Identified:** A required independent record, relation, constraint, state, or history is missing or ambiguous.
- **Resolution Proposed:** A documented change awaits explicit owner approval.
- **Validated:** Evidence and resolution (if needed) have been reviewed and accepted.

**Priorities:** Critical (integrity/security/financial loss); High (core workflow/data preservation); Medium (operational correctness); Low (nonessential enhancement).

**Gate:** The audit cannot be closed with unresolved Critical/High gaps or unverified requirements that are required for initial implementation. Deferred requirements must be explicitly approved and recorded with scope and rationale.

## 3. Approved logical table inventory (144)

### Customer and application (44)

`customers`, `customer_roles`, `customer_role_assignments`, `customer_name_history`, `customer_emails`, `customer_phones`, `customer_addresses`, `customer_address_purposes`, `customer_contacts`, `customer_phone_sms_consent_history`, `customer_relationships`, `customer_relationship_types`, `customer_notes`, `customer_note_categories`, `customer_note_revisions`, `customer_activity_revisions`, `customer_activity_types`, `customer_activity_log`, `customer_communication_preference_history`, `customer_communication_preferences`, `customer_interest_categories`, `customer_interests`, `customer_document_categories`, `customer_documents`, `customer_document_versions`, `customer_payment_terms`, `customer_tax_exemptions`, `customer_account_holds`, `customer_account_restriction_types`, `customer_account_restrictions`, `customer_financial_profiles`, `application_audit_log`, `customer_wants`, `customer_want_matches`, `customer_auction_eligibility_history`, `application_messages`, `customer_import_batches`, `customer_import_records`, `application_users`, `application_roles`, `application_user_roles`, `application_permissions`, `application_role_permissions`, `application_user_preferences`

### Inventory and promotional (37)

`inventory_items`, `inventory_acquisitions`, `inventory_ownership_history`, `inventory_box_history`, `books`, `catalogs`, `magazines`, `magazine_articles`, `inventory_images`, `inventory_item_types`, `subjects`, `inventory_item_subjects`, `contributors`, `book_contributors`, `publishers`, `publication_publishers`, `publisher_relationships`, `inventory_number_sequences`, `periodical_titles`, `inventory_price_history`, `promotions`, `promotion_items`, `acquisition_payments`, `acquisition_documents`, `website_sync_events`, `inventory_required_field_rules`, `book_isbns`, `periodical_title_relationships`, `inventory_saved_searches`, `inventory_export_templates`, `inventory_import_batches`, `inventory_import_rows`, `inventory_validation_exceptions`, `inventory_import_issues`, `inventory_duplicate_links`, `inventory_consignor_minimum_history`, `inventory_commission_agreement_assignments`

### Auction (13)

`auction_inventory_assignments`, `auctions`, `auction_sessions`, `auction_lots`, `auction_lot_items`, `auction_import_batches`, `auction_import_rows`, `auction_import_issues`, `auction_lot_changes`, `auction_catalog_versions`, `auction_launch_checklist_items`, `auction_lot_images`, `auction_lot_field_overrides`

### Invoicing and payment (12)

`buyer_invoices`, `buyer_invoice_items`, `invoice_payments`, `invoice_payment_requests`, `payment_methods`, `customer_credit_ledger`, `credit_refunds`, `invoice_refunds`, `email_templates`, `outbound_email_messages`, `invoice_reminders`, `invoice_late_charges`

### Consignor settlement and commission (10)

`consignor_settlements`, `consignor_settlement_lines`, `consignor_payouts`, `consignor_payout_allocations`, `consignor_invoice_offsets`, `customer_account_adjustments`, `consignor_commission_agreements`, `consignor_commission_tiers`, `consignor_adjustment_recoveries`, `consignor_repayments`

### Inventory pulling (2)

`inventory_pull_sessions`, `inventory_pull_session_invoices`

### Auction shipping (2)

`shipping_packages`, `shipping_package_lots`

### Fulfillment exceptions (1)

`fulfillment_exceptions`

### Online sales (9)

`online_sales`, `online_sale_items`, `online_sale_platform_fees`, `online_sale_fee_allocations`, `online_sale_fee_adjustments`, `online_sale_refunds`, `online_sale_payments`, `online_shipping_packages`, `online_shipping_package_items`

### Business accounting and settings (14)

`business_expenses`, `expense_categories`, `expense_attachments`, `payment_accounts`, `business_vehicles`, `business_trips`, `business_trip_stops`, `sales_tax_filings`, `florida_sales_tax_rates`, `bookkeeping_reminders`, `accounting_years`, `application_settings`, `financial_report_versions`, `financial_report_files`

## 4. Requirements coverage matrix — initial register

**Important:** The approval record is not the same as structural validation. All rows below begin as **Not Reviewed**. Summaries appear only when recoverable from the checkpoint SRS; otherwise the source decision must be consulted. Table mappings are deliberately blank until evidence is examined. This prevents an untested guess from being treated as a verified relationship.

| Finding | Decision | Requirement summary / source | Candidate tables | Status | Gap ID | Evidence |
|---|---|---|---|---|---|---|
| 001 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 002 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 003 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 004 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 005 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 006 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 007 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 008 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 009 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 010 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 011 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 012 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 013 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 014 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 015 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 016 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 017 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 018 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 019 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 020 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 021 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 022 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 023 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 024 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 025 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 026 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 027 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 028 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 029 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 030 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 031 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 032 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 033 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 034 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 035 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 036 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 037 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 038 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 039 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 040 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 041 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 042 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 043 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 044 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 045 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 046 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 047 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 048 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 049 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 050 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 051 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 052 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 053 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 054 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 055 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 056 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 057 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 058 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 059 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 060 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 061 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 062 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 063 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 064 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 065 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 066 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 067 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 068 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 069 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 070 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 071 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 072 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 073 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 074 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 075 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 076 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 077 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 078 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 079 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 080 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 081 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 082 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 083 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 084 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 085 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 086 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 087 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 088 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 089 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 090 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 091 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 092 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 093 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 094 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 095 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 096 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 097 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 098 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 099 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 100 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 101 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 102 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 103 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 104 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 105 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 106 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 107 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 108 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 109 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 110 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 111 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 112 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 113 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 114 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 115 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 116 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 117 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 118 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 119 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 120 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 121 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 122 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 123 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 124 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 125 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 126 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 127 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 128 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 129 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 130 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 131 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 132 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 133 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 134 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 135 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 136 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 137 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 138 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 139 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 140 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 141 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 142 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 143 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 144 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 145 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 146 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 147 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 148 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 149 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 150 | Approved (see source) | Consult approved decision log / historical checkpoint; detailed source mapping pending | — | Not Reviewed | — | — |
| 151 | Approved (see source) | Vendor refunds and credits; preserve original expense, source, cash refunds vs future-use credits and reconciliation. | — | Not Reviewed | — | — |
| 152 | Approved (see source) | Vendor prepayments and deposits; distinguish advance assets/credits from recognized expense, reconcile applications and refunds. | — | Not Reviewed | — | — |
| 153 | Approved (see source) | Business fixed assets and disposals using existing records; acquisition, depreciation/accountant review, sale/disposal and audit. | — | Not Reviewed | — | — |
| 154 | Approved (see source) | Expense reclassification with authorized corrections and original transaction preservation. | — | Not Reviewed | — | — |
| 155 | Approved (see source) | Unpaid vendor bills tracked separately from paid expenses; cash-basis recognition remains accountant-reviewed. | — | Not Reviewed | — | — |
| 156 | Approved (see source) | Recurring expenses and expected obligations via existing records; reminders, prevent duplicate actual charges. | — | Not Reviewed | — | — |
| 157 | Approved (see source) | Vendors represented through customer roles and existing customer records; role separation and audit. | — | Not Reviewed | — | — |
| 158 | Approved (see source) | Manual vendor statement reconciliation, missing/duplicate charges and resolution history. | — | Not Reviewed | — | — |
| 159 | Approved (see source) | Duplicate vendor invoice detection and authorized exception resolution. | — | Not Reviewed | — | — |
| 160 | Approved (see source) | Expense approval workflow, permission separation and documented authorization. | — | Not Reviewed | — | — |
| 161 | Approved (see source) | Budgets using existing expense/settings/reporting records; compare planned versus actual without accounting entries. | — | Not Reviewed | — | — |
| 162 | Approved (see source) | Receipt and supporting-document requirements based on expense category, exceptions and audit. | — | Not Reviewed | — | — |
| 163 | Approved (see source) | Dropbox-managed expense attachments with version history and initial integrity verification. | — | Not Reviewed | — | — |
| 164 | Approved (see source) | Expense-document retention indefinitely by default, controlled disposal and legal/audit holds. | — | Not Reviewed | — | — |
| 165 | Approved (see source) | Accountant expense-document ZIP exports with controlled access, completeness and audit. | — | Not Reviewed | — | — |
| 166 | Approved (see source) | Accountant-recommended adjustments linked to original transaction; noncash vs cash, closed-year protection, reversals. | — | Not Reviewed | — | — |
| 167 | Approved (see source) | Vehicle mileage and expenses; historical rates, business/personal use, reimbursement vs deduction, no double count. | — | Not Reviewed | — | — |
| 168 | Approved (see source) | Mixed-purpose trips with business/personal segment mileage and documented shared-cost allocations. | — | Not Reviewed | — | — |
| 169 | Approved (see source) | Travel expenses and reimbursements; payer, partial reimbursements, substantiation and separate tax treatment. | — | Not Reviewed | — | — |
| 170 | Approved (see source) | Travel advances, documented substantiation, repayments and unresolved balances. | — | Not Reviewed | — | — |
| 171 | Approved (see source) | Canceled or partly completed travel; cancellation fees, deposits, credits, refunds and advance reconciliation. | — | Not Reviewed | — | — |
| 172 | Approved (see source) | Optional travel per diem; historical rates, eligibility, approvals and duplicate-claim prevention. | — | Not Reviewed | — | — |
| 173 | Approved (see source) | Meals and entertainment classification; attendees/purpose, receipts, deduction fraction vs actual cost. | — | Not Reviewed | — | — |
| 174 | Approved (see source) | Inventory gifts, promotional giveaways and other non-sale dispositions; ownership, cost and approval. | — | Not Reviewed | — | — |
| 175 | Approved (see source) | Damaged/lost/stolen/destroyed inventory; repair/write-off, consignor rights, insurance and audit. | — | Not Reviewed | — | — |
| 176 | Approved (see source) | Inventory restoration/conservation; service expenses, before/after condition and owner authorization. | — | Not Reviewed | — | — |
| 177 | Approved (see source) | Condition and grading history; source/assessor, revisions, publication snapshots and audit. | — | Not Reviewed | — | — |
| 178 | Approved (see source) | Authenticity, provenance and attribution; claims vs verified evidence, conflicts and inventory-linked documents. | — | Not Reviewed | — | — |
| 179 | Approved (see source) | Inventory research notes and bibliographic evidence; identifiable notes/sources and historical versions. | — | Not Reviewed | — | — |
| 180 | Approved (see source) | Cataloging review and publication approval; approvals tied to content version and repeat review cycles. | — | Not Reviewed | — | — |
| 181 | Approved (see source) | Temporary inventory reservations; history, expiration, conflict prevention and release. | — | Not Reviewed | — | — |
| 182 | Approved (see source) | Consignor returns and withdrawals; requests, approvals, custody handover and historical evidence. | — | Not Reviewed | — | — |
| 183 | Approved (see source) | Inventory storage transfers, temporary movements and location history including non-box locations. | — | Not Reviewed | — | — |
| 184 | Approved (see source) | Physical inventory counts; sessions, expected snapshots, observed results, discrepancies and approvals. | — | Not Reviewed | — | — |
| 185 | Approved (see source) | Temporary external inventory custody; custodian, permissions, handover, due date and inspection. | — | Not Reviewed | — | — |
| 186 | Approved (see source) | Inventory image versions and independent channel selections; immutable published image sets. | — | Not Reviewed | — | — |
| 187 | Approved (see source) | Multi-volume sets and components; structured component quantities, completeness and fulfillment. | — | Not Reviewed | — | — |
| 188 | Approved (see source) | Inventory splits/combinations; source-result lineage, cost allocation, ownership and sale prevention. | — | Not Reviewed | — | — |
| 189 | Approved (see source) | Channel-specific asking prices; effective periods, pricing history and realized-price separation. | — | Not Reviewed | — | — |
| 190 | Approved (see source) | Market/insurance valuations; source, methodology, date, evidence and nonaccounting treatment. | — | Not Reviewed | — | — |
| 191 | Approved (see source) | Inventory insurance claims; affected items, claims, partial recoveries and consignor allocations. | — | Not Reviewed | — | — |
| 192 | Approved (see source) | Inventory purchase offers/counteroffers; negotiation history, offer status and resulting sale linkage. | — | Not Reviewed | — | — |
| 193 | Approved (see source) | Layaway/installment sales; agreements, installment schedules, payments, inventory commitment, fulfillment restrictions and refunds. | — | Not Reviewed | — | — |
| 194 | Approved (see source) | Fixed-price returns/exchanges; authorization, physical receipt, inspection, refunds, restocking and consignor rights. | — | Not Reviewed | — | — |
| 195 | Approved (see source) | Payment disputes/chargebacks; processor references, evidence, deadlines, fees, reversals and partial recoveries. | — | Not Reviewed | — | — |
| 196 | Approved (see source) | Customer credit types, issue sources, partial redemption, refundability, restrictions and lawful expiration. | — | Not Reviewed | — | — |
| 197 | Approved (see source) | Customer account statements; authoritative transactions, opening/closing balances, available credits separately and reconciliation. | — | Not Reviewed | — | — |
| 198 | Approved (see source) | Sales tax refund adjustments; original item/jurisdiction/rate, partial refunds, filing-period review and no excess refund. | — | Not Reviewed | — | — |
| 199 | Approved (see source) | Returned-to-sender shipments; carrier status vs physical custody, inspection, linked reshipments and disposition. | — | Not Reviewed | — | — |
| 200 | Approved (see source) | Lost/damaged/misdelivered carrier claims; shipment/item links, evidence, customer remedies, partial recoveries and consignor protections. | — | Not Reviewed | — | — |
| 201 | Approved (see source) | Carrier shipping label voids, replacements and refunds; retain original label, refund status, replacement link and audit. | — | Not Reviewed | — | — |
| 202 | Approved (see source) | Combined shipping across buyer invoices and auctions; allocate charges and package contents without duplicating fulfillment or revenue. | — | Not Reviewed | — | — |
| 203 | Approved (see source) | Local pickup and delivery; appointments, custody handover, proof of release, partial pickup and audit. | — | Not Reviewed | — | — |
| 204 | Approved (see source) | Customer shipping preferences; default versus transaction-specific instructions, consent and history. | — | Not Reviewed | — | — |
| 205 | Approved (see source) | Shipping address verification and corrections; preserve original invoice address and verified shipment destination. | — | Not Reviewed | — | — |
| 206 | Approved (see source) | Packed weights, dimensions and carrier adjustments; preserve measured figures, label quotes, adjustments and reconciliation. | — | Not Reviewed | — | — |
| 207 | Approved (see source) | Shipping supplies inventory; purchases, stock movements, package consumption and expense classification. | — | Not Reviewed | — | — |
| 208 | Approved (see source) | Shipment tracking and delivery evidence; carrier events, delivery confirmation, exceptions and customer notifications. | — | Not Reviewed | — | — |
| 209 | Approved (see source) | International customs documentation; declared values, contents, approvals, export restrictions and immutable shipment evidence. | — | Not Reviewed | — | — |
| 210 | Approved (see source) | Shipping insurance coverage; declared value, carrier/policy coverage, premiums, claims and limits. | — | Not Reviewed | — | — |
| 211 | Approved (see source) | Shipment holds and release; reasons, authorizations, partial holds, release prerequisites and history. | — | Not Reviewed | — | — |
| 212 | Approved (see source) | Carrier pickup/drop-off manifests; grouped packages, tender evidence, scan discrepancies and reconciliation. | — | Not Reviewed | — | — |
| 213 | Approved (see source) | Shipping quotes and approvals; estimates versus final charges, customer approval and expiry. | — | Not Reviewed | — | — |
| 214 | Approved (see source) | Split shipments and outstanding items; invoice-item/package allocation, partial dispatch, backorders and final fulfillment. | — | Not Reviewed | — | — |
| 215 | Approved (see source) | Customer shipping charges versus actual carrier/handling expense; reconcile variances without rewriting issued invoices. | — | Not Reviewed | — | — |
| 216 | Approved (see source) | Pre-fulfillment cancellations; preserve sale, payment, inventory, refund and consignor effects with approval. | — | Not Reviewed | — | — |
| 217 | Approved (see source) | Buyer nonpayment and default; notices, deadlines, authorized cancellations, inventory/consignor effects and audit. | — | Not Reviewed | — | — |
| 218 | Approved (see source) | Post-sale auction catalog corrections; preserve published versions, corrected text and buyer/consignor notification. | — | Not Reviewed | — | — |
| 219 | Approved (see source) | Published auction lot withdrawals; approvals, reasons, external update flags, inventory and financial safeguards. | — | Not Reviewed | — | — |
| 220 | Approved (see source) | Reoffering unsold, withdrawn or defaulted inventory; retain prior sale/lot history and availability checks. | — | Not Reviewed | — | — |
| 221 | Approved (see source) | Draft auction lot consolidation and division; preserve item allocations, identifiers and numbering protections. | — | Not Reviewed | — | — |
| 222 | Approved (see source) | Auction reserve versus consignor minimum; independent contractual minimum and lot reserve, with reviewed conflicts. | — | Not Reviewed | — | — |
| 223 | Approved (see source) | Unsold auction lot post-auction dispositions; manual ownership/location/retail-release decisions and audit. | — | Not Reviewed | — | — |
| 224 | Approved (see source) | External auction results import and reconciliation; stage source results, match lots, resolve conflicts and preserve provenance. | — | Not Reviewed | — | — |
| 225 | Approved (see source) | External bidder identity matching; verify ambiguous identities and preserve external identifiers without auto-merge. | — | Not Reviewed | — | — |
| 226 | Approved (see source) | Auction bidder disputes and sale-result challenges; case evidence, holds, resolution and immutable original result. | — | Not Reviewed | — | — |
| 227 | Approved (see source) | Buyer premiums and fees; versioned auction policies, line-item calculations, exceptions and audit. | — | Not Reviewed | — | — |
| 228 | Approved (see source) | Auction-specific bidder registration and approval; eligibility, conditions, verification, restrictions and history. | — | Not Reviewed | — | — |
| 229 | Approved (see source) | Bidder deposits and guarantees; receipt, application, refund, forfeiture, outstanding liability and reconciliation. | — | Not Reviewed | — | — |
| 230 | Approved (see source) | Buyer payment deadlines and extensions; policy, authorized exceptions, notices and history. | — | Not Reviewed | — | — |
| 231 | Approved (see source) | Buyer overpayments and unapplied funds; separate customer liabilities, applications, refunds and no double counting. | — | Not Reviewed | — | — |
| 232 | Approved (see source) | Payment processor fees and net bank deposits; gross receipts, fees, settlement timing and bank reconciliation. | — | Not Reviewed | — | — |
| 233 | Approved (see source) | Buyer invoice consolidation and separation across auction sessions; preserve source sales, line allocations and audit. | — | Not Reviewed | — | — |
| 234 | Approved (see source) | Auction buyer invoice delivery and acknowledgment; per-attempt recipient/channel/version, failures, confirmation versus acceptance. | — | Not Reviewed | — | — |
| 235 | Approved (see source) | Buyer invoice corrections and replacement documents; immutable original, supersession, payment/tax/consignor consequences. | — | Not Reviewed | — | — |
| 236 | Approved (see source) | Buyer invoice write-offs and uncollectible balances; authorization, partial write-offs, later recovery and accountant treatment. | — | Not Reviewed | — | — |
| 237 | Approved (see source) | Consignor settlement disputes and corrections; independent disputes, holds, evidence, supplemental payments and recoveries. | — | Not Reviewed | — | — |
| 238 | Approved (see source) | Consignor payout failures, voids and replacements; original and linked attempts, verified outcomes, no duplicate payment. | — | Not Reviewed | — | — |
| 239 | Approved (see source) | Consignor payout preferences and instructions; verified destinations, sensitive-data controls, changes and one-time overrides. | — | Not Reviewed | — | — |
| 240 | Approved (see source) | Consignor settlement statement delivery and acknowledgment; exact version, attempts, receipt versus acceptance and audit. | — | Not Reviewed | — | — |
| 241 | Approved (see source) | Consignor payout scheduling and partial disbursements; eligible/scheduled/issued/paid distinctions, holds and rescheduling. | — | Not Reviewed | — | — |
| 242 | Approved (see source) | Consignor advances against future auction proceeds; independent advances, disbursement, multi-auction recovery and balances. | — | Not Reviewed | — | — |
| 243 | Approved (see source) | Consignor reimbursable expenses; actual expense versus charge, shared allocations, partial waiver and no double allocation. | — | Not Reviewed | — | — |
| 244 | Approved (see source) | Multi-auction consignor balance reconciliation; independent settlements, cross-auction allocations, recoveries and historical balances. | — | Not Reviewed | — | — |
| 245 | Approved (see source) | Consignor settlement periods and closing controls; review checks, individual closing, exceptions, immutable finalized amounts, controlled reopening and accounting peri... | — | Not Reviewed | — | — |
| 246 | Approved (see source) | Consignor settlement reports and historical reconciliation snapshots; as-of balances, parameters, immutable report versions, restatements and access controls. | — | Not Reviewed | — | — |
| 247 | Approved (see source) | Consignor death/incapacity and legal representative authority; verified scope, holds, competing claims, ownership continuity and authorized release. | — | Not Reviewed | — | — |
| 248 | Approved (see source) | Consignment agreement renewals, amendments and termination; versioned effective terms, item/sale applicability, surviving obligations and signed evidence. | — | Not Reviewed | — | — |
| 249 | Approved (see source) | Unclaimed consignor-owned inventory after termination; notices, custody, partial returns, disputes, lawful disposition and retained ownership. | — | Not Reviewed | — | — |
| 250 | Approved (see source) | Consignor inventory condition changes during custody; intake evidence, independent observations, photos, investigation, consignor notice and catalog corrections. | — | Not Reviewed | — | — |
| 251 | Approved (see source) | Consignor temporary loans and custody. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subj... | — | Not Reviewed | — | — |
| 252 | Approved (see source) | Consignor trades and exchanges. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to ... | — | Not Reviewed | — | — |
| 253 | Approved (see source) | Consignor purchase offers and counteroffers. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit... | — | Not Reviewed | — | — |
| 254 | Approved (see source) | Consignor buyouts. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to structural va... | — | Not Reviewed | — | — |
| 255 | Approved (see source) | Consignor ownership transfers. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to s... | — | Not Reviewed | — | — |
| 256 | Approved (see source) | Consignor returns and releases. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to ... | — | Not Reviewed | — | — |
| 257 | Approved (see source) | Consignor storage charges. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to struc... | — | Not Reviewed | — | — |
| 258 | Approved (see source) | Consignor retrieval appointments. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject t... | — | Not Reviewed | — | — |
| 259 | Approved (see source) | Consignor inventory inspections. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to... | — | Not Reviewed | — | — |
| 260 | Approved (see source) | Catalog reproduction rights and permissions. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit... | — | Not Reviewed | — | — |
| 261 | Approved (see source) | Catalog authenticity and attribution. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subje... | — | Not Reviewed | — | — |
| 262 | Approved (see source) | Catalog bibliographic research sources. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, sub... | — | Not Reviewed | — | — |
| 263 | Approved (see source) | Catalog editorial tasks and review. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject... | — | Not Reviewed | — | — |
| 264 | Approved (see source) | Catalog proofs and final signoff. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject t... | — | Not Reviewed | — | — |
| 265 | Approved (see source) | Catalog distribution campaigns. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to ... | — | Not Reviewed | — | — |
| 266 | Approved (see source) | Catalog printing orders. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to structu... | — | Not Reviewed | — | — |
| 267 | Approved (see source) | Printed catalog stock. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to structura... | — | Not Reviewed | — | — |
| 268 | Approved (see source) | Catalog errata and corrections. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to ... | — | Not Reviewed | — | — |
| 269 | Approved (see source) | Catalog archives and public access. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject... | — | Not Reviewed | — | — |
| 270 | Approved (see source) | Historical auction lot research. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to... | — | Not Reviewed | — | — |
| 271 | Approved (see source) | Catalog indexes and cross-references. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subje... | — | Not Reviewed | — | — |
| 272 | Approved (see source) | Catalog templates and front matter. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject... | — | Not Reviewed | — | — |
| 273 | Approved (see source) | Catalog generation runs and reproducibility. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit... | — | Not Reviewed | — | — |
| 274 | Approved (see source) | Catalog image selection, crops and layout. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, ... | — | Not Reviewed | — | — |
| 275 | Approved (see source) | Accessible catalog formats. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to stru... | — | Not Reviewed | — | — |
| 276 | Approved (see source) | Multilingual catalog translations. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject ... | — | Not Reviewed | — | — |
| 277 | Approved (see source) | Complimentary catalog copies. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to st... | — | Not Reviewed | — | — |
| 278 | Approved (see source) | Paid catalog sales. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to structural v... | — | Not Reviewed | — | — |
| 279 | Approved (see source) | Digital catalog downloads and entitlements. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit,... | — | Not Reviewed | — | — |
| 280 | Approved (see source) | Customer catalog requests and special orders. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audi... | — | Not Reviewed | — | — |
| 281 | Approved (see source) | Catalog reprints and print-on-demand. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subje... | — | Not Reviewed | — | — |
| 282 | Approved (see source) | Archival copies and institutional donations. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit... | — | Not Reviewed | — | — |
| 283 | Approved (see source) | Catalog physical condition, damage, repair and disposal. Reuse approved existing records; preserve independent operational states, source links, authorization and hist... | — | Not Reviewed | — | — |
| 284 | Approved (see source) | Catalog physical stock counts. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to s... | — | Not Reviewed | — | — |
| 285 | Approved (see source) | Catalog subscriptions and standing orders. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, ... | — | Not Reviewed | — | — |
| 286 | Approved (see source) | Reciprocal catalog exchanges and institutional agreements. Reuse approved existing records; preserve independent operational states, source links, authorization and hi... | — | Not Reviewed | — | — |
| 287 | Approved (see source) | Institutional catalog loans. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to str... | — | Not Reviewed | — | — |
| 288 | Approved (see source) | Customer catalog reservations and waitlists. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit... | — | Not Reviewed | — | — |
| 289 | Approved (see source) | Complimentary replacement catalogs. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject... | — | Not Reviewed | — | — |
| 290 | Approved (see source) | Catalog publication schedules. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit, subject to s... | — | Not Reviewed | — | — |
| 291 | Approved (see source) | Catalog correction recipient notifications. Reuse approved existing records; preserve independent operational states, source links, authorization and historical audit,... | — | Not Reviewed | — | — |
| 292 | Approved (see source) | External bibliographic listings and submissions. Reuse approved existing records; preserve independent operational states, source links, authorization and historical a... | — | Not Reviewed | — | — |
| 293 | Approved (see source) | External scholarly citations and research usage. Reuse approved existing records; preserve independent operational states, source links, authorization and historical a... | — | Not Reviewed | — | — |
| 294 | Approved (see source) | Catalog research inquiries and reference assistance. Independent inquiries; requester identity; exact edition/lot links; assignment, deadlines, evidence, partial answe... | — | Not Reviewed | — | — |
| 295 | Approved (see source) | Research reproduction requests and permission fulfillment. Independent reproduction requests and deliveries; rights and use limits; source assets, transformed derivati... | — | Not Reviewed | — | — |
| 296 | Approved (see source) | Catalog digital preservation and integrity monitoring. Authoritative archival files; independent checks, SHA-256 expectations, exceptions, recoveries and migrations; c... | — | Not Reviewed | — | — |
| 297 | Approved (see source) | Preservation format migrations and long-term readability. Original source retention; independent conversion attempts and derivatives; software/configuration, validatio... | — | Not Reviewed | — | — |
| 298 | Approved (see source) | Archival package completeness and validation. Independent archival packages and assessments; required versus optional components, file/dependency validation, exception... | — | Not Reviewed | — | — |
| 299 | Approved (see source) | Archival access requests and controlled retrieval. Independent file-specific access requests, approvals and retrieval events; exact versions, limits, expiry, revocatio... | — | Not Reviewed | — | — |
| 300 | Approved (see source) | Archival retention, legal holds and authorized disposition. Independent retention decisions, policy versions, legal holds, amendments/releases, approved disposition, s... | — | Not Reviewed | — | — |

### Customer decisions Q1–127

All Q1–127 remain approved in the Master Decision Log. Audit them as a **separate numbering system**, with an independent Q-prefixed coverage register during the customer domain review. Do not confuse customer Q128 (not approved) with application Finding 128 (approved Option B). Initial customer review must include identifiers, active-only uniqueness, name history, contacts, consent, tax exemptions, Dropbox document versioning, immutable invoice use, and audit history.

## 5. Structural gaps register

No gap has yet been **confirmed by the audit**. The following are **validation questions / risk candidates**, not approved schema changes.

| ID | Priority | Validation question | Status | Proposed resolution | Owner decision |
|---|---|---|---|---|---|
| RISK-001 | Critical | Can existing general-purpose records model independent archival access requests, authorization scopes, retrieval attempts and outcomes (Finding 299)? | Not Reviewed | Pending evidence | Pending |
| RISK-002 | Critical | Can existing records represent independently enforceable legal holds, releases and deletion approval/outcome chains (Finding 300)? | Not Reviewed | Pending evidence | Pending |
| RISK-003 | High | Can catalog archival packages, checksum checks, migration projects and derivative lineage be represented independently (Findings 296–298)? | Not Reviewed | Pending evidence | Pending |
| RISK-004 | Critical | Are financial corrections, allocations, refunds, credits and historical reports independently traceable without double counting? | Not Reviewed | Pending evidence | Pending |
| RISK-005 | High | Can consignor custody, ownership transfer, loans, offers, inspections, returns and approvals be reconstructed across auctions (Findings 251–259)? | Not Reviewed | Pending evidence | Pending |
| RISK-006 | High | Are customer active-only uniqueness, identity histories, certificate usage, consent histories and document version links structurally enforceable? | Not Reviewed | Pending evidence | Pending |
| RISK-007 | High | Are Dropbox references, version integrity, access permissions, recovery and provider failures consistently represented? | Not Reviewed | Pending evidence | Pending |
| RISK-008 | Medium | Do checkpoint summaries contain stale cross-references (e.g. 250 vs 300 or resume at 251 vs 301)? Reconcile editorial text without changing decisions. | Not Reviewed | Documentation-only review | Pending |

## 6. Resolution and approval log

| Date | Finding / Q | Gap ID | Decision / rationale | Approved by | Affected tables | Verification |
|---|---|---|---|---|---|---|
| — | — | — | No audit resolutions approved yet | — | — | — |

**Process:** Record the specific requirement → reproduce a representative scenario → show exact table/field/relationship evidence → identify gap → propose smallest valid resolution → request explicit approval → update inventory and ERDs only after approval → retest and record outcome. A generic note, message or audit event is not an acceptable substitute for an independently queryable business entity unless the design explicitly proves the required semantics.

## 7. Readiness checklist

- [ ] Every Finding 1–300 has source text, mapped evidence, and final status.
- [ ] Customer Q1–127 have separately mapped evidence and final status.
- [ ] All 144 logical tables reviewed for purpose, ownership and relationships.
- [ ] Independent business entities and lifecycle states demonstrably represented.
- [ ] Historical snapshots, effective dates, version lineage and audit trails defined.
- [ ] Customer identifiers, active-only uniqueness and tax exemption rules reconciled.
- [ ] Financial integrity, corrections, reversals and reporting reconciled.
- [ ] File storage, retention, holds, access and integrity safeguards reconciled.
- [ ] Role-based permissions and sensitive-data boundaries reviewed.
- [ ] Critical/High gaps resolved or explicitly deferred with owner approval.
- [ ] Domain ERDs and complete table data dictionary reviewed.
- [ ] Physical constraints, indexes and migration strategy reviewed.
- [ ] Hosting, authentication, backups and external integrations validated.
- [ ] Owner signs off logical schema and separate technical architecture.
- [ ] Explicit authorization given before SQL or application code begins.

## 8. Initial audit sequence

1. Customer/application foundation: identities, roles, permission model, consent, documents and tax exemptions.
2. Inventory and catalog metadata: ownership, provenance, images, categories and validation.
3. Auction and consignments: assignment, lots, custody, agreements and settlements.
4. Buyer invoicing, online sales, shipping, refunds and credit ledger.
5. Accounting, tax and immutable financial reporting.
6. Catalog publication, archival preservation, access, legal holds and disposition.
7. Cross-domain scenarios, concurrency, failure/recovery, final coverage and sign-off.

**Next working item:** Audit **customer identity and role assignments** against `customers`, `customer_roles`, `customer_role_assignments`, `customer_name_history`, and the approved Q-series decisions. No decision or table change is implied by beginning this review.
