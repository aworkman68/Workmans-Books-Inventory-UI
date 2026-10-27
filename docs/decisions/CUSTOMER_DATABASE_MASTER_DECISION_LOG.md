# Workman’s Books — Customer Database Master Decision Log

**Status:** Customer Questions 1–127 owner-confirmed · 20 October 2026; separate application logical reconciliation Findings 1–200 approved · 27 October 2026; physical schema not approved  
**Scope:** Customer Questions 1–127 plus cross-reference to application logical reconciliation Findings 1–200. No physical database schema or implementation approved by this document.

> Source: owner-provided “Workman's Books DB Schema Questions 1 through 96.docx” for Questions 1–96. Questions 97–127 are reconstructed from decisions recorded in the follow-on conversation. The original Word file remains the detailed source for Questions 1–96.

## Review notes

- **Q1** is an unnumbered initial question in the source: one customer record supports multiple roles; approved.
- **Q96** has no owner answer in the uploaded Word source; the owner explicitly approved Option A in the subsequent review: prevent duplicate active relationships in either direction while allowing different relationship types between the same customers.
- Customer-code rules were refined across Q23–Q27; the **latest approved rule supersedes earlier interim examples**.
- Table definitions and ERDs remain design deliverables; transcript references to “approved tables” do not mean physical tables exist.
- Source Word tables and non-text UI previews are not exhaustively reproduced here.

## Questions 1–96 — Source-based decision register

### Question 1 — Multiple customer roles

**Status:** Approved. One customer record may be Buyer, Consignor, Inventory Source, or combinations; independent role associations.

### Q002 — Multiple Addresses

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Our proposed customer_addresses table will support: Multiple addresses associated with one customer. Separate default billing and shipping addresses. Address labels such as Home, Business, or Other. The ability to select a different shipping address for an individual invoice without changing the customer's default. Preservation of the billing and shipping addresses used on historical invoices, even if the customer's saved addresses change later. That last point is particularly important for maintaining accurate sales and shipping records.

### Q003 — Multiple Email Addresses

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend a separate customer_emails table with the following capabilities: Store multiple email addresses for each customer. Identify one primary email address for general correspondence. Designate a preferred invoice email address, which may be different from the primary address. Label addresses as Personal, Business, or Other. Allow you to change the recipient when sending an individual invoice without automatically changing the customer's saved preferences. Preserve the actual recipient address in the invoice email history for auditing. This is consistent with the invoice-emailing requirements we approved in SRS Version 2.0.

### Q004 — Multiple Phone Numbers

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Our proposed customer_phone_numbers table will support: Multiple phone numbers associated with a single customer. Labels such as Mobile, Home, Business, Fax, or Other. One designated primary phone number. Optional extensions for business phone numbers. International phone numbers. Adding, editing, and deactivating phone numbers without affecting the customer's transaction history. This keeps our customer contact information flexible and avoids limiting customers to a single telephone number.

### Q005 — Individual vs. Business Customers

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend the following structure: For business customers, we'll support contact names, job titles, and preferred contact designations. Each business will remain a single customer for invoicing and transaction history. For example, a bookstore could have an owner, purchasing manager, and accounting contact without requiring three separate customer accounts. We'll also ensure that a business contact can be updated without altering historical invoices or correspondence.

### Q006 — Customer Codes

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Our proposed customers table will include a unique customer_code field with these rules: The application suggests a code based on the customer's name. You can accept or modify the suggested code before saving. The system checks that the code isn't already assigned to another customer. Once saved, the code becomes permanent, protecting references in inventory numbers and historical records. Codes are never reused, even if a customer record is deactivated. For example, a customer code of SMIJO01 could be incorporated into an inventory number such as SMIJO01-26-0003.

### Q007 — Duplicate Customer Detection

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** When creating a customer, the application will check existing records for possible matches using: Customer or contact names Business or organization names Email addresses Phone numbers If potential duplicates are found, the application will display them for review before saving the new customer. You'll be able to open an existing record or proceed with creating a new one. The application will never automatically merge customer records. We'll also distinguish between exact matches and possible matches, since two different customers could legitimately share a surname, telephone number, or business address.

### Q008 — Customer Status

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Our proposed customers table will support: Active: Customer appears in normal searches and selection lists. Inactive: Customer remains in the database but is hidden from normal selection lists unless you choose to include inactive records. Reactivation: An inactive customer can be restored to Active status at any time. Historical preservation: Inventory, acquisitions, consignments, auctions, invoices, payments, and correspondence remain linked to the customer. Audit history: Status changes record who made the change, when it occurred, and the previous and new status. We'll also prevent routine deletion of customer records that have associated business transactions.

### Q009 — Customer Notes

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend two complementary approaches: The notes history will support: Automatically recorded creation date and time. The user who created each note. Searchable note content. Optional categories such as General, Collecting Interests, Shipping, Billing, and Follow-up. Editing with an audit trail so changes can be traced. Preservation of notes when a customer becomes inactive. For example, you could record that a customer collects Spanish colonial coinage, prefers USPS Priority Mail, or requested a particular auction catalog.

### Q010 — Customer Relationships

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** I recommend adding a customer_relationships table that allows us to associate customers without combining their accounts. The design will support: Relationship types: Spouse, Business Owner, Employee, Associated Organization, and Other. Multiple relationships: A customer can be associated with several other customers. Independent accounts: Each customer retains their own inventory, invoices, payments, and financial history. Relationship notes: Optional details explaining the association. History: Relationships can be ended without deleting their historical records. For example, John Smith could be associated with Smith's Rare Books as its owner while both retain separate customer records.

### Q011 — Tax-Exempt Customers

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend a separate customer_tax_exemptions table so we can maintain exemption records without overcrowding the main customer table. The design will support: Exemption type: Resale, governmental, or another applicable exemption category. Certificate number: The identifying number from the exemption documentation. Issuing jurisdiction: State or other applicable taxing authority. Effective and expiration dates: Where applicable. Supporting documents: A stored copy of the exemption certificate, linked to the customer record. Verification status: Pending, Verified, Expired, or Revoked. Historical accuracy: Invoices retain the exemption and tax calculations that applied when they were issued. The application will also flag expired or unverified exemptions for review. Tax-exempt status will only affect invoices when the exemption is valid and applicable to the transaction.

### Q012 — Customer Communication Preferences

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** I recommend adding a customer_communication_preferences table with the following capabilities: Preferred contact method: Email, telephone, postal mail, or no preference. Auction announcements: Opt in or out of upcoming auction notifications. New inventory notifications: Opt in or out of announcements about newly available books and other inventory. General promotions: Opt in or out of special offers and sales. Transactional communications: Keep invoices, payment receipts, and other necessary business correspondence separate from marketing preferences. Preference history: Record when preferences change, who updated them, and how consent was obtained. Unsubscribe handling: Honor promotional email opt-outs without disabling necessary transactional communications. We'll also design these preferences so they can be managed directly from the customer record.

