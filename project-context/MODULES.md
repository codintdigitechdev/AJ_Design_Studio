# Module Specifications

All module designs are **PROPOSED** unless a line carries another tag (`CLAUDE.md` §3).
Client decisions that a module implements are marked **CLIENT-DECISION**; the way the module
implements them is still PROPOSED until approved.

Necessity ratings:
- **Core** – needed for the system to make sense.
- **Recommended** – high value, low risk.
- **Optional** – build only if the client confirms the need.

Default roles (PROPOSED, D-30; users PENDING Q-U1): **ADM** Admin/Principal · **STF** Office
staff · **SITE** Site engineer/designer (assigned projects only). The former **ACC** (Accounts)
role is **removed from the defaults** because financial data is Admin-only [CLIENT-DECISION];
the permission system still allows a role to be added later. Full matrix: `docs/PERMISSION_MATRIX.md`.

**Financial data is Admin-only everywhere** [CLIENT-DECISION] — definition in
`BUSINESS_REQUIREMENTS.md` §4.1. Wherever a module below mentions amounts, rates, balances,
commission or finance actions, they exist only for ADM; other roles receive no such fields
from the server.

---

## Part A — Public website modules

| # | Module | Necessity | Summary |
|---|---|---|---|
| P1 | Pages (Home, About Studio, Services, Contact) | Core | Displays content edited in Settings → Website content (R-04); each block has a review status (W-16) |
| P2 | Portfolio listing + Project details | Core | Published projects only; highlighted (major) projects first; slug URLs with 301 on change |
| P3 | Gallery | Recommended | Portfolio images with "show in gallery" on (R-02); separate page PENDING Q-W2 |
| P4 | Enquiry form | Core | Saves to the single enquiry module with status "New – unreviewed" (R-01); honeypot + rate limit + CSRF |
| P5 | WhatsApp click-to-chat | Core | `wa.me` link; number from Settings (Q-W4). Clicks only increment a daily counter — never an enquiry record (C-05) |
| P6 | SEO | Core | Titles/meta, Open Graph, `sitemap.xml` (published items only), `robots.txt` (disallow `/erp/`), schema.org `LocalBusiness` |

Details: `docs/PORTFOLIO_WEBSITE_PLAN.md`.

---

## Part B — ERP modules

### 1. Dashboard — Core
- **Operational widgets (ADM, STF; SITE filtered to own projects/follow-ups — C-10):**
  new website enquiries, follow-ups due/overdue, quotations awaiting response (count only for
  non-ADM), active projects by stage.
- **Financial widgets (ADM only):** Agreed / Billed / Received / Outstanding (C-08 — "Billed"
  shown only for bills-method projects), recent payments, credit held, expenses this month,
  **commission awaiting approval** and **commission outstanding**.

### 2. Enquiry Management — Core (merged with website enquiries, R-01 / C-06)
- **Fields:** number, date, source (Website, WhatsApp, Phone, Walk-in, Instagram, Contractor,
  Referral, Other — lookup), **contractor/referral partner** (when source is Contractor/Referral),
  name, mobile, email, preferred contact (C-09), location/site, project type, approx. area + unit,
  services interested (multi-select, C-09), budget text (optional; non-financial free text),
  message, consent timestamp (website, C-09), assigned to, status, next follow-up.
- **Statuses:** New – unreviewed (website) → New → Contacted → Meeting / site visit → Quotation
  sent → Converted / Lost / Closed. Lost and close reasons from lookups.
- **Pre-project meetings and site visits** are recorded as enquiry **activities** (C-03, R-03).
- **Actions:** activity, follow-up, mark spam/duplicate, convert to Client + Project (copies data
  incl. source and partner), create quotation (ADM — Q-R12).
- **Duplicate check:** warn on same mobile/email as an open enquiry or a client.
- WhatsApp conversations are entered by hand with source WhatsApp (C-05).

### 3. Client Management — Core
- Client type, name, contact person, mobiles, email, address, city, **state and state code**
  (GST place of supply), PIN, GSTIN (ADM only), notes.
- Client page: projects, documents (non-financial categories) for all permitted roles;
  quotations, bills, payments, credit and balance **ADM only**.
- Soft delete; a client with financial records is deactivated, not deleted.

### 4. Project Management — Core
- **Fields:** project code, name, client, project type (lookup; Q-S3), site address, city,
  plot / built-up area + unit, floors, dates, status, team, notes,
  **source type (Direct / Contractor)** and **contractor/referral partner** [CLIENT-DECISION],
  **billing method (agreement / bills — ADM, D-26)**.
- **Statuses:** Proposal (C-02 — replaces "Enquiry stage"), Design, Working drawings,
  Approval/Municipal, Under construction (supervision), Interiors, Completed, On hold, Cancelled.
  List PENDING Q-P1.
