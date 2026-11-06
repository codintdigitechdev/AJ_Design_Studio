# Module Specifications

All module designs are **PROPOSED** unless a line carries another tag (`CLAUDE.md` §3).
Client decisions that a module implements are marked **CLIENT-DECISION**.
**Status: APPROVED 2026-11-06 (Stage 1 gate).** Items marked PROPOSED in this document are approved as written; anything still marked PENDING waits for the named answer.

Necessity ratings:
- **Core** – needed for the system to make sense.
- **Recommended** – high value, low risk.
- **Optional** – build only if the client confirms the need.

Default roles (PROPOSED, D-30; only the Admin uses the ERP for now — CLIENT-DECISION CD-80): **ADM** Admin/Principal · **STF** Office
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
| P3 | Gallery | Merged into P2 [CLIENT-DECISION CD-44] | No separate Gallery page; each project page has its own gallery |
| P4 | Enquiry form | Core | Saves to the separate **Website Enquiries** inbox (module 12, CD-31); built-in CAPTCHA (CD-48) + honeypot + rate limit + CSRF; notification email to the studio |
| P5 | WhatsApp click-to-chat | Core | `wa.me` link; number 8806956877 (CD-46). Clicks only increment a daily counter — never an enquiry record (C-05) |
| P6 | SEO | Core | English + Marathi pages with hreflang (CD-50); titles/meta, Open Graph, `sitemap.xml` (published items only), `robots.txt` (disallow `/erp/`), schema.org `LocalBusiness` |

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
- High-priority follow-ups are also emailed to the Admin (CD-32).

### 2. Enquiry Management — Core (manual enquiries; website submissions arrive through module 12 — CD-31)
- **Fields:** number, date, source (Website, WhatsApp, Phone, Walk-in, Instagram, Contractor,
  Referral, Other — lookup), **contractor/referral partner** (when source is Contractor/Referral),
  name, mobile, email, preferred contact (C-09), location/site, project type, approx. area + unit,
  services interested (multi-select, C-09), budget text (optional; non-financial free text),
  message, consent timestamp (website, C-09), assigned to, status, next follow-up.
- **Statuses:** New → Contacted → Meeting / site visit → Quotation
  sent → Converted / Lost / Closed. Lost and close reasons from lookups.
- **Pre-project meetings and site visits** are recorded as enquiry **activities** (C-03, R-03, CD-78).
- **Advance at enquiry stage** (ADM): a payment may be recorded against the enquiry and moves to the project on conversion (CD-69).
- **Date-wise delete** (ADM): Lost/Closed enquiries can be permanently deleted for a chosen date range (CD-34).
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
- **Fields:** project code, name, client, project type (Architectural, Civil, Interior, Landscape — CD-41), site address, city,
  plot / built-up area + unit, floors, dates, status, team, notes,
  **source type (Direct / Contractor / Referral — CD-71)** and **contractor/referral partner** [CLIENT-DECISION],
  **billing method (agreement / bills — ADM, D-26)**.
- **Statuses** [CLIENT-DECISION CD-76]: Planned, OnGoing, OnHold, Completed, HandOver, Cancelled.
  (Replaces the earlier proposal incl. "Proposal" — C-02 superseded.)
- **Site-visit log** [CLIENT-DECISION CD-77]: logged without limits, after the project exists (C-03);
  usable on mobile (CD-81). Chargeable flag (ADM) — extra charges are billed separately (CD-62, C-17).
- **Tabs:** Overview · Quotations (ADM) · Fees & Bills (ADM) · Payments (ADM) · Expenses (ADM) ·
  Source & Commission (ADM) · Documents · Site visits · Timeline.

### 5. Service and Work Categories — Core [CLIENT-DECISION: Admin manages; demo initially]
- Two-level master: Category → Items. ADM can add, update, reorder and **soft-delete**.
- Each record has a **content origin**: reference (from the sample quotation), **demo**
  (initial demo content — CLIENT-DECISION), or client-confirmed. Demo items carry a badge in the ERP.