### Q013 — Customer Documents

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend a customer_documents table that stores document information and references to the corresponding Dropbox files. The design will support: Multiple documents per customer: Consignment agreements, tax-exemption certificates, correspondence, purchase records, and other relevant documents. Document categories: Configurable categories to keep records organized. Document details: Filename, description, document date, upload date, and uploading user. Dropbox integration: Store secure file references in the database rather than storing the actual documents in database fields. Access controls: Restrict sensitive documents based on user permissions. Document history: Preserve an audit trail of uploads, replacements, and removals. Search and filtering: Find documents by customer, category, date, or description. We'll also avoid storing sensitive identification documents unless there's a legitimate business need.

### Q014 — Customer Account Summary

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** When you open a customer record, you'll have a central place to review that customer's business activity. The summary will include: We'll retrieve this information from the appropriate related tables rather than duplicating financial records in the customers table.

### Q015 — Customer Activity Timeline

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** The timeline will bring together important events from across the Workman's Books application, including purchases, payments, consignments, inventory acquisitions, emails, and customer notes. It will support filtering by date and activity type, with links to the original records. I recommend generating the timeline from existing transaction and activity records rather than maintaining duplicate information. That will help keep the history accurate and consistent.

### Q016 — Customer Merge Functionality

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** The merge process will include: Side-by-side comparison: Review both customer records before making changes. Primary record selection: Choose which customer record to retain. Conflict resolution: Decide which contact information, addresses, and preferences to keep. Transaction preservation: Maintain all invoices, payments, consignments, acquisitions, and inventory history. Customer code preservation: Never reuse or silently change customer codes already embedded in inventory numbers. Merge audit trail: Record the original customer IDs, retained customer ID, administrator, date, and changes made. Safety checks: Prevent a merge if unresolved conflicts could compromise historical records. The original customer record will remain traceable after merging, even though it will no longer appear as a separate active customer.

### Q017 — Customer Tags

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** I recommend using two related tables: This will allow us to: Create tags such as Spanish Colonial, Ancient Coins, Rare Books, and Treasure Hunting. Assign multiple tags to the same customer. Search and filter customers by one or more tags. Rename tags without updating every customer record. Retire tags without losing their historical associations. Prevent duplicate tag assignments. Tags will remain separate from formal customer roles and communication preferences.

### Q018 — Customer Identification Numbers

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend adding a customer_external_ids table to associate customers with identifiers assigned by other systems. The design will support multiple identifiers per customer, prevent conflicting assignments within the same external system, and preserve identifiers when customer records are merged. This should be particularly useful when importing iCollector auction results and matching bidders to existing customers.

### Q019 — Customer Contact History

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend adding a customer_contact_history table to record communications with customers, including those that occur outside the application. The design will support: Contact date and time: When the interaction occurred. Communication method: Telephone, email, in person, postal mail, or other. Subject and summary: What was discussed. Contact person: Particularly useful when communicating with a business customer. Direction: Incoming or outgoing communication. Follow-up information: Any action needed and its due date. Recorded by: The application user who entered the interaction. Related records: Optional links to invoices, auctions, consignments, or inventory. Audit history: Preserve changes to contact records. These interactions will also appear automatically in the Customer Activity Timeline we approved earlier.

### Q020 — Follow-Up Reminders

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** I recommend adding a customer_follow_ups table to manage reminders associated with customer interactions. The design will support: Customer association: Each reminder is linked to a customer. Reminder details: Subject, description, and due date. Status: Pending, Completed, Canceled, or Overdue. Priority: Optional Low, Normal, or High priority. Assigned user: The Administrator or Staff member responsible. Related records: Optional links to contact history, invoices, auctions, or consignments. Completion history: Record when a follow-up was completed and by whom. Message & Status Center: Display upcoming and overdue reminders. Reminders will remain internal unless you explicitly initiate a customer communication.

### Q021 — Customer Record Change History

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** We'll use the centralized audit_events table already planned in our SRS, rather than creating separate audit tables for each customer-related entity. The Change History view will provide: What changed: The field or information modified. Previous and new values: Where appropriate and permitted by security rules. Who made the change: The responsible Administrator or Staff member. When it changed: Date and time. Action performed: Created, Updated, Deactivated, Reactivated, or Merged. Filtering: Search by date, user, or type of change. Read-only history: Audit records cannot be edited or deleted through normal application functions. Sensitive information will be protected from unnecessary exposure in audit logs.

### Q022 — Customer Record Creation

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** The customer creation process will work as follows: When you open the New Customer form, the application suggests an available customer code. You can accept or edit that suggestion. When you click Save, the application validates the customer information and checks that the code is still unique. If validation succeeds, the customer record and its permanent code are saved together. If saving fails or you cancel, no customer code is assigned or reserved. We'll also account for simultaneous users so that two customers can never receive the same code.

### Q023 — Customer Code Format

**Status:** Approved / recorded.
**Owner answer:** I think it should be a fixed format
**Recorded outcome (excerpt):** Since we've already been using SMIJO01 as an example, I recommend retaining that seven-character format: SMIJO01 SMIJO 5 letters Derived from customer name 2 digits Unique numeric suffix The application would automatically suggest a code, allow you to edit it before saving, and enforce exactly five uppercase letters followed by two digits. Once saved, the code would remain permanent.

### Q024 — Handling Exhausted Customer Codes

**Status:** Approved / recorded.
**Owner answer:** I suppose we could use base 16 so when we get to 99 the next would be 0A... or would that work?
**Recorded outcome (excerpt):** We'll retain our original seven-character customer code format: AAAAA00 — Five uppercase letters followed by two decimal digits. For example: SMIJO01, SMIJO02, SMIJO03, through SMIJO99. The rules will be: The numeric suffix ranges from 01 to 99 (00 is not assigned). The application automatically suggests the next available code for a given five-letter prefix. You can edit the suggested code before saving. Customer codes must be unique and become permanent upon successful Save. If all 99 suffixes are used, the application will suggest a different five-letter prefix. The database validation pattern will be ^[A-Z]{5}(0[1-9]|[1-9][0-9])$.

### Q025 — Customer Code Prefixes

**Status:** Approved / recorded.
**Owner answer:** yes... first three of last unless the last name is only two characters long, then we'd use first three of first... and I like the first 5 of the company name
**Recorded outcome (excerpt):** Our customer codes will retain the fixed five-letter prefix + two-digit suffix format. We'll automatically convert letters to uppercase, ignore spaces and punctuation when generating business prefixes, and check for duplicates. As previously agreed, you can manually adjust the suggested code before saving, and it becomes permanent after the customer record is successfully saved.

### Q026 — Short Names

