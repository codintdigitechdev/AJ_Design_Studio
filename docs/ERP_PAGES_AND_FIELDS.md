# ERP Pages, URLs and Module-wise Field Specifications

**Status: PROPOSED — PENDING APPROVAL.**

**URL rules:**
- All ERP URLs sit under `/erp/` and go through the ERP front controller
  (`docs/TECHNICAL_REQUIREMENTS.md` §2.2).
- Any page that changes data uses **POST with a CSRF token**. GET pages only display data.

**Permission column:** uses the codes from `docs/PERMISSION_MATRIX.md`.

**Field-type abbreviations:**

| Code | Meaning |
|---|---|
| T | text (max length given) |
| TA | long text (textarea) |
| N | number |
| M | money (₹, 2 decimals, ≥ 0) |
| D | date (DD/MM/YYYY on screen) |
| DT | date and time |
| SEL | choose one from a list |
| MSEL | choose several from a list |
| CHK | checkbox |
| FILE | file upload |
| RO | read-only |
| AUTO | filled in by the system |

---

## 1. Page and URL list

### 1.1 Authentication

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/login` | GET, POST | Login form | public |
| `/erp/logout` | POST | Log out | any user |
| `/erp/forgot-password` | GET, POST | Request a reset email (always shows the same message) | public |
| `/erp/reset-password?token=…` | GET, POST | Set a new password | valid token |
| `/erp/change-password` | GET, POST | Change own password (forced on first login) | any user |
| `/erp/profile` | GET, POST | Own profile | any user |

### 1.2 Dashboard and follow-ups

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/` → `/erp/dashboard` | GET | Dashboard | 1 / 1a |
| `/erp/follow-ups` | GET | Follow-up list (due today / overdue / upcoming) | 13 |
| `/erp/follow-ups/new`, `/erp/follow-ups/{id}/edit` | GET, POST | Add or edit a follow-up | 13 |
| `/erp/follow-ups/{id}/done` | POST | Mark done, with outcome | 13 |

### 1.3 Enquiries

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/enquiries` | GET | List: filters for status, source, assignee, date range; "Website – unreviewed" queue | 2 V |
| `/erp/enquiries/new` | GET, POST | New enquiry | 2 C |
| `/erp/enquiries/{id}` | GET | Detail: summary, activities, follow-ups, quotations | 2 V |
| `/erp/enquiries/{id}/edit` | GET, POST | Edit | 2 E |
| `/erp/enquiries/{id}/status` | POST | Change status, with reason | 2 S |
| `/erp/enquiries/{id}/activities` | POST | Add an activity | 2 E |
| `/erp/enquiries/{id}/convert` | GET, POST | Convert to client + project (wizard) | 2b |
| `/erp/enquiries/{id}/spam` | POST | Mark as spam | 2a |

### 1.4 Clients

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/clients` | GET | List | 3 V |
| `/erp/clients/new` | GET, POST | New client | 3 C |
| `/erp/clients/{id}` | GET | Detail: projects, quotations, financial summary (3a) | 3 V |
| `/erp/clients/{id}/edit` | GET, POST | Edit | 3 E |
| `/erp/clients/{id}/deactivate` | POST | Deactivate | 3 D |

### 1.5 Projects

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/projects` | GET | List: filters for status, type, client, member | 4 V |
| `/erp/projects/new` | GET, POST | New project | 4 C |
| `/erp/projects/{id}` | GET | Overview tab | 4 V |
| `/erp/projects/{id}/edit` | GET, POST | Edit | 4 E |
| `/erp/projects/{id}/status` | POST | Change status | 4 S |
| `/erp/projects/{id}/members` | POST | Manage the team | 4 E |
| `/erp/projects/{id}/quotations` | GET | Quotations tab | 6 V |
| `/erp/projects/{id}/fees` | GET | Fees tab: agreement, variations, milestones, bills | 4b |
| `/erp/projects/{id}/payments` | GET | Payments tab: payments, allocations, credit, refunds | 4b |
| `/erp/projects/{id}/expenses` | GET | Expenses tab | 9 V |
| `/erp/projects/{id}/documents` | GET | Documents tab | 10 V |
| `/erp/projects/{id}/site-visits` | GET | Site visits tab ◇ | 4a |
| `/erp/projects/{id}/timeline` | GET | Activities and status history | 4 V |

### 1.6 Site visits ◇ (Q-P3)

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/projects/{id}/site-visits/new` | GET, POST | New visit (photos optional) | 4a C |
| `/erp/site-visits/{id}`, `/erp/site-visits/{id}/edit` | GET, POST | View or edit a visit | 4a |