- Demo services are **never shown on the public site** [CLIENT-DECISION CD-42].
- Final public list = the quotation categories (CD-94): architectural drawings, working & municipal
  drawings, exterior 3D, interior design, interior 3D, site supervision visits, material & colour
  selection — marked client-confirmed; descriptions drafted by CodInt for client review.
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
- Send, accept, reject: ADM. No staff drafting (CD-83). No separate approval step (CD-93). Discount at most 5% (CD-61).
- Quotation number `AJDS/Q/{fy}/{seq3}` (CD-52); shared by download + WhatsApp, no ERP email (CD-57).
- PDF/print on the logo + visiting-card letterhead with "श्री", no QR (CD-13, CD-53), acceptance block
  (CD-55), all standard term sections (CD-56), in English or Marathi (CD-50); commission and partner
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
  [CLIENT-DECISION]; the studio is not GST-registered today, so GST stays off (CD-60).
- Credit notes; write-offs (ADM only — CD-67).

### 8. Payments and Receipts — Core (ADM only) [CLIENT-DECISION: partial, staged, advances]
- Payment: date, client, project, amount (any amount > 0 — **partial payments always accepted**),
  mode (Online, Cash, UPI — CD-64), reference, bank, notes. Receipt number and printable receipt.
- **Allocation:** each allocation has exactly one target — a bill (bills method), or a stage or the
  fee agreement (agreement method) (D-29). Unallocated money is project **credit / advance** (C-15).
- Apply credit later. **No credit transfer between projects** (CD-68).
- **Reversal** (bounced cheque, wrong entry): linked negative entry; allocations reversed automatically.
- **Refunds** from credit, with an optional percentage deduction (C-14, CD-66).
- Advances before a project exists are recorded against the enquiry and move to the project on conversion (CD-69).

### 9. Expense Management — Recommended (ADM only; rent, travel and similar — CD-65)
- Date, category, project (blank = office overhead), paid to, amount, mode, attachment
  (private, financial), notes. Client reimbursement not requested (flag off — C-16).
- Posted on save; corrections by reversal (D-14).
- Commission payments are **not** recorded as expenses (no double counting).
- No staff expense claims (CD-83).

### 10. Project Documents and Attachments — Core
- Categories (lookup) carry an **is_financial** flag; financial categories are ADM-only.
- Stored outside the web root; downloaded only through `/erp/files/{id}/download`, which checks
  the owning record's permission (C-11, D-34). Financial downloads are always audited.
- File types kept minimal — PDF, JPG, PNG, WebP — with small size limits (CD-79).

### 11. Portfolio and Gallery Management — Core [CLIENT-DECISION: major projects, removal]
- Fields: title, slug, category, city-level location, descriptions, completion year, area (hidden
  by default), services, cover image, gallery images (alt text required; from client originals — CD-43),
  Marathi title and descriptions (CD-50), client name shown only with permission (CD-47), **featured** (home page),
  **highlighted / major** and **display priority**, content review status, SEO fields, consent record.
- **Display sequence** (PROPOSED): highlighted projects by display priority → other projects by
  display priority → completion year (newest first) → title.
- **Publish** requires consent recorded, cover image, alt text on every image, reviewed content.
  Originals stay private; public web versions are created on publish.
- **Unpublish / remove**: reason recorded; public images withdrawn; removed from listings and the
  sitemap; slug returns 410/404.
- Publish/unpublish: ADM. The gallery is part of each project page (CD-44).

### 12. Website Enquiries — Core [CLIENT-DECISION CD-31: kept distinct]
- Separate inbox of website form submissions (name, mobile, email, city, project type, services,
  area, message, preferred contact, consent, language).
- Statuses: new, reviewed, spam, duplicate, converted. **Convert to enquiry** copies the data and keeps the link.
- Notification email to the studio for each submission (CD-48). Date-wise delete by ADM (CD-34).
- WhatsApp clicks are counted only, never stored as enquiries (C-05).

### 13. Follow-ups and Reminders — Recommended
- Linked to an enquiry, project, quotation, bill or commission. Due date/time, assignee, note,
  outcome. Follow-ups linked to bills, payments or commission are ADM-only.