**Status:** Approved / recorded.
**Owner answer:** it should always be last name letters then first so John Li would be LIJOH01... in the case of Bo Li it would be LIBOX01 and yes, I like the X or, we could use an underscore... LIBO*01
**Recorded outcome (excerpt):** For individuals, we'll concatenate the last name followed by the first name, then take the first five characters. If fewer than five characters are available, we'll pad the remainder. For businesses, we'll use the first five letters of the company name. Both approaches work technically, but they have slightly different advantages. Underscore (LIBO_01) clearly indicates a padding character, but requires expanding our original letters-and-digits validation rule. X (LIBOX01) keeps every customer code strictly alphanumeric, making it simpler to type, search, and exchange with other systems. My recommendation is X, primarily because customer codes become part of inventory numbers and may appear in CSV exports and external integrations. Would you prefer to finalize the padding character as X or underscore (*)?

### Q027 — Middle Names and Initials

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Middle names and initials will be stored as part of the customer's information but will not affect their automatically generated customer code. For example: These examples show the initial suggested code for each name independently. If a code is already assigned, the application will suggest the next available numeric suffix. This completes our customer code naming rules!

### Q028 — Customer Name Changes

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Our database design will follow these rules: Permanent customer code: Once assigned, a customer's code never changes. Editable names: First names, middle names, last names, and business names can be updated. Inventory protection: Existing inventory numbers remain unchanged. Audit history: Name changes record the previous name, new name, date, and responsible user. Historical records: Existing invoices, acquisitions, consignments, and other transactions retain their historical information. Searchability: The customer can still be found using their permanent code. For example, if John Smith (SMIJO01) changes his surname to Johnson, his customer code remains SMIJO01.

### Q029 — Previous Names and Business Aliases

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** I recommend adding a customer_names table to preserve alternate and historical names associated with each customer. The design will support: Previous personal names: Former surnames, maiden names, and other previously used names. Business aliases: Former business names, trade names, and DBA names. Searchability: Searching an old name or alias will locate the current customer record. Historical dates: Optional start and end dates for when a name was used. Audit history: Record when names are added, modified, or retired. Permanent customer codes: Name changes will never alter an assigned customer code. For example, a customer currently named Smith Numismatics could still be found by searching its former name, Smith's Rare Books.

### Q030 — Customer Record Attachments and Images

**Status:** Deferred.
**Owner answer:** I don't see the need for that now... maybe a future add-on
**Recorded outcome (excerpt):** We'll leave profile images and business logos out of the initial database design and place them on our Future Enhancements list. That keeps the initial implementation focused without ruling out the feature later.

### Q031 — Customer Record Layout

**Status:** Approved / recorded.
**Owner answer:** like a left side menu? that would be good
**Recorded outcome (excerpt):** We'll use a left-side navigation menu within the Customer screen instead of horizontal tabs. Customer: John Smith Active Customer Code: SMIJO01 GeneralAddressesAccountActivityCommunicationsDocumentsAdministration General Customer information, roles, and contact details Select a menu item to preview its section. This is a simple interactive layout preview, not an implemented application screen. The menu would stay visible while you navigate between customer sections, making it easy to move around without losing your place.

### Q032 — Customer Search

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** The Customer List screen will support: One search box: Search across customer names, customer codes, business names, email addresses, phone numbers, previous names, and aliases. Advanced filters: Customer type, roles, Active/Inactive status, and tags. Combined filters: For example, find active consignors interested in Spanish colonial coinage. Sortable results: Sort by customer name, code, date added, or most recent activity. Quick access: Select a customer to open their record with the left-side navigation menu we approved. Inactive customers: Hidden by default but available through filtering. We'll also make sure searching works with partial names and codes, so you won't need to remember an exact spelling.

### Q033 — Customer List Customization

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** The Customer List will support: Show/hide columns: Choose which customer details appear. Reorder columns: Arrange them using drag-and-drop. Resize columns: Adjust widths to fit the information. Sorting: Sort by customer name, code, balance, or other available fields. Saved preferences: Remember your layout, column widths, and sorting choices between sessions. Reset to default: Restore the original layout whenever needed. Individual preferences: Each Administrator or Staff user can maintain their own layout. These preferences will be stored separately from customer business data, so changing your layout won't affect customer records.

### Q034 — Exporting Customer Lists

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** The Customer List will support: CSV exports: For compatibility with other applications and data-processing tools. Excel exports: For reviewing, sorting, and working with customer information in Microsoft Excel. Filtered exports: Export only customers matching your current search and filters. Selectable columns: Choose which fields to include. All matching records: Export the entire filtered result set, not just the currently visible page. Security: Respect Administrator and Staff permissions, excluding restricted information when necessary. Export history: Record who exported customer information and when. We'll also ensure exported files handle commas, quotation marks, and special characters correctly.

### Q035 — Importing Customer Records

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend a guided import process with the following capabilities: File formats: CSV (.csv) and Excel (.xlsx). Column mapping: Match spreadsheet columns to customer fields, including names, customer codes, addresses, emails, and phone numbers. Import preview: Review the proposed customer records before saving anything. Validation: Identify missing required fields, invalid customer codes, and improperly formatted information. Duplicate detection: Compare incoming records against existing customers using names, emails, phone numbers, and customer codes. Error reporting: Show which rows need corrections and why. Import history: Record the source filename, import date, responsible user, and results. Safety: Never overwrite existing customer information without explicit approval. We'll also make sure the import process respects our approved customer code rules, including the permanent seven-character format.

### Q036 — Handling Duplicate Records During Import

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** The customer import process will support: We'll also include these safeguards: Potential duplicates are flagged for review. Existing customer information is never silently overwritten. Permanent customer codes cannot be changed through an import. Financial and transaction histories remain untouched. Import results and approved changes are recorded in the audit history. If some rows fail validation, the application identifies them without losing the successfully processed records.

### Q037 — Import Templates

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** The customer import feature will provide: CSV and Excel templates with the correct column headings. Individual customer examples showing first name, last name, customer code, and contact details. Business customer examples showing company name, contact people, and business information. Required and optional field indicators to help prevent import errors. Customer code guidance explaining our five-letter, two-digit format. Blank customer codes permitted so the application can generate them during import. Sample data clearly identified so it isn't accidentally imported as real customer information. These templates will be generated from the application's current import requirements, helping them stay consistent as the system evolves.

### Q038 — Import Preview and Rollback

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend tracking each import as a separate batch, using tables such as customer_import_batches and customer_import_records. The Undo Import feature will support: Import history: View previous imports, including filenames, dates, users, and record counts. Preview before undoing: See exactly which customer records and field changes would be affected. Safe reversal: Reverse newly created records that have no subsequent business activity. Transaction protection: Never automatically remove customers linked to invoices, payments, inventory, consignments, or other business transactions. Updated records: Restore previous field values only when doing so won't overwrite changes made after the import. Partial rollback: Identify records that can be safely reversed and those requiring manual review. Audit trail: Record who initiated the rollback, when it occurred, and its results. Customer codes assigned during an import will remain permanently retired if their records are reversed, so those codes cannot accidentally be reused.