### 1.7 Documents

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/projects/{id}/documents/upload` | GET, POST | Upload a document or a new version | 10a |
| `/erp/documents/{id}/download` | GET | Stream the file after a permission check; the download is recorded in the audit log (optional) | 10 V |
| `/erp/documents/{id}/delete` | POST | Soft delete | 10b |

### 1.8 Services

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/services` | GET | Categories with their items | 5 V |
| `/erp/services/categories/new`, `/erp/services/categories/{id}/edit` | GET, POST | Add or edit a category | 5 C/E |
| `/erp/services/items/new`, `/erp/services/items/{id}/edit` | GET, POST | Add or edit an item | 5 C/E |
| `/erp/services/reorder` | POST | Change the display order | 5 E |

### 1.9 Quotations

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/quotations` | GET | Register: filters for status, date, client | 6 V |
| `/erp/quotations/new?enquiry={id}` or `?project={id}` | GET, POST | Create, starting with R0 | 6 C |
| `/erp/quotations/{id}` | GET | Header, current revision, revision history | 6 V |
| `/erp/quotations/{id}/revisions/{rev}/edit` | GET, POST | Quotation builder (Draft only) | 6 E |
| `/erp/quotations/{id}/revisions/{rev}` | GET | View a frozen revision | 6 V |
| `/erp/quotations/{id}/revisions/{rev}/print` | GET | Print view (HTML) | 6 V |
| `/erp/quotations/{id}/revisions/{rev}/pdf` | GET | PDF | 6 V/X |
| `/erp/quotations/{id}/compare?a={rev}&b={rev}` | GET | Compare two revisions | 6 V |
| `/erp/quotations/{id}/approve` | POST | Approve ◇ | 6b |
| `/erp/quotations/{id}/send` | POST | Mark as sent | 6a |
| `/erp/quotations/{id}/new-revision` | POST | Create the next revision | 6 E |
| `/erp/quotations/{id}/decision` | POST | Accept / reject / expire / cancel | 6a |
| `/erp/quotations/{id}/email` | GET, POST | Email the PDF ◇ (Q-Q9) | 6a |

### 1.10 Fees, bills and credit notes

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/projects/{id}/fee-agreement/new` | GET, POST | Create an agreement by hand | 7 C |
| `/erp/fee-agreements/{id}/variations/new` | GET, POST | Add a variation | 7 E |
| `/erp/fee-agreements/{id}/milestones` | GET, POST | Edit milestones ◇ | 7 E |
| `/erp/bills` | GET | Bill register ◇ | 7a V |
| `/erp/bills/new?project={id}` | GET, POST | New draft bill ◇ | 7a C |
| `/erp/bills/{id}`, `/erp/bills/{id}/edit` | GET, POST | View or edit a draft bill ◇ | 7a |
| `/erp/bills/{id}/issue` | POST | Issue the bill ◇ | 7b |
| `/erp/bills/{id}/cancel` | POST | Cancel the bill ◇ | 7c |
| `/erp/bills/{id}/pdf` | GET | Bill PDF ◇ | 7a V |
| `/erp/bills/{id}/apply-credit` | POST | Apply available credit ◇ | 8a |
| `/erp/bills/{id}/credit-notes/new` | GET, POST | New credit note ◇ | 7c |
| `/erp/credit-notes/{id}`, `/erp/credit-notes/{id}/pdf` | GET | View or print a credit note ◇ | 7a V |

### 1.11 Payments and refunds

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/payments` | GET | Collection register | 8 V |
| `/erp/payments/new?project={id}` | GET, POST | Record a payment, with allocation | 8 C |
| `/erp/payments/{id}` | GET | Detail, with its allocations | 8 V |
| `/erp/payments/{id}/allocate` | GET, POST | Allocate or de-allocate | 8a |
| `/erp/payments/{id}/reverse` | GET, POST | Reverse, with reason | 8b |
| `/erp/payments/{id}/receipt` | GET | Receipt print / PDF | 8d |
| `/erp/refunds/new?project={id}` | GET, POST | New refund ◇ | 8c |
| `/erp/refunds/{id}`, `/erp/refunds/{id}/reverse` | GET, POST | View or reverse a refund ◇ | 8c |

### 1.12 Expenses ◇

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/expenses` | GET | List | 9 V |
| `/erp/expenses/new` | GET, POST | New expense | 9 C |
| `/erp/expenses/{id}` | GET | View | 9 V |
| `/erp/expenses/{id}/reverse` | POST | Reverse | 9a |