- **Site-visit log** (Recommended, Q-P3): after the project exists only (C-03). Chargeable flag
  only if Q-F5 and Q-P3 are confirmed; a chargeable visit can become a bill line (C-17).
- **Tabs:** Overview · Quotations (ADM) · Fees & Bills (ADM) · Payments (ADM) · Expenses (ADM) ·
  Source & Commission (ADM) · Documents · Site visits · Timeline.

### 5. Service and Work Categories — Core [CLIENT-DECISION: Admin manages; demo initially]
- Two-level master: Category → Items. ADM can add, update, reorder and **soft-delete**.
- Each record has a **content origin**: reference (from the sample quotation), **demo**
  (initial demo content — CLIENT-DECISION), or client-confirmed. Demo items carry a badge in the ERP.
- Public display of demo services before the client confirms them: **PENDING Q-S5**
  (setting off by default).
- Item fields: default description, default unit, **default rate (ADM-only, optional)**,
  show-on-website, active, sort order.
- Soft-deleted items stay on existing quotations and portfolio items, are hidden from new
  selection and disappear from the public site.

### 6. Quotation Management — Core (ADM only for pricing and decisions — Q-R12)
- Created from an enquiry (prospect) or a project (C-01).
- Header, scope (from service master, editable), fee lines: area-based, area per category, fixed,
  item-wise, custom [CLIENT-DECISION: area + item-wise; no mandatory fixed pricing].
- Rates editable by ADM only; no rate is pre-filled unless the ADM set a default.
- Optional blocks, off by default: discount, **Apply GST (per revision, only if the studio is
  GST-registered — D-27)**, rounding, payment schedule, validity, terms, exclusions, bank
  details, acceptance block, amount in words.
- **Revisions** R0, R1…; statuses per revision: Draft, Sent, Accepted, Rejected, Expired,
  Cancelled, **Superseded** (C-04 — "Revised" is not a status).
- Send, accept, reject: ADM. Staff scope-only drafting PENDING Q-U4 (off by default).
- PDF/print on the logo + visiting-card letterhead [CLIENT-DECISION]; commission and partner
  data never printed.
- Acceptance → conversion if needed → fee agreement (`docs/WORKFLOWS.md` A.4).

### 7. Design Fees and Billing — Core (ADM only) [CLIENT-DECISION: flexible billing]
- **Per-project billing method** (D-26, PROPOSED): *agreement* (payments are applied to the fee
  agreement or its stages; bills optional) or *bills* (demand notes/tax invoices are issued and
  payments are applied to bills). Studio default in Settings. Replaces the earlier studio-wide
  "billing mode" (C-07, superseded).
- Fee agreement from the accepted revision or entered manually; variations (+/−) with reason.
- **Payment schedule (stages)** — core capability, used per project when wanted [CLIENT-DECISION].
- Bills (bills method): from stages, manual lines, chargeable visits or reimbursable expenses
  (C-16, C-17), or **ad hoc without a fee agreement**. Draft → Issued → Cancelled; Partly paid /
  Paid are calculated.
- **GST per document** (agreement, variation, bill, credit note) — optional, never compulsory
  [CLIENT-DECISION]; treatment PENDING Q-F3.
- Credit notes; write-offs (PENDING Q-F10).

### 8. Payments and Receipts — Core (ADM only) [CLIENT-DECISION: partial, staged, advances]
- Payment: date, client, project, amount (any amount > 0 — **partial payments always accepted**),
  mode, reference, bank, notes. Receipt number and printable receipt.
- **Allocation:** each allocation has exactly one target — a bill (bills method), or a stage or the
  fee agreement (agreement method) (D-29). Unallocated money is project **credit / advance** (C-15).
- Apply credit later; credit transfer between projects ◇ (Q-F11).
- **Reversal** (bounced cheque, wrong entry): linked negative entry; allocations reversed automatically.
- **Refunds** from credit ◇ (C-14, Q-F9).
- Advance before a project exists: PENDING Q-F12.

### 9. Expense Management — Recommended (ADM only; scope PENDING Q-F8)
- Date, category, project (blank = office overhead), paid to, amount, mode, attachment
  (private, financial), notes. Reimbursable flag only if Q-F5 and Q-F8 confirmed (C-16).
- Posted on save; corrections by reversal (D-14).
- Commission payments are **not** recorded as expenses (no double counting).
- Staff expense claims for ADM approval: PENDING Q-U4 (off by default).

### 10. Project Documents and Attachments — Core
- Categories (lookup) carry an **is_financial** flag; financial categories are ADM-only.
- Stored outside the web root; downloaded only through `/erp/files/{id}/download`, which checks
  the owning record's permission (C-11, D-34). Financial downloads are always audited.