### Q039 — Import Permissions

**Status:** Approved / recorded.
**Owner answer:** restricted to admins is fine
**Recorded outcome (excerpt):** Our role-based permissions will work as follows: These permissions will be enforced by the backend, not merely by hiding buttons in the interface. All import and rollback operations will be recorded in the centralized audit history.

### Q040 — Import Error Handling

**Status:** Approved / recorded.
**Owner answer:** partial imports with the ability to correct would be good
**Recorded outcome (excerpt):** The customer import process will support the following: For example, if you import 500 customer records and 12 contain errors, the application can save the 488 valid records and hold the remaining 12 for correction. All imports and retries will remain Administrator-only operations, as we previously approved.

### Q041 — Saving Import Progress

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend extending our import batch tracking to support imports that remain in progress across multiple application sessions. The design will support: Automatic progress saving: Preserve import progress, column mappings, and corrections as you work. Resume later: Reopen an unfinished import after closing and restarting the application. Error preservation: Retain failed records and their validation messages. Completed record tracking: Remember which records were successfully imported so they aren't imported twice. Safe retries: Retry only records that still need processing. Import status: Track sessions as Draft, In Progress, Partially Completed, Completed, or Canceled. Administrator-only access: Only Administrators can resume, modify, or cancel import sessions. Audit history: Record import attempts, corrections, and completion. We'll also ensure that closing the application doesn't interrupt an individual database transaction halfway through.

### Q042 — Import Session Retention

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Our customer import system will follow these rules: No automatic expiration: Unfinished imports remain available regardless of how much time has passed. Automatic progress saving: Column mappings, corrections, validation results, and import progress are preserved. Resume anytime: An Administrator can reopen an unfinished import and continue working. Status Center notifications: Unfinished imports appear in the Message & Status Center, with older sessions highlighted for review. Explicit completion or cancellation: Only an Administrator can close an unfinished import. Safe cancellation: Canceling an import won't automatically remove records already imported successfully. The separate Undo Import feature will handle reversals. Audit history: Completion, cancellation, and resumption events are recorded. This gives us a comprehensive customer import system with error correction, partial imports, rollback safeguards, and resumable sessions.

### Q043 — Customer Record Save Behavior

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** The customer form will support: Automatic draft saving: Save unfinished work approximately every 30 seconds when changes are present. Draft recovery: Resume an unfinished customer record after closing or restarting the application. No premature customer codes: Drafts won't receive permanent customer codes until successfully saved. Separate draft storage: Unfinished records won't appear in normal customer searches or reports. Manual Save: Validate the information and create the official customer record. Discard Draft: Allow you to explicitly remove an unwanted draft. Access control: Drafts will be associated with the user who created them. We'll also ensure that automatic draft saving doesn't accidentally create duplicate customers.

### Q044 — Multiple Customer Drafts

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** I recommend including a customer_drafts table with the following capabilities: Multiple drafts: Create and maintain several unfinished customer records simultaneously. Automatic saving: Save changes approximately every 30 seconds. Draft Customers list: Display each draft's customer name, last modified date, and creator. Resume editing: Open any draft and continue where you left off. Individual draft management: Save or discard drafts independently. No permanent customer code: Assign the code only when the customer record is successfully saved. Duplicate detection: Check for potential duplicates when converting a draft into an official customer record. User permissions: Drafts are private to their creator unless explicitly shared with an authorized user.

### Q045 — Unsaved Changes Warning

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** If you attempt to leave a customer form while changes haven't yet been saved, the application will offer three choices: We'll also include these safeguards: Automatic draft saving continues approximately every 30 seconds. The warning appears only when there are changes that haven't been saved. Existing customer records won't be modified simply because a draft was saved. New customers won't receive permanent customer codes until their official records are saved. The application will use a browser-leave warning where supported, although browser restrictions may limit the available choices.

### Q046 — Draft Retention

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** Our proposed customer_drafts table will support: No automatic expiration: Drafts remain available regardless of age. Multiple drafts: You can maintain several unfinished customer records simultaneously. Automatic saving: Changes are saved approximately every 30 seconds. Draft recovery: Resume work after closing or restarting the application. Explicit removal: Drafts are removed only when saved as official customer records or deliberately discarded. No premature customer codes: Permanent codes are assigned only when the official customer record is saved. User ownership: Drafts remain associated with their creator, with access controlled by permissions.

### Q047 — Customer Draft Visibility

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Administrators can access all customer drafts, while Staff members can access only their own. We'll also include these safeguards: Drafts retain the identity of their original creator. Administrator access to another user's draft is recorded in the audit history. Drafts cannot be edited simultaneously by two users without conflict protection. Recovering a draft does not change its original creator. Drafts remain available indefinitely until saved or explicitly discarded.

### Q048 — Draft Editing Conflicts

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Each customer draft will support the following behavior: One active editor: Only one user can modify a particular draft at a time. Read-only access: Other authorized users can view the draft without changing it. Editor identification: The application displays who is currently editing the draft. Automatic lock release: Editing locks expire after a configurable period of inactivity or a lost connection. Conflict protection: The application verifies the draft's version before saving, preventing an expired editor session from overwriting newer changes. Administrator recovery: An Administrator can recover a draft when necessary, with the action recorded in the audit history. We'll design this around a temporary editing lock rather than permanently locking records to individual users.

### Q049 — Editing Existing Customer Records

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Our customer editing system will follow these rules: One active editor: Only one user can edit a customer's main record at a time. Read-only access: Other authorized users can still view the customer record. Editor identification: The application displays who is currently editing the record. Automatic lock release: Editing locks expire after a configurable period of inactivity or lost connectivity. Conflict detection: Version checks prevent outdated edits from overwriting newer information. Administrator override: Administrators can release abandoned locks, with the action recorded in the audit history. Independent transactions: Other users can continue processing invoices, payments, and other authorized transactions without being blocked by someone editing the customer's contact information. This will protect customer data while allowing normal business operations to continue.

### Q050 — Customer Record Navigation

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** The Customer screen will support: Previous / Next buttons: Move between customer records without returning to the Customer List. Preserved search results: Navigation follows the current search filters and sorting order. Position indicator: Display your location within the results, such as Customer 12 of 85. Boundary handling: Disable Previous on the first record and Next on the last. Unsaved changes protection: Warn before navigating away if edits haven't been saved. Editing locks: Release the previous customer's editing lock when leaving that record, provided any pending changes have been handled. These controls will appear near the top of the Customer screen, alongside the customer name and code.