### 1.13 Portfolio

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/portfolio` | GET | Portfolio items: published / draft / featured | 11 V |
| `/erp/portfolio/new`, `/erp/portfolio/{id}/edit` | GET, POST | Add or edit an item | 11 C/E |
| `/erp/portfolio/{id}/images` | GET, POST | Upload, reorder, alt text, gallery switch | 11 E |
| `/erp/portfolio/{id}/preview` | GET | Preview as the public page | 11 V |
| `/erp/portfolio/{id}/publish`, `/erp/portfolio/{id}/unpublish` | POST | Publish or unpublish (checks consent) | 11a |

### 1.14 Reports (Q-R1)

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/reports` | GET | Report index | 14 |
| `/erp/reports/enquiries` | GET | Enquiry report; add `?format=csv` for export | 14 V/X |
| `/erp/reports/quotations` | GET | Quotation register | 14 V/X |
| `/erp/reports/projects` | GET | Project status report | 14 V/X |
| `/erp/reports/outstanding` | GET | Outstanding amounts | 14a |
| `/erp/reports/collections` | GET | Collection register | 14a |
| `/erp/reports/expenses` | GET | Expense report | 14a |
| `/erp/reports/profitability` | GET | Profitability ◇ | 14a |

### 1.15 Administration

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/users`, `/erp/users/new`, `/erp/users/{id}/edit` | GET, POST | Users | 15 |
| `/erp/users/{id}/reset-password`, `/erp/users/{id}/unlock` | POST | Admin actions on a user | 15 |
| `/erp/roles`, `/erp/roles/{id}/permissions` | GET, POST | Role permission grid | 15 |
| `/erp/settings/studio` | GET, POST | Studio profile | 16 |
| `/erp/settings/letterhead` | GET, POST | Letterhead / PDF | 16 |
| `/erp/settings/numbering` | GET, POST | Numbering formats | 16 |
| `/erp/settings/finance` | GET, POST | Billing mode, tax, rounding, lock date, features | 16 / 16c |
| `/erp/settings/website` | GET, POST | Website content | 16a |
| `/erp/settings/security` | GET, POST | Timeouts, password policy | 16 |
| `/erp/settings/lookups/{list_type}` | GET, POST | Master lists | 16 |
| `/erp/settings/backup` | GET, POST | Download a backup | 16b |
| `/erp/audit-log` | GET | Audit log, with filters | 17 |

### 1.16 Background (AJAX, JSON only)

| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/api/duplicate-check` | GET | Look for matching mobile/email | 2 C |
| `/erp/api/service-items?category={id}` | GET | Items for one category | 6 E |
| `/erp/api/quotation-preview-totals` | POST | Recalculate totals on the server | 6 E |
| `/erp/api/open-bills?project={id}` | GET | Open bills for allocation | 8 C |

The public site (`/`, `/about`, …, `/enquiry`) is listed in `docs/PORTFOLIO_WEBSITE_PLAN.md` §2.

---

## 2. Field specifications by module

Every field is checked on the server. Lengths are proposed. Fields that appear only in the
database design (`DATABASE_DESIGN.md`) and not on a form are filled in by the system.

### 2.1 Login
- **Username or email:** T 100, required.
- **Password:** required.
- **On failure:** the same generic message every time. Lockout rule: `SECURITY_RULES.md` §3.

### 2.2 Enquiry (ERP form)

| Field | Type | Req. | Validation / notes |
|---|---|---|---|
| Enquiry no. | AUTO | — | From the sequence |
| Enquiry date | D | Y | ≤ today |
| Source | SEL (`enquiry_source`) | Y | "Website" is set by the system for form submissions |
| Name | T 120 | Y | |
| Mobile | T 15 | Y | 10-digit Indian mobile, optional +91; triggers the duplicate check |
| Email | T 150 | N | Valid email format |
| Preferred contact | SEL phone / WhatsApp / email | N | |
| Location / site | T 200 | N | |
| Project type | SEL (`project_type`) | N | List PENDING (Q-S3) |
| Approx. area + unit | AREA + SEL | N | > 0 |
| Services interested | MSEL (service categories) | N | |
| Budget | T 60 | N | Free text; no amount is assumed |
| Message | TA 2000 | N | |
| Assigned to | SEL (users) | N | |
| Next follow-up | DT | N | Creates a follow-up |
| Status | SEL | Y | Transitions as in `WORKFLOWS.md` A.2 |
| Lost / close reason | SEL + TA | When Lost or Closed | |
| Consent timestamp | RO | — | Website submissions only |

### 2.3 Public enquiry form (website)
- **Fields:**
  - Name*, Mobile*, Email, City/site, Project type, Services (MSEL), Approx. area + unit,
    Message, Preferred contact
  - Privacy-notice consent tick* (required)