- Each follow-up has a priority; **high-priority** items are emailed to the Admin when due, all items
  show on the dashboard and header badge (CD-32). Emails to non-ADM users contain no amounts.
  SMS/WhatsApp automation not assumed.

### 14. Reports — Core (all listed reports — CD-84)
| Report | Access |
|---|---|
| Enquiry report (source, status, conversion) | ADM, STF |
| Enquiries/projects by source (Direct / Contractor / Referral / partner) — counts | ADM (staff excluded — CD-74) |
| Quotation register — counts and statuses | ADM, STF (no amounts) |
| Quotation register with values | ADM |
| Project status report | ADM, STF |
| Agreed / Billed / Received / Outstanding by client and project (C-08) | ADM |
| Collection register; refunds; credit held | ADM |
| Expense report | ADM |
| **Commission payable / paid / outstanding by partner and project** | ADM |
| **Commission payment register** | ADM |
| Project profitability (fees received − project expenses − commission paid) | ADM |
All exports are audited; financial exports are ADM-only.

### 15. User and Role Management — Core
- Users, roles (ADM, STF, SITE by default; only ADM in use now — CD-80; no two-step login — CD-82), permission matrix editable by ADM, password reset,
  forced first-login change, lockout. At least one active ADM; ADM cannot be deleted.

### 16. Organization Settings — Core
- Studio profile (name, address, phones, WhatsApp, email, Instagram), letterhead/PDF (logo +
  visiting-card style, "श्री" kept, no QR — CD-53; English and Marathi templates — CD-50), numbering formats (D-28), **finance (ADM)**:
  default billing method, **GST profile** (registered yes/no, GSTIN, state, default rates, SAC —
  not registered today — CD-60), "apply GST by default" (off), rounding, lock date, optional-feature switches.
- Website content blocks in English and Marathi, with review status (R-04, W-16, CD-50). Masters (lookups, R-07). Backup (ADM).

### 17. Audit Log — Core (cross-cutting)
- Who, when, IP, module, record, action, before/after. Read-only, ADM only. Covers every
  financial and commission action, financial exports and financial document downloads.

### 18. Contractor / Referral Sources and Commission — Core [CLIENT-DECISION]
- **Partner master** (contractor / referral / other): name, firm, mobile, email, address, notes,
  active; bank and tax details and default commission suggestion are ADM-only. Staff see no partner
  or source data (CD-74). Records kept until removed (CD-75).
- **Project commission** (Contractor- or Referral-source projects; one partner per project — CD-70, CD-71): applicable Yes/No, type
  Percentage/Fixed, rate or fixed amount, base = final agreed fee excl. GST incl. variations (CD-72), calculated amount, status
  Draft → Pending approval → Approved / Rejected / Cancelled, remarks, status history.
- **Never automatic, never on direct projects**; payable only after approval **and** project completion
  (Completed/HandOver — CD-72). Fee variations change the commission (automatic adjustments).
- GST may apply on commission payments (CD-73); TDS field kept but off (CD-92). On cancellation or
  non-payment the Admin decides (CD-75).
- **Adjustments** (signed, reason) instead of edits after approval.
- **Commission payments**: number, date, amount (partial allowed), mode, reference, proof file,
  reversal instead of edit. Paid ≤ payable.
- Outstanding = approved amount + adjustments − net paid.
- Never shown on client documents or the website; ADM only; fully audited.
- Details: `docs/DATABASE_DESIGN.md` group I, `docs/WORKFLOWS.md` Part C.

---

## Necessity summary

| Core | Recommended | Not included |
|---|---|---|
| Dashboard, Website Enquiries, Enquiries, Clients, Projects, Site-visit log, Services, Quotations, Fees & Billing, Payments (incl. refunds, write-offs), Documents, Portfolio, Reports (all), Users, Settings, Audit, **Contractor & Commission**, Marathi website and documents | Expenses, Follow-ups (priority emails) | Separate Gallery page (CD-44), credit transfer (CD-68), client portal (CD-33), staff claims/drafting (CD-83), two-step login (CD-82), Marathi ERP screens |