### Q051 — Recently Viewed Customers

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** I recommend storing recently viewed customers as a user-specific preference, rather than as part of the customer's business information. The feature will support: 10 most recently viewed customers, ordered from newest to oldest. Quick access: Click a customer to reopen their record. Individual history: Each Administrator or Staff member has their own list. Automatic updates: Opening a customer moves that record to the top. No duplicates: Each customer appears only once. Permission checks: Users can only reopen records they're authorized to access. Clear history: Optionally clear your recently viewed list without affecting customer records. We'll include this in the application's navigation design.

### Q052 — Favorite Customers

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** Favorites will work as follows: One-click Favorites: Mark or unmark a customer using a star icon. Personal Favorites: Each Administrator or Staff member maintains their own list. No fixed limit: You can favorite as many customers as you like. Persistent: Favorites remain saved between application sessions. Quick access: A Favorites section in the Customer navigation menu. Search and sorting: Find and organize your favorite customers. Permissions: Favorites never override customer access restrictions. We'll keep Favorites separate from Recently Viewed Customers. Recently Viewed updates automatically, while Favorites remain until you remove them.

### Q053 — Customer Record Completion

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** The application will identify missing or incomplete customer information and display helpful reminders. We'll use these principles: Nonblocking warnings: Missing optional information won't prevent saving. Visual indicators: The Customer screen will identify information that needs attention. Context-sensitive validation: Information may become required for a particular operation, such as preparing a shipment. Configurable rules: We can adjust completeness requirements as business needs evolve. No artificial completeness score: We'll focus on actionable missing information rather than assigning customers arbitrary percentages. Next Step — Customer Database Tables With our customer functionality decisions established, I recommend moving from feature planning into the actual relational database design. We'll document each table's fields, data types, primary keys, foreign keys, indexes, and relationships. We'll also build the ERD we agreed upon.

### Q054 — Primary Keys

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll use an automatically generated numeric customer_id as the primary key and retain our permanent, seven-character customer_code as a unique business identifier. Now we're ready to begin defining the actual database tables! Customer Database Schema — Table 1: customers I recommend starting with the central customers table, which will serve as the foundation for the entire Customer Management module. Proposed schema, not yet approved or implemented. Data types are intended for MySQL/MariaDB and can be refined during schema review. We'll keep addresses, phone numbers, email addresses, customer roles, notes, and other repeating information in separate related tables. That will allow each customer to have multiple entries without duplicating the main customer record.

### Q055 — Customer Name Fields

**Status:** Approved / recorded.
**Owner answer:** we probably will need a suffix and prefix field for Mr. Jr. etc
**Recorded outcome (excerpt):** We'll include optional name_prefix and name_suffix fields for individual customers and business contacts, alongside their first, middle, and last names. These fields will support proper names in correspondence, invoices, and customer searches without affecting customer-code generation.

### Q056 — Customer Status

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Inactive customers will remain available for new business transactions, with a warning indicating their inactive status. We'll implement the following behavior: Inactive customers remain searchable and selectable. Selecting an inactive customer displays a warning. The warning does not prevent creating invoices, consignments, or inventory acquisitions. Customers can be reactivated whenever appropriate. Historical transactions and status changes remain preserved.

### Q057 — Customer Types

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Administrators will be able to change a customer record between Individual and Business, with appropriate safeguards. We'll establish the following rules: Only administrators can change the customer type. The application displays a confirmation warning before saving. The existing customer_id and customer_code remain unchanged. All historical transactions and customer relationships are preserved. Any incompatible information is flagged for review rather than automatically deleted. The change is recorded in the audit history, including the previous and new customer types.

### Q058 — Customer Roles

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll use separate relational tables to manage customer roles, allowing each customer to be a Buyer, Consignor, Inventory Source, or any combination of these. Approved Customer Roles Schema We'll also enforce a unique constraint on the combination of customer_id and role_id, preventing duplicate role assignments. This design will allow us to add additional customer roles in the future without restructuring the database.

### Q059 — Default Customer Role

**Status:** Approved / recorded.
**Owner answer:** A is fine
**Recorded outcome (excerpt):** When creating a new customer, the Buyer role will be selected automatically. The behavior will be: Buyer is selected by default. You can deselect Buyer before saving. You can select Consignor, Inventory Source, or any combination of roles. Role assignments are stored in customer_role_assignments. Existing customer roles can be modified later, with changes recorded in the audit history.

### Q060 — Customers Without Roles

**Status:** Approved / recorded.
**Owner answer:** I should think a customer can have multiple roles
**Recorded outcome (excerpt):** We'll establish these rules: Buyer is selected by default when creating a customer. Every customer must have at least one role before saving. Customers can have multiple roles simultaneously. You can deselect Buyer if you select Consignor or Inventory Source instead. Roles can be added or removed later, provided at least one remains assigned. That keeps our customer database focused on actual business relationships.

### Q061 — Role Changes and Transaction History

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Customer roles can be removed without affecting historical transactions. For example, if John Smith stops consigning books, we can remove his Consignor role while preserving his previous consignments, payments, and associated records. We'll also record role changes in the audit history, including who made the change and when.

### Q062 — Role Assignment History

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll maintain a complete history of customer role assignments, including when each role was added, removed, or reassigned. Updated customer_role_assignments Table A role is considered currently active when removed_at is empty. We'll also enforce a database constraint to prevent a customer from having two active assignments for the same role, while allowing multiple historical assignments.

### Q063 — Customer Contact Information

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll use the customer_emails table to support multiple email addresses per customer, with separate designations for the primary contact address and the default invoice address. We'll enforce these rules: Each customer can have multiple email addresses. Only one active email can be designated as primary. Only one active email can be designated as the default invoice recipient. The primary and invoice email can be the same address. Email addresses are optional when creating a customer. Inactive email addresses remain available for historical reference. Changes to email addresses and their designations are recorded in the audit history.

### Q064 — Email Address History

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll preserve previous customer email addresses as inactive records rather than overwriting or deleting them. This means: Previous email addresses remain searchable for historical reference. Inactive addresses won't be selected automatically for new correspondence. An inactive address can be reactivated if the customer begins using it again. Previously sent invoices and communications retain the actual recipient email address. All changes are recorded in the audit history.

### Q065 — Email Address Verification

**Status:** Approved / recorded.
**Owner answer:** sure
**Recorded outcome (excerpt):** We'll add email verification tracking to the customer_emails table. New email addresses will default to Unverified. Verification will be optional, and staff can update the status manually. Addresses marked Invalid will trigger a warning before use.

### Q066 — Duplicate Email Addresses

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll allow the same email address to be associated with multiple customer records while displaying a duplicate-address warning. For example, John and Mary Smith could each have their own customer record while sharing smithfamily@example.com. The application will: Allow shared email addresses without blocking saves. Identify other customers using the same address. Display a warning with links to those customer records. Never automatically merge customers because they share an email. Preserve each customer's independent invoices, purchases, and transaction history.