- **Hidden fields:** a spam-trap field (must stay empty), a timestamp (minimum fill time —
  PROPOSED 3 s), and a CSRF token.
- **Limits:** 5 submissions per IP address per hour (PROPOSED). Message 2000 characters.
  At most 2 links.

### 2.4 Client

| Field | Type | Req. | Notes |
|---|---|---|---|
| Client type | SEL | Y | individual / company / trust / institution |
| Name | T 150 | Y | |
| Contact person | T 120 | If not an individual | |
| Mobile | T 15 | Y | Duplicate warning |
| Alternate mobile | T 15 | N | |
| Email | T 150 | N | |
| Address | TA 300 | N | |
| City | T 80 | N | |
| PIN | T 6 | N | 6 digits |
| GSTIN | T 15 | N | GSTIN format; shown only if tax is enabled (Q-F3) |
| Notes | TA | N | |

### 2.5 Project

| Field | Type | Req. | Notes |
|---|---|---|---|
| Project code | AUTO | — | Format PENDING (Q-P2) |
| Project name | T 150 | Y | |
| Client | SEL / search | Y | |
| Project type | SEL | Y | |
| Site address | TA 300 | N | |
| City | T 80 | N | |
| Plot area / built-up area + unit | AREA + SEL | N | |
| Floors | N 0–50 | N | Used to generate floor-plan scope items |
| Start date | D | N | |
| Expected completion | D | N | Must be ≥ the start date |
| Status | SEL | Y | `WORKFLOWS.md` A.3 |
| Services | MSEL | N | Set from the accepted quotation |
| Team members | MSEL users + role text | N | |
| Notes | TA | N | |

### 2.6 Site visit ◇

| Field | Type | Req. | Notes |
|---|---|---|---|
| Visit date | D | Y | |
| Stage | SEL (`site_visit_stage`) | Y | Starting list from the sample, editable |
| Visited by | SEL users | Y | |
| Observations | TA 4000 | N | |
| Photos | FILE (several), JPG/PNG/WebP | N | Size limit PENDING |
| Chargeable | CHK | N | ◇ Only if Q-F5 is confirmed |

### 2.7 Project document

| Field | Type | Req. | Notes |
|---|---|---|---|
| Category | SEL (`document_category`) | Y | |
| Title | T 150 | Y | |
| Version label | T 20 | N | e.g. R1 |
| Document date | D | N | |
| File | FILE | Y | Allowed types and maximum size PENDING (Q-D1) |
| Replaces document | SEL | N | Keeps the version chain |
| Notes | TA | N | |

### 2.8 Service category and item
- **Category:** Name T 100*, Slug (AUTO, editable), Description TA, Website title T 150,
  Website description TA, Show on website CHK, Sort order N, Active CHK.
- **Item:** Category SEL*, Name T 150*, Default description TA, Default unit SEL*,
  Default rate M (optional), Show on website CHK, Sort order, Active CHK.

### 2.9 Quotation builder (one revision)

| Section | Fields | Notes |
|---|---|---|
| Header | Quotation no. (AUTO), revision (AUTO), date D*, valid until D (◇), enquiry or project (RO), client (RO / SEL), subject T 200*, site location T 200, intro text TA | |
| Area | Area AREA, basis SEL (built-up / carpet / plot / all floors / other)*, unit SEL* | Required if any area line is used; basis PENDING (Q-Q3) |
| Scope | Repeating sections: section title; items (text, link to service item, included / optional / excluded); reorder | Add from the service master; all text editable |
| Fee lines | Repeating rows: type SEL (area / area-category / fixed / item / custom), description, category, quantity, unit, area, rate, amount (AUTO, or entered for fixed/custom lines) | At least one line. Order of calculation: `WORKFLOWS.md` A.5 |
| Discount ◇ | Type SEL, value | Must not exceed the subtotal. Approval PENDING (Q-F4) |
| Tax ◇ | Tax lines (name, SAC, rate) | Only if tax is enabled (Q-F3) |
| Rounding | SEL none / ₹1 / ₹10 | Default comes from Settings |
| Payment schedule ◇ | Stage, %, amount, trigger | Must add up to 100% / the grand total |
| Text blocks ◇ | Terms, exclusions, bank details, client-acceptance block on/off, amount-in-words on/off | All off by default (`CLAUDE.md` §7) |
| Totals | Subtotal, discount, taxable, tax, rounding, grand total, amount in words — all RO | Calculated on the server |

### 2.10 Fee agreement and variation
- **Agreement:** project (RO), source revision (RO or none), agreement date D*,
  base amount M*, tax amount M, total (AUTO). A manual reason TA* is required when there is
  no quotation.
