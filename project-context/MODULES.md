# Module Specifications (Proposed)

All modules below are **[PROPOSED]**. Each carries a necessity rating to evaluate
against the studio's actual workflow before implementation:

- **Core** – needed for the system to make sense.
- **Recommended** – high value, low risk.
- **Optional** – build only if the client confirms the need.

Role abbreviations (proposed, PENDING Q-U1): **ADM** Admin/Principal · **STF** Office staff ·
**ACC** Accounts · **SITE** Site engineer/designer (read-mostly).

---

## Part A — Public website modules

| # | Module | Necessity | Summary |
|---|---|---|---|
| P1 | Pages (Home, About Studio, Services, Contact) | Core | Content blocks editable from ERP Settings / Website Content |
| P2 | Portfolio listing + Project details | Core | Published projects, filter by category, slug URLs |
| P3 | Gallery | Recommended | Aggregated published images, filter by category; may merge with P2 (Q-W2) |
| P4 | Enquiry form | Core | Saves to ERP `Website Enquiries`; honeypot + rate limit |
| P5 | WhatsApp click-to-chat | Core | `wa.me` link with pre-filled text; number from settings |
| P6 | SEO | Core | Titles/meta per page and project, Open Graph, `sitemap.xml`, `robots.txt`, schema.org `LocalBusiness` |

Details: `docs/PORTFOLIO_WEBSITE_PLAN.md`.

---

## Part B — ERP modules

### 1. Dashboard — Core
- **Purpose:** one-screen view of what needs attention today.
- **Widgets:** new website enquiries; follow-ups due today/overdue; quotations
  awaiting response; active projects by stage; fees billed vs received (month / FY);
  recent payments; outstanding balance; expenses this month.
- **Access:** all roles; finance widgets only for ADM/ACC.

### 2. Enquiry Management — Core
- **Fields:** date, source (Website, WhatsApp, Phone, Walk-in, Referral, Instagram, Other —
  configurable), name, mobile, email, location/site, project type, approx. area + unit,
  services interested in, budget (optional), message, assigned to, status, next follow-up date.
- **Statuses:** New → Contacted → Site visit / meeting → Quotation sent → Converted / Lost / Closed.
  Lost reason captured.
- **Actions:** add notes, schedule follow-up, convert to Client + Project (copies data, keeps link).
- **Duplicate check:** warn on same mobile/email.

### 3. Client Management — Core
- Client type (Individual / Company / Trust / Institution), name, contact person,
  mobiles, email, address, city, PIN, GSTIN (optional, PENDING Q-F3), notes.
- Client page shows projects, quotations, bills, payments, balance, documents.
- Soft delete; cannot delete a client with financial records.

### 4. Project Management — Core
- **Fields:** project code (auto, configurable format), name, client, project type
  (Bungalow, Residential, Commercial, Interior, Temple, … — configurable, Q-S1),
  site address, city, plot area / built-up area + unit, floors, start date,
  expected completion, status, assigned team, notes.
- **Statuses (proposed):** Enquiry stage, Design, Working drawings, Approval/Municipal,
  Under construction (supervision), Interiors, Completed, On hold, Cancelled.
- **Scope:** services included (from accepted quotation).
- **Site visits** (Recommended, Q-P3): date, stage (Centerline, Footing, PCC, Wall,
  7′ level, Slab, Plaster, Tiles, Interior, Ceiling, Electrical, Furniture, Material
  selection, Colour selection, Surprise — seeded from sample, editable), visited by,
  observations, photos, chargeable flag.
- **Tabs:** Overview · Quotations · Fees & Bills · Payments · Expenses · Documents · Site visits · Timeline/notes.

### 5. Service and Work Categories — Core
- Two-level master: **Category** (e.g. Architectural drawings, Working drawings,
  3D work, Interior design, Interior 3D, Site visits) → **Items** (e.g. Ground floor
  plan, Sections, Municipal drawing, Ceiling layout …).
- Seed list taken from the sample quotation, marked "reference" until the client confirms (Q-S1).
- Each item: default description, default unit (lump sum / sq.ft / sq.m / per visit / per room / per sheet),
  optional default rate, show-on-website flag, active flag, sort order.

### 6. Quotation Management — Core
- Created from an enquiry or project. Header: ref no., date, client, project,
  site, area + unit, subject line, intro text.
- **Scope section:** pick categories/items; edit text per quotation; ordering.
- **Fee section — calculation methods:**
  1. *Area-based*: area × rate (per sq.ft/sq.m), optionally per category.
  2. *Fixed fee*: lump sum.
  3. *Item-wise*: qty × rate per line.
  4. *Custom charges*: free lines (e.g. extra visits, travel) — enabled per quotation.
  Combinations allowed (e.g. area-based design fee + item-wise extras).
- Optional, **off by default** until approved: discount, tax lines (GST %),
  payment schedule (stage-wise % or amounts), validity days, terms & conditions,
  exclusions, bank details.
- **Revisions:** R0, R1, R2…; each revision is a frozen snapshot (lines, totals,
  text, rate). Compare revisions.