### Q067 — Email Address Formatting

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll automatically trim leading and trailing spaces from email addresses and validate their formatting before saving. The application will preserve the entered capitalization, reject clearly malformed addresses, and check for duplicates using a case-insensitive comparison. Formatting validation won't be treated as proof that an email address exists or can receive messages.

### Q068 — Customer Phone Numbers

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll adopt the proposed customer_phones table structure. Each customer can have multiple phone numbers, including international numbers and extensions. We'll support customizable labels such as Mobile, Home, Work, and Fax. We'll also enforce these rules: Only one active phone number can be designated as primary. Phone numbers are optional when creating a customer. Previous numbers can be marked inactive without losing their history. Changes are recorded in the audit history. Phone numbers remain searchable from the Customer Management screen.

### Q069 — Shared Phone Numbers

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll allow multiple customers to share the same phone number while displaying a duplicate warning. The system will: Compare normalized phone numbers so formatting differences don't prevent duplicate detection. Account for international country codes and extensions. Show links to other customers associated with the same number. Allow the number to be saved despite the warning. Never automatically merge customer records because of shared contact information.

### Q070 — Phone Number Formatting

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll store both the original display-formatted phone number and a normalized version for searching and duplicate detection. Updated customer_phones Table If the application cannot reliably determine a country code, it will preserve the entered number rather than guessing.

### Q071 — Customer Addresses

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll adopt the proposed customer_addresses table, including international address support and separate default billing and shipping addresses. The finalized design will support: Multiple addresses per customer. Customizable address labels (Home, Business, PO Box, etc.). One default billing address and one default shipping address. The same address serving both purposes. Historical addresses retained as inactive records. Address snapshots on invoices and shipments to preserve transaction accuracy. Audit tracking for address changes.

### Q072 — Address History

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll preserve previous customer addresses as inactive records rather than overwriting them when a customer moves. This means: Previous addresses remain available for historical reference. New addresses receive their own address_id. Default billing and shipping addresses can be updated independently. Inactive addresses won't be automatically selected for new transactions. Existing invoices and shipping records retain their original address information. Address changes are recorded in the audit history. We'll also distinguish between correcting a typo in an existing address and recording an actual address change, so minor corrections don't unnecessarily create new address records.

### Q073 — Address Validation

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll include basic address validation in the Workman's Books Customer Management module without requiring external address verification. The application will: Check that entered addresses have the appropriate basic fields and formatting. Validate U.S. ZIP code formats (five digits or ZIP+4). Support international postal codes and address formats. Display warnings for incomplete or unusual addresses without unnecessarily blocking saves. Allow addresses to be marked as verified manually. Leave integration with USPS or another address-verification service as a possible future enhancement.

### Q074 — Address-Specific Notes

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll add an optional address_notes field to the customer_addresses table. These notes will be specific to an individual address rather than the customer's overall record. Updated Address Fields Address notes will be visible when reviewing or selecting an address, particularly when preparing shipments. you could add a "care of" or c/o field to address that situation That's an excellent suggestion! 😊 A Care Of (c/o) field would be a simple, practical solution, particularly for Workman's Books. Rather than requiring a separate business contact relationship just to address correspondence, we can add the following field to customer_addresses: For example, a mailing address could appear as: John Smith c/o Robert Johnson 123 Main Street Orlando, FL 32801 Or for a business: Workman's Books c/o Receiving Department 456 Commerce Drive Orlando, FL 32801 The care_of field would be optional, searchable, and included on shipping labels or correspondence when populated. We would also preserve its value in historical invoice and shipping address snapshots.

### Q075 — Revised decision

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll add an optional care_of field to the customer_addresses table and defer linking individual addresses directly to business contacts. This gives us a straightforward way to address mail and shipments without unnecessarily complicating the database. Updated customer_addresses Fields The c/o information will also be preserved in historical shipping and invoice address snapshots.

### Q076 — Address Formatting

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll automatically format customer addresses according to the destination country's postal conventions when generating invoices, shipping labels, and correspondence. The application will preserve the original address information in the database and apply formatting only when displaying or printing it. This will include appropriate placement of postal codes, states or provinces, and country names. We'll also retain the ability to review an address before printing.

### Q077 — Business Contacts

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll adopt the proposed customer_contacts table for managing multiple contact people associated with a business customer. Each business can have multiple contacts, with one designated as the primary contact. We'll also preserve former contacts as inactive records rather than deleting their history.

### Q078 — Business Contact Email Addresses and Phone Numbers

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll extend our existing customer_emails and customer_phones tables to support individual business contacts without creating redundant tables. Updated Contact Information Relationships When contact_id is empty, the information belongs to the customer or business generally. When populated, it belongs to a specific business contact. We'll also enforce referential integrity so that a contact cannot accidentally be associated with another customer's email or phone number.

### Q079 — Business Contact Communication Preferences

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll allow business contacts to have multiple communication purposes, helping Workman's Books direct correspondence to the appropriate person. Proposed Communication Purpose Tables Rather than limiting each contact to a single purpose, I recommend two related tables: For example, Mary Jones could be assigned both Accounting and Shipping, while John Smith handles Purchasing. These assignments will help suggest recipients for correspondence, but you'll always be able to override the suggestion. We'll also retain the actual recipient information in the communication history.

### Q080 — Former Business Contacts

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll preserve former business contacts as inactive records, including their historical communication purposes and correspondence. When a contact leaves a company: Their record remains in the database. Their previous communications and assignments remain available for reference. They are excluded from automatic recipient suggestions. Another contact can assume their responsibilities. The change is recorded in the audit history. This will help Workman's Books maintain accurate business relationships without losing valuable historical information.

### Q081 — Business Contact History

**Status:** Approved / recorded.
**Owner answer:** A is fine
**Recorded outcome (excerpt):** We'll keep business contacts associated with their respective business customer records. For example, if Mary Jones leaves Company A and joins Company B, we'll mark her contact record at Company A inactive and create a new contact record under Company B. This keeps the design straightforward while preserving each company's independent contact history.

### Q082 — Customer Notes

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll adopt the proposed customer_notes table, including categorized, searchable notes and a complete audit history of edits. Each note will retain its creation date, author, last modification date, and editing history. Notes will appear chronologically in the customer's record, with options to search and filter by category.

### Q083 — Customer Note Categories

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll make customer note categories configurable, allowing administrators to manage them without changing the database structure. Updated Customer Notes Schema We'll use two related tables: Administrators will be able to add, rename, and deactivate categories. Deactivated categories will remain associated with existing notes but won't be available for new notes. All category changes will be recorded in the audit history.