### 11. Portfolio and Gallery Management — Core [CLIENT-DECISION: major projects, removal]
- Fields: title, slug, category, city-level location, descriptions, completion year, area (hidden
  by default), services, cover image, gallery images (alt text required), **featured** (home page),
  **highlighted / major** and **display priority**, content review status, SEO fields, consent record.
- **Display sequence** (PROPOSED): highlighted projects by display priority → other projects by
  display priority → completion year (newest first) → title.
- **Publish** requires consent recorded, cover image, alt text on every image, reviewed content.
  Originals stay private; public web versions are created on publish.
- **Unpublish / remove**: reason recorded; public images withdrawn; removed from listings and the
  sitemap; slug returns 410/404.
- Publish/unpublish: ADM (Q-W11 may extend this).

### 12. Website Enquiry Management — merged into module 2 (R-01, C-06)
Kept as a numbered placeholder only. Website submissions appear in module 2 as "New – unreviewed".

### 13. Follow-ups and Reminders — Recommended
- Linked to an enquiry, project, quotation, bill or commission. Due date/time, assignee, note,
  outcome. Follow-ups linked to bills, payments or commission are ADM-only.
- Shown on the dashboard and as a header badge. Optional daily digest (Q-G5) — non-ADM digests
  contain no amounts. SMS/WhatsApp automation not assumed.

### 14. Reports — Core (list PENDING Q-R1)
| Report | Access |
|---|---|
| Enquiry report (source, status, conversion) | ADM, STF |
| Enquiries/projects by source (Direct / Contractor / partner) — counts only | ADM; STF if Q-C5 allows |
| Quotation register — counts and statuses | ADM, STF (no amounts) |
| Quotation register with values | ADM |
| Project status report | ADM, STF |
| Agreed / Billed / Received / Outstanding by client and project (C-08) | ADM |
| Collection register; refunds; credit held | ADM |
| Expense report | ADM |
| **Commission payable / paid / outstanding by partner and project** | ADM |
| **Commission payment register** | ADM |
| Project profitability (fees received − project expenses − commission paid) — Optional | ADM |
All exports are audited; financial exports are ADM-only.

### 15. User and Role Management — Core
- Users, roles (ADM, STF, SITE by default), permission matrix editable by ADM, password reset,
  forced first-login change, lockout. At least one active ADM; ADM cannot be deleted.

### 16. Organization Settings — Core
- Studio profile (name, address, phones, WhatsApp, email, Instagram), letterhead/PDF (logo +
  visiting-card style; "श्री" optional — Q-Q2), numbering formats (D-28), **finance (ADM)**:
  default billing method, **GST profile** (registered yes/no, GSTIN, state, default rates, SAC —
  dormant until Q-F3), "apply GST by default" (off), rounding, lock date, optional-feature switches.
- Website content blocks with review status (R-04, W-16). Masters (lookups, R-07). Backup (ADM).

### 17. Audit Log — Core (cross-cutting)
- Who, when, IP, module, record, action, before/after. Read-only, ADM only. Covers every
  financial and commission action, financial exports and financial document downloads.

### 18. Contractor / Referral Sources and Commission — Core [CLIENT-DECISION]
- **Partner master** (contractor / referral / other): name, firm, mobile, email, address, notes,
  active; bank and tax details and default commission suggestion are ADM-only. STF may select a
  partner on an enquiry/project only if Q-C5 allows.
- **Project commission** (contractor-source projects only): applicable Yes/No, type
  Percentage/Fixed, rate or fixed amount, base (PENDING Q-C3), calculated amount, status
  Draft → Pending approval → Approved / Rejected / Cancelled, remarks, status history.
- **Never automatic, never on direct projects**; payable only after approval.
- **Adjustments** (signed, reason) instead of edits after approval.
- **Commission payments**: number, date, amount (partial allowed), mode, reference, proof file,
  reversal instead of edit. Paid ≤ payable.
- Outstanding = approved amount + adjustments − net paid.
- Never shown on client documents or the website; ADM only; fully audited.
- Details: `docs/DATABASE_DESIGN.md` group I, `docs/WORKFLOWS.md` Part C.

---

## Necessity summary

| Core | Recommended | Optional / confirm first |
|---|---|---|
| Dashboard, Enquiries (incl. website), Clients, Projects, Services, Quotations, Fees & Billing, Payments, Documents, Portfolio, Reports, Users, Settings, Audit, **Contractor & Commission** | Expenses, Follow-ups, Site-visit log, Gallery page | Refunds, write-offs, credit transfer, profitability report, email digests, Marathi UI, client portal |