- **Status:** Draft, Sent, Revised, Accepted, Rejected, Expired, Cancelled. Who/when recorded.
- **Output:** HTML print view and PDF on letterhead (logo, address, signature block
  "Ar. Ajit Kumbhar (Principal Architect)" — configurable). Amount in words.
- Accepting a quotation can generate the project fee schedule (module 7).
- Full rationale: `docs/QUOTATION_ANALYSIS.md`.

### 7. Design Fees and Billing — Core (model PENDING Q-F1..F5)
- Project fee agreement = total agreed fee (from accepted quotation revision).
- Fee schedule / milestones (e.g. advance, on plans, on working drawings…) — only if client uses stages.
- **Bills / invoices** (or "fee demand notes" if not GST-registered — Q-F3): number,
  date, lines, tax (if enabled), total. Status: Draft, Issued, Partly paid, Paid, Cancelled.
- Issued bills are never edited; corrections via cancellation + re-issue or credit note.

### 8. Payments and Receipts — Core
- Payment: date, client, project, against bill(s) or on account/advance, amount,
  mode (Cash, UPI, Bank transfer, Cheque — configurable), reference/UTR/cheque no., bank, notes.
- Receipt number auto, printable/PDF receipt.
- Allocation of a payment across bills.
- Reversal (bounced cheque, wrong entry) creates a negative reversal entry linked to the original.
- Client and project balance = billed − received (or agreed fee − received if no billing; Q-F1).

### 9. Expense Management — Recommended (scope PENDING Q-F8)
- Date, category (Travel, Printing/plotting, Software, Office, Site, Other — configurable),
  project (optional — office overhead when blank), paid to, amount, mode, bill attachment, notes.
- Reimbursable-to-client flag (only if confirmed).
- Edits after a lock date require reversal.

### 10. Project Documents and Attachments — Core
- Upload drawings (PDF, DWG?, images), 3D renders, municipal approvals, agreements.
- Fields: project, category (Plans, Working drawings, Municipal, 3D, Interior, Site photos,
  Agreement, Other), title, version, date, uploaded by, visibility (internal only).
- Stored **outside web root**; downloaded only via authorized PHP script.
- Allowed types and max size configurable (Q-D1 for DWG/large files).

### 11. Portfolio and Gallery Management — Core
- Portfolio project: title, slug, category, location (city level by default), short and
  long description, completion year, area (optional, hide by default), services shown,
  cover image, gallery images (ordered, captions, alt text), featured flag,
  published/unpublished, SEO title/description, link to internal project (optional).
- Image processing on upload: resize to web sizes (e.g. 400/800/1600 px), WebP + JPEG,
  strip EXIF/GPS.
- Client-consent checkbox before publishing ("Client permission obtained") – PROPOSED, Q-W5.
- Preview before publish.

### 12. Website Enquiry Management — Core
- Inbox of website form/WhatsApp-click submissions, separate from manually created enquiries
  until reviewed (mark spam, mark duplicate, convert to Enquiry).
- Could be merged into module 2 with source = Website (recommended to reduce duplication; Q-G4).

### 13. Follow-ups and Reminders — Recommended
- Follow-ups on enquiries, quotations, payments due, projects.
- Due date/time, assigned to, note, outcome, done flag.
- Shown on dashboard and as a header badge. Optional daily email digest via cron (Q-G5).
- SMS/WhatsApp automation **not** assumed.

### 14. Reports — Core (list PENDING Q-R1)
Proposed starting set, each filterable by date range and exportable to CSV/print:
- Enquiry report (by source, status, conversion rate).
- Quotation register (status, value).
- Project status report.
- Fees billed vs received, outstanding by client/project.
- Payment collection register (by mode).
- Expense report (by category, by project).
- Project profitability (fees received − project expenses) – Optional.

### 15. User and Role Management — Core
- Users: name, username, email, mobile, role, active, last login.
- Roles with permission matrix (module × view/create/edit/delete/approve/export).
- Default roles: ADM, STF, ACC, SITE (PENDING Q-U1). ADM cannot be deleted; at least one active ADM.
- Password reset by email; force change on first login; lockout after repeated failures.

### 16. Organization Settings — Core
- Studio profile: name, tagline, address, phone, WhatsApp, email, social links, logo variants.
- Letterhead/PDF settings: header, footer, signature name/designation, signature image (optional).
- Numbering formats: enquiry, project, quotation (e.g. `{seq}/{yyyy}` like sample), bill, receipt; FY start (April?).
- Tax settings (off by default), default terms text, default validity (blank).
- Masters: project types, enquiry sources, payment modes, expense categories, area units.
- Website content: home hero, about text, services text, contact block, SEO defaults.
- Backup: download DB backup (ADM only).

### 17. Audit Log — Core (cross-cutting)
- Who, when, IP, module, record, action (create/update/delete/status change/login/export),
  before/after summary. Read-only screen for ADM.

---

## Necessity summary

| Core | Recommended | Optional / confirm first |
|---|---|---|
| Dashboard, Enquiries, Clients, Projects, Services, Quotations, Fees & Billing, Payments, Documents, Portfolio, Website enquiries (merged), Reports, Users, Settings, Audit | Expenses, Follow-ups, Site-visit log, Gallery page | Profitability report, email digests, Marathi UI, client portal, contractor/vendor tracking |