### Q084 — Note Visibility

**Status:** Approved / recorded.
**Owner answer:** I don't see that detail as necessary
**Recorded outcome (excerpt):** We'll keep customer notes straightforward: All authorized users who can access a customer record can view its notes. Notes will remain categorized, searchable, and dated. The application will record who created or modified each note. We won't add a separate Administrator Only designation.

### Q085 — Editing and Deleting Notes

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll allow customer notes to be edited and soft-deleted while preserving their history. The rules will be: Authorized users can edit existing notes. Previous versions remain available through the audit history. Deleted notes disappear from the normal customer view but remain in the database. Administrators can review and restore deleted notes. Every edit, deletion, and restoration is recorded with the responsible user and timestamp.

### Q086 — Customer Note Attachments

**Status:** Approved / recorded.
**Owner answer:** A is fine
**Recorded outcome (excerpt):** We'll allow customer notes to link directly to documents already associated with that customer. Updated Customer Notes Schema We'll introduce a linking table: This will allow one note to reference multiple documents and one document to be associated with multiple notes. The files themselves will remain in Dropbox, as previously planned. Removing a document link from a note won't delete the underlying document.

### Q087 — Customer Note Reminders

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll allow customer notes to be linked to one or more follow-up reminders. For example, a note about a customer's request for an updated invoice could be linked to a reminder assigned to a staff member. Proposed customer_note_reminders Table The combination of note_id and reminder_id will be unique, preventing duplicate links. Reminders will remain independent records. Completing, rescheduling, or removing a link to a reminder won't change the original note.

### Q088 — General Customer Notes

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll add a dedicated general_notes field to the main customers table, separate from the categorized customer note history. Updated customers Table This field will: Appear on the customer's General screen. Support longer descriptions and customer preferences. Be searchable through Customer Management. Be available to authorized staff. Preserve previous versions through our audit history. The categorized customer_notes table will continue to handle dated notes, correspondence details, and follow-up information.

### Q089 — Customer Tags

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll allow unlimited customer tags for both individuals and businesses. Approved Customer Tagging Schema We'll enforce a unique constraint on customer_id and tag_id to prevent duplicate assignments. This design will allow Workman's Books to: Assign multiple collecting interests or classifications to a customer. Search and filter customers by one or more tags. Use tags to identify potential buyers for particular inventory. Support targeted communications while honoring promotional opt-in preferences. Let administrators add, rename, or deactivate tags without losing existing assignments.

### Q090 — Tag Organization

**Status:** Approved / recorded.
**Owner answer:** that's fine
**Recorded outcome (excerpt):** We'll organize customer tags into administrator-configurable categories, making them easier to manage as Workman's Books grows. Updated Customer Tagging Schema We'll use three related tables: Administrators will be able to create, rename, and deactivate categories and tags without losing historical customer assignments.

### Q091 — Tag Selection and Filtering

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll support both Match ANY and Match ALL when filtering customers by multiple tags. For example, selecting Spanish Colonial Numismatics and Rare Books will produce different results depending on the selected mode: These filters will work alongside other customer search criteria, such as customer roles, account status, and location.

### Q092 — Customer Tag History

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll preserve the complete history of customer tag assignments and removals, consistent with our approach to customer roles. Updated customer_tag_assignments Table Only active assignments will appear on a customer's current profile, but historical assignments will remain available for reference. We'll also prevent duplicate active assignments of the same tag.

### Q093 — Customer Relationships

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** Customer relationships will be visible automatically from both customer records, without requiring duplicate entries. For example, if John Smith and Mary Smith are linked as spouses, each customer's profile will display the other under Related Customers. We'll also account for directional relationships. For example, if John Smith is recorded as the owner of a business, the business's record will identify John as its owner. Each customer will continue to maintain separate customer codes, invoices, payments, and transaction histories.

### Q094 — Relationship History

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll preserve historical customer relationships, including optional start and end dates. Updated customer_relationships Table We'll ensure that relationships appear on both customer profiles and that ending a relationship doesn't affect either customer's financial or transaction history.

### Q095 — Relationship Types

**Status:** Approved / recorded.
**Owner answer:** yes
**Recorded outcome (excerpt):** We'll make customer relationship types administrator-configurable, including their reverse descriptions. Approved customer_relationship_types Table For example, if John Smith is recorded as the Owner of a business, the business's customer record can automatically display John under Owned By. Administrators will be able to add, rename, and deactivate relationship types. Existing relationships will retain their history. We'll also update customer_relationships to reference relationship_type_id rather than storing the relationship name directly.

### Q096 — Preventing Duplicate Relationships

**Status:** Owner-approved in follow-on review (20 October 2026).
**Owner answer:** Option A — prevent duplicate active relationships in either direction while allowing distinct relationship types between the same two customers.
**Decision:** Detect reversed duplicates using the relationship type and its reverse description; warn and open the existing active relationship instead of inserting another. Preserve historical ended relationships and permit multiple different relationship types between the same customer pair.

## Questions 97–127 — Owner-reconfirmed follow-on decision register

**Review status:** All 31 decisions reconfirmed in the 20 October 2026 review. The detailed question-and-answer transcript for these questions is not in the uploaded Q1–96 Word file; the concise register below preserves the recovered decisions.

**Source note:** These summaries are based on decisions documented in the current project continuation, not the uploaded Q1–96 Word file.

### Q097

**Status:** Approved / recorded. **Decision:** Independent customer_tax_exemptions records per customer, jurisdiction, certificate and document.

### Q098

**Status:** Approved / recorded. **Decision:** Expired certificate warning; authorized audited override.

### Q099

**Status:** Approved / recorded. **Decision:** PDF/JPG/PNG supporting documents with history.

### Q100

**Status:** Approved / recorded. **Decision:** New certificates Pending until administrator approval.

### Q101

**Status:** Approved / recorded. **Decision:** Permanent audit history of approval, rejection, revocation and edits.

### Q102

**Status:** Approved / recorded. **Decision:** Match approved exemption to invoice jurisdiction; audited override; preserve finalized history.

### Q103

**Status:** Approved / recorded. **Decision:** Invoice shows exemption designation/type/certificate number.

### Q104

**Status:** Approved / recorded. **Decision:** Renewal creates linked new certificate requiring approval; preserve previous.

### Q105

**Status:** Approved / recorded. **Decision:** Configurable 30/60/90-day renewal and expiry notifications.

### Q106

**Status:** Approved / recorded. **Decision:** Administrator-only certificate management; no customer portal.

### Q107

**Status:** Approved / recorded. **Decision:** Archive instead of delete; archived certificates excluded from new invoices.

### Q108

**Status:** Approved / recorded. **Decision:** Administrator-only filtered reports and CSV/Excel/PDF exports.

### Q109