- **Variation:** date D*, amount (signed M; ≠ 0)*, reason TA*, linked revision SEL (optional).
- **Milestone ◇:** stage name T 100*, % or amount*, trigger text, due date (optional). The
  milestones must add up to the current agreed fee (a warning, not a block — PROPOSED).

### 2.11 Bill ◇
- **Header:** bill type (RO, from Settings), project*, bill date D*, due date D (optional),
  milestone SEL (optional).
- **Lines:** same structure as the quotation fee lines, plus "from site visit" and
  "from reimbursable expense" pickers ◇.
- **Tax and rounding:** as in the quotation.
- **Notes:** TA.
- **Cancel:** reason TA*. **Credit note:** amount M* ≤ the bill's open value, reason TA*.

### 2.12 Payment

| Field | Type | Req. | Notes |
|---|---|---|---|
| Receipt no. | AUTO | — | Format PENDING (Q-F6) |
| Payment date | D | Y | Must be after the lock date (unless ADM) |
| Client / project | SEL | Y | Project is limited to the chosen client's projects |
| Amount | M > 0 | Y | |
| Mode | SEL (`payment_mode`) | Y | List PENDING (Q-F7) |
| Reference / UTR / cheque no. | T 60 | Required for non-cash modes | |
| Bank | T 80 | N | |
| Notes | TA | N | |
| Allocation grid (Mode A) | Open bills with an amount box each | N | Total ≤ amount; the remainder becomes credit |
| Reversal | Reason SEL* + note TA*, reversal date D* | — | |

### 2.13 Refund ◇
- **Fields:** date D*, project*, amount M* (≤ available credit), mode SEL*, reference T 60,
  reason TA*.
- **Approved by:** AUTO (must be ADM).

### 2.14 Expense ◇

| Field | Type | Req. |
|---|---|---|
| Date | D | Y |
| Category | SEL | Y |
| Project | SEL | N (blank means overhead) |
| Paid to | T 120 | Y |
| Amount | M > 0 | Y |
| Mode | SEL | Y |
| Reference | T 60 | N |
| Attachment | FILE PDF/JPG/PNG | N |
| Reimbursable | CHK ◇ | N |
| Notes | TA | N |

### 2.15 Portfolio item

| Field | Type | Req. | Notes |
|---|---|---|---|
| Title | T 150 | Y | |
| Slug | T 160 | Y | Unique; letters, digits and hyphens |
| Category | SEL (`portfolio_category`) | Y | |
| Location | T 80 | N | City/area level only |
| Completion year | N 4 | N | |
| Area + unit, show area | AREA, CHK | N | Show area is off by default |
| Services | MSEL | N | |
| Short description | TA 300 | Y | |
| Long description | Rich text (safe-list) | N | |
| Featured | CHK | N | |
| SEO title / description | T 70 / T 160 | N | Defaults are generated |
| Linked internal project | SEL | N | |
| Client consent obtained | CHK + note | Required before publishing ◇ | Q-W5 |
| Images | FILE (several) JPG/PNG/WebP; per image: alt text T 150*, caption T 200, show in gallery CHK, order | ≥ 1 image and a cover image before publishing | Resized to 400/800/1600 px, WebP + JPEG, location data removed |

### 2.16 Follow-up
- **Fields:** linked record (RO), due DT*, assigned to SEL*, note TA*.
- **When marked done:** outcome TA*.

### 2.17 User
- **Fields:** full name T 120*, username T 50* (unique), email*, mobile, role SEL*,
  active CHK.
- **New user:** gets a temporary password, which they must change at first login.
- **Password rule:** minimum 10 characters, not the same as the username (PROPOSED, D-16).

### 2.18 Settings

| Section | Fields |
|---|---|
| Studio | Name, tagline, address, phone, WhatsApp number, email, Instagram URL, office hours, map embed URL — all publishing PENDING (Q-W3, Q-W4) |
| Letterhead | Header style SEL (logo / text heading — Q-Q2), invocation text (e.g. "श्री", optional), footer text, signature name and designation (Q-Q10), signature image ◇ |
| Numbering | Format and reset period per sequence (`WORKFLOWS.md` B.11) |
| Finance | Billing mode (Q-F1), tax enabled + default tax lines (Q-F3), rounding mode, default validity days (blank), default terms (blank), FY start month, lock date, on/off switch for each optional feature (`STAGE1_GAP_RESOLUTION.md` §5) |
| Website | Hero image(s) and text, intro, About (rich text), contact block, SEO defaults |
| Security | Idle timeout, absolute timeout, minimum password length, lockout threshold |