**Status:** Approved / recorded. **Decision:** Immutable per-invoice certificate usage and tax calculation history.

### Q110

**Status:** Approved / recorded. **Decision:** Approved certificates apply to purchases in applicable jurisdiction, subject to tax law.

### Q111

**Status:** Approved / recorded. **Decision:** Automatic priority selection of eligible certificates; audited administrator override.

### Q112

**Status:** Approved / recorded. **Decision:** Finalized invoices preserved; corrections through linked adjustments/corrected invoices.

### Q113

**Status:** Approved / recorded. **Decision:** No periodic manual review requirement; expiration alerts and administrator-initiated review.

### Q114

**Status:** Approved / recorded. **Decision:** Rejection/revocation recalculates affected unfinalized invoices; finalized invoices unchanged.

### Q115

**Status:** Approved / recorded. **Decision:** CSV/Excel certificate import with mapping, preview, duplicate detection, validation.

### Q116

**Status:** Approved / recorded. **Decision:** Comprehensive validation; incomplete drafts permitted but cannot be approved.

### Q117

**Status:** Approved / recorded. **Decision:** Document versions, uploader/time and current-version designation.

### Q118

**Status:** Approved / recorded. **Decision:** Configurable administrator RBAC for certificate operations, with audit.

### Q119

**Status:** Approved / recorded. **Decision:** Secure document references, metadata, permissions and storage/recovery coordination.

### Q120

**Status:** Approved / recorded. **Decision:** Certificate files in Dropbox; use Dropbox versioning/recovery for documents; database backups separate.

### Q121

**Status:** Approved / recorded. **Decision:** Central Dropbox certificate folder; unique filenames.

### Q122

**Status:** Approved / recorded. **Decision:** Filename CustomerNumber_TAX_CERT_Year.extension (year of issuance).

### Q123

**Status:** Approved / recorded. **Decision:** Suffix \_02, \_03 etc. on filename collisions; never overwrite.

### Q124

**Status:** Approved / recorded. **Decision:** Application-driven upload, naming, reference storage and retrieval via Dropbox.

### Q125

**Status:** Approved / recorded. **Decision:** Secure temporary retention and retry for failed uploads, Pending Upload and administrator alerts.

### Q126

**Status:** Approved / recorded. **Decision:** Verify initial upload success and integrity; no periodic integrity checks.

### Q127

**Status:** Approved / recorded. **Decision:** Authorized administrator PDF/JPG/PNG preview and download through application.

## Reconciliation notes and schema design guardrails

- **Review completion:** Q1–127 are owner-confirmed, including Q96 answered in the follow-on review. This confirms business decisions, **not** proposed SQL tables or deployment.
- **Q23–27:** Final customer code is immutable after first save, five uppercase letters and decimal suffix 01–99; middle names excluded. Use the latest rules over earlier examples.
- **Q54 / Q122:** Internal numeric `customer_id`, immutable seven-character `customer_code`, and certificate filename `CustomerNumber` are distinct concepts. **The mapping/definition of `CustomerNumber` in certificate filenames needs clarification during schema design**; do not silently equate it to `customer_id` or `customer_code`.
- **Q58 / Q62:** The early suggestion of unconditional uniqueness `(customer_id, role_id)` conflicts with retained assignment history. Final rule: at most one **active** assignment for each customer/role, with repeat historical rows allowed.
- **Q74–75:** Preserve optional `address_notes` and `care_of`; defer address-to-business-contact direct linking; snapshot `care_of` for historical shipping/invoices.
- **Q81:** Contact persons belong to one business customer record. A person joining another business receives a separate contact record, preserving the first company's history.
- **Q84:** No special administrator-only visibility level for notes; all staff with authorized customer access may view notes.
- **Q93–96:** One relationship stored, displayed from both ends; use reverse descriptions, track active/history, block reverse duplicates only for the same active relationship type.
- **Q109 / Q112 / Q114:** Finalized invoices and exemption usage remain immutable; changes require linked corrections, while unfinalized invoices can be recalculated.
- **Q120:** Dropbox document version/recovery and central database backup/restore are **separate** designs. Restore reconciliation, file identifiers, permission boundaries, and retention need technical specification.
- **Q126:** Verify file integrity at upload; no scheduled recurring integrity verification requirement.

## Next design tasks (not yet approved)

1. Produce a **draft** customer ERD and table inventory, including PK/FK, uniqueness, history, deletion and access rules.
2. Define logical and physical constraints (including active-only uniqueness), transactional save/rollback behavior, and indexing.
3. Define secure Dropbox integration and database/document disaster recovery and reconciliation.
4. Validate tax eligibility rules and external integrations before implementation.
5. Review detailed ERD/schema with owner; customer questionnaire Q128 remains separate from the approved application reconciliation Finding 128. Application reconciliation is paused at Finding 200, with Finding 151 next after checkpoint acknowledgment.

## Application-wide logical reconciliation cross-reference — 27 October 2026

**Separate numbering system:** Customer Questions Q1–127 in this document are distinct from application-wide logical schema Findings 1–200. In particular, **Finding 128 is approved (Option B)** and does not resolve or supersede any earlier reference to a future customer Question Q128.

The owner approved application-wide Findings 1–200, including Finding 150 Option A on manual credit card statement reconciliation. The approved working inventory contains **144 logical tables**, not deployed tables. The latest continuity checkpoint is `Workmans_Books_Continuity_Checkpoint_Through_Finding_150_2026-10-27.docx`. The full inventory and detailed financial requirements addendum are in `docs/requirements/SOFTWARE_REQUIREMENTS.md`.

### Additional approved tables after Finding 100

- Finding 103: `consignor_repayments` (141 → 142).
- Finding 118: `financial_report_versions` (142 → 143).
- Finding 121: `financial_report_files` (143 → 144).
- Findings 122–150: no further tables.

### Customer-related reconciliation guardrails

- Customer drafts are stored locally on Windows, not in a `customer_drafts` database table (Finding 57); this supersedes preliminary table suggestions in Q44–48.
- Existing customer role/relationship/history, tax-exemption, documents, import and audit decisions remain intact unless explicitly superseded by a later approved finding.
- Use the working 144-table inventory for current logical table names; earlier candidate names in customer Q1–127 excerpts are historical proposals, not automatic additions.
- Preserve finalized invoices, settlements, historical customer identities and audit trails; use authorized corrections and linked adjustments.
- Continue one finding at a time, with explicit approval. No SQL or implementation until the complete logical design and architecture are separately approved.

## Finding 200 continuity addendum — approved logical decisions 151–200

**Status:** All Findings 151–200 approved as Option A, no additional logical tables. Total **200 approved findings / 144 logical tables**. Pause before Finding 201. The Version 2.0 SRS baseline and customer Q1–127 decisions remain intact. No SQL, implementation or physical-schema sign-off.

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
