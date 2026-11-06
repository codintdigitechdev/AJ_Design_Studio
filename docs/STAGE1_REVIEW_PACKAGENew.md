# AJ Design Studio — Stage 1 Review Package (Structured)

| | |
|---|---|
| Project | AJ Design Studio — Public Portfolio Website + Private ERP |
| Developer | CodInt Digitech |
| Client | AJ Design Studio · Principal Architect: Ar. Ajit Kumbhar |
| Prepared | 2026-11-06 |
| Status recorded in project files | Stage 0 – Documentation & requirements, awaiting approval (`CLAUDE.md`; `DEVELOPMENT_ROADMAP.md` §5) |
| Sources | `CLAUDE.md`, `project-context/*.md` (7 files), and `docs/*.md` (6 files) where cited |

## How to read this document

- This is a **structured synthesis** of the existing project files. It adds no new requirements.
  Each item cites its source file and section. If this document and a source file disagree,
  the source file is authoritative.
- Status markers:
  - **CONFIRMED** – the item is stated in a supplied reference (logo, sample quotation,
    public Instagram profile) or in the developer brief.
  - **CONFIRMED (brief)** – the developer brief requires it, but the client has not yet
    checked it against how the studio actually works (`BUSINESS_REQUIREMENTS.md` header).
  - **PROPOSED** – a developer recommendation. It is not yet approved.
  - **ASSUMPTION** – a working assumption that still has to be checked.
  - **PENDING APPROVAL** – not decided yet. Needs a client or developer decision. The
    question ID (`Q-…`) refers to `docs/CLIENT_QUESTIONS.md`.
- Every item marked PROPOSED or ASSUMPTION is also **PENDING APPROVAL** until it is recorded in
  the decision log (`DEVELOPMENT_ROADMAP.md` §5). So far, the decision log records **no
  approvals**.
- This document contains no application code and no SQL.

---

## 1. Project overview and objectives

### 1.1 Vision — CONFIRMED (`CLAUDE.md` §1)
The developer will build one integrated web application on **one hosting account and one
domain**. It has two independent user experiences:

| Area | Audience | URL |
|---|---|---|
| A. Public portfolio website (new — the client has **no existing website**) | Everyone, no login | `https://<domain>/` |
| B. Private ERP | Authorized organization users only | `https://<domain>/erp/`, `/erp/login`, `/erp/dashboard` |

- Public visitors must never reach ERP data, files or configuration.
- The ERP is also the content-management back office for the website.
- Domain name: **PENDING APPROVAL** (Q-H1).

### 1.2 Organization facts — CONFIRMED (sample quotation letterhead, public Instagram profile; `PROJECT_OVERVIEW.md` §3.1)

| Item | Value |
|---|---|
| Name | AJ Design Studio |
| Profession | Architect, Interior Designer |
| Address | Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan |
| Area line | Patan, Karad, Satara |
| Phone | 8806956877 |
| Email | ar.ajitkumbhar16@gmail.com |
| Instagram | @ar.ajkumbhar |

Two things about these details still need a decision:
- Whether these details may be published on the website, and whether this phone number is
  also the WhatsApp number: **PENDING APPROVAL** (Q-W3, Q-W4).
- Contact details, project names and client names must not be published until approved
  (`CLAUDE.md` §6).

### 1.3 Stakeholders (`PROJECT_OVERVIEW.md` §2)

| Role | Who | Status |
|---|---|---|
| Client | AJ Design Studio | CONFIRMED |
| Principal Architect | Ar. Ajit Kumbhar | CONFIRMED |
| Decision authority | Ar. Ajit Kumbhar | ASSUMPTION |
| Developer | CodInt Digitech | CONFIRMED |
| Other ERP users | Unknown | PENDING APPROVAL (Q-U1) |
| Website visitors | Prospective clients, public | CONFIRMED |

### 1.4 Objectives (`PROJECT_OVERVIEW.md` §4)

| # | Goal | Status |
|---|---|---|
| G1 | Premium online presence with a portfolio | CONFIRMED |
| G2 | Capture enquiries from the website (form + WhatsApp) | CONFIRMED |
| G3 | Manage enquiries, clients and projects in one place | CONFIRMED (brief) |
| G4 | Consistent, professional quotations with revisions/approval | CONFIRMED (brief) |
| G5 | Track fees billed, payments received and expenses per project | PROPOSED |
| G6 | Store project documents privately | PROPOSED |
| G7 | Studio can update the website without a developer | CONFIRMED (brief) |

### 1.5 Constraints (`PROJECT_OVERVIEW.md` §5; `CLAUDE.md` §8)
- **CONFIRMED:**
  - Core PHP, MySQL/MariaDB, PDO prepared statements, Bootstrap 5, HTML5/CSS3/vanilla JS,
    and AJAX where useful.
  - XAMPP for development and cPanel for production.
  - No heavy frameworks.
- **PROPOSED:** PHP 8.1+.
- **PENDING APPROVAL:** hosting provider and plan (Q-H2), budget and timeline (none supplied).

### 1.6 Explicitly not assumed (`BUSINESS_REQUIREMENTS.md` §7; `PROJECT_SCOPE.md` §3)
The following are **out of scope** unless the client requests them and approves a change:
- construction execution or contracting, material procurement or resale, turnkey interiors
- vendor or contractor payments, payroll, inventory
- GST filing, accounting ledger, Tally integration
- online payment gateway, client portal, mobile apps
- SMS or WhatsApp Business API automation
- multi-branch, multi-currency
- content writing and photography
- domain or hosting purchase
- historical data migration (Q-G10)

---

## 2. User roles and permissions

### 2.1 Proposed roles — PENDING APPROVAL (Q-U1) (`MODULES.md` header, §15)

| Code | Role | Proposed scope |
|---|---|---|
| ADM | Admin / Principal | Full access; the only role for financial reversals, user/role changes, settings and backups by default (`SECURITY_RULES.md` §8) |
| STF | Office staff | Day-to-day operations (detailed rights not yet defined) |
| ACC | Accounts | Finance; can see the finance widgets on the dashboard |
| SITE | Site engineer / designer | Mostly read-only; may see only the projects assigned to them (record-level rule PENDING APPROVAL) |

### 2.2 Permission model — PROPOSED (`MODULES.md` §15; `SECURITY_RULES.md` §1, §8)
- **Permission matrix:** each module × view / create / edit / delete / approve / export.
- **Checks on every request:** every ERP request goes through one entry point that checks the
  session is valid, the user is active, and the user has permission for that module and
  action. The checks run on the server, not just by hiding menu items.
- **Admin safeguards:** the ADM role cannot be deleted, and there must always be at least one
  active ADM.
- **Dashboard finance widgets:** visible only to ADM and ACC (`MODULES.md` §1).

### 2.3 Not yet defined — PENDING APPROVAL
- **The full role × module permission matrix.** This is a Stage 1 deliverable and **has not
  been produced yet**.
- Who uses the ERP, what each person may see or do, and whether staff may see fees and
  payments (Q-U1).
- Who can approve or send a quotation (Q-Q8).
- Whether discounts need approval (Q-F4).
- ERP use on mobile at site (Q-U2).
- Two-factor login (TOTP) for Admin (Q-U3).
- Number of users. Working assumption: 1–5 (ASSUMPTION A1).

---

## 3. Application modules and features

All modules are **PROPOSED** (`MODULES.md`). Each module has a necessity rating:
- **Core** – needed for the system to make sense.
- **Recommended** – high value, low risk.
- **Optional** – build only if the client confirms the need.

The final module list is **PENDING APPROVAL** (Stage 1 gate).

### 3.1 Public website modules (`MODULES.md` Part A; `docs/PORTFOLIO_WEBSITE_PLAN.md`)

| # | Module | Necessity | Key features |
|---|---|---|---|
| P1 | Pages: Home, About Studio, Services, Contact | Core | Content blocks editable from the ERP |
| P2 | Portfolio listing + Project details | Core | Published projects, category filter, readable page addresses (`/portfolio/{slug}`) |
| P3 | Gallery | Recommended | Combined published images with a category filter. Separate page or merged with Portfolio: PENDING APPROVAL (Q-W2) |
| P4 | Enquiry form | Core | Saves into the ERP; hidden spam-trap field + rate limit + CSRF protection |
| P5 | WhatsApp click-to-chat | Core | `wa.me` link with a pre-filled message; number taken from Settings (number PENDING APPROVAL, Q-W4) |
| P6 | SEO | Core | Titles and descriptions per page/project, social-sharing previews (Open Graph), `sitemap.xml`, `robots.txt`, business information for search engines (schema.org `LocalBusiness`) |

**Proposed pages** (`PORTFOLIO_WEBSITE_PLAN.md` §2):

| Page | URL |
|---|---|
| Home | `/` |
| About Studio | `/about` |
| Services | `/services` |
| Portfolio | `/portfolio` |
| Project details | `/portfolio/{slug}` |
| Gallery | `/gallery` |
| Contact | `/contact` |
| Enquiry | `/enquiry` |
| Enquiry thank-you | `/enquiry/thank-you` |
| Privacy notice | `/privacy` |
| Page not found | branded 404 page |
| System files | `/sitemap.xml`, `/robots.txt` |

**Content rule:** no invented projects, services, statistics, awards or testimonials.

### 3.2 ERP modules (`MODULES.md` Part B)

| # | Module | Necessity | Key features (proposed) |
|---|---|---|---|
| 1 | Dashboard | Core | New website enquiries, follow-ups due or overdue, quotations awaiting response, active projects by stage, fees billed vs received, recent payments, outstanding balance, expenses this month |
| 2 | Enquiry management | Core | Source, contact and site details, project type, approximate area + unit, services wanted, budget, assignee, status, next follow-up, reason if lost, warning on duplicate mobile/email, convert to Client + Project |
| 3 | Client management | Core | Client type, contacts, address, optional GSTIN (Q-F3), client page showing projects, quotations, bills, payments, balance and documents. Soft delete only; a client with financial records cannot be deleted |
| 4 | Project management | Core | Automatic project code, project type, site, plot/built-up area + unit, floors, dates, status, team. Tabs: Overview, Quotations, Fees & Bills, Payments, Expenses, Documents, Site visits, Timeline |
| 4a | Site-visit log | Recommended — PENDING APPROVAL (Q-P3) | Date, stage (stage list seeded from the sample and editable), visited by, observations, photos, chargeable flag |
| 5 | Service & work categories | Core | Two levels: Category → Items, with default description, unit and rate, a show-on-website flag and sort order. Seed list from the sample is marked "reference" until confirmed (Q-S1) |
| 6 | Quotation management | Core | Quotation builder, calculation methods (see §8), revisions R0/R1/…, statuses, HTML print view and PDF on letterhead, amount in words |
| 7 | Design fees & billing | Core — billing model PENDING APPROVAL (Q-F1..F5) | Fee agreement taken from the accepted revision, fee schedule/milestones, bills or "fee demand notes", bill statuses |
| 8 | Payments & receipts | Core | Payment modes, reference numbers, payment split across several bills, automatic receipt number with PDF, reversals |
| 9 | Expense management | Recommended — scope PENDING APPROVAL (Q-F8) | Category, optional project, payee, amount, payment mode, attached bill, "reimbursable by client" flag (only if confirmed), lock date |
| 10 | Project documents | Core | Categories, version, uploaded by, internal-only visibility, stored outside the website's public folder, downloaded only after a permission check |
| 11 | Portfolio & gallery management | Core | Project title, slug, category, city-level location, descriptions, images with captions and alt text, featured flag, publish switch, SEO fields, automatic image resizing (400/800/1600 px, WebP + JPEG, location data removed), preview before publishing. Client-consent checkbox PENDING APPROVAL (Q-W5) |
| 12 | Website enquiry management | Core | Inbox of website submissions: mark as spam/duplicate, convert to enquiry. Proposed to merge into module 2 — PENDING APPROVAL (Q-G4) |
| 13 | Follow-ups & reminders | Recommended | Linked to enquiries, quotations, payments or projects; due date, assignee, outcome. Shown on the dashboard and as a header badge. Optional daily email digest (Q-G5). SMS/WhatsApp automation is not assumed |
| 14 | Reports | Core — list PENDING APPROVAL (Q-R1) | See §8 |
| 15 | User & role management | Core | Users, roles, permission matrix, password reset by email, password change forced on first login, lockout after repeated failures |
| 16 | Organization settings | Core | Studio profile, letterhead/PDF settings, numbering formats, tax settings (off by default), default terms, master lists, website content, database backup download (ADM only) |
| 17 | Audit log | Core (applies to all modules) | Who, when, IP address, module, record, action, summary of before/after. Read-only screen for ADM |

### 3.3 Necessity summary (`MODULES.md`)

| Core | Recommended | Optional / confirm first |
|---|---|---|
| Dashboard, Enquiries, Clients, Projects, Services, Quotations, Fees & Billing, Payments, Documents, Portfolio, Website enquiries (merged), Reports, Users, Settings, Audit | Expenses, Follow-ups, Site-visit log, Gallery page | Profitability report, email digests, Marathi interface, client portal, contractor/vendor tracking |

---

## 4. Business rules and workflows

### 4.1 Core business flow — PROPOSED; real sequence PENDING APPROVAL (Q-G2) (`BUSINESS_REQUIREMENTS.md` §2)
```
Website form / WhatsApp / phone / walk-in / referral
  → ENQUIRY → follow-ups → (lost / dropped)
  → converted → CLIENT → PROJECT (site, type, area)
  → QUOTATION (draft → revision n → sent → accepted/rejected)
  → accepted → FEE SCHEDULE / BILLS → PAYMENTS & RECEIPTS
      ├── project stages & site visits
      ├── documents (drawings, 3D, municipal)
      ├── expenses
      └── (optional) publish to PORTFOLIO
```
Still to be confirmed: whether projects are opened before the quotation, and when something
counts as a "project" (Q-G2).

### 4.2 Status workflows — PROPOSED

| Record | Statuses | Source / pending |
|---|---|---|
| Enquiry | New → Contacted → Site visit / meeting → Quotation sent → Converted / Lost / Closed | `MODULES.md` §2 |
| Project | Enquiry stage, Design, Working drawings, Approval/Municipal, Under construction (supervision), Interiors, Completed, On hold, Cancelled | `MODULES.md` §4; PENDING APPROVAL (Q-P1) |
| Quotation | Draft, Sent, Revised, Accepted, Rejected, Expired, Cancelled | `MODULES.md` §6; PENDING APPROVAL (Q-Q8) |
| Bill | Draft, Issued, Partly paid, Paid, Cancelled | `MODULES.md` §7; billing model PENDING APPROVAL (Q-F1) |

### 4.3 Quotation rules (`CLAUDE.md` §7; `BUSINESS_REQUIREMENTS.md` §5)

| ID | Rule | Status |
|---|---|---|
| — | The sample quotation (`Ref 1/2025`, 1100 sq.ft × ₹100 = ₹1,10,000) is a **dummy** | CONFIRMED |
| Q-R03 | Never hardcode ₹100/sq.ft, the area or the total | CONFIRMED |
| Q-R04 | GST/tax, discounts, payment schedule, validity and terms are configurable and **off/blank by default** until approved | CONFIRMED (brief) |
| — | Do not assume extra-visit charges or revision limits | CONFIRMED |
| Q-R01 | Calculation methods: area-based, fixed fee, item-wise, custom charges | PROPOSED |
| Q-R02 | Rate, area unit and rounding entered per quotation, with optional defaults in Settings | PROPOSED |
| Q-R05 | Scope built from service categories, with sub-items editable per quotation | PROPOSED |
| Q-R06 | Any change after "Sent" creates a new revision; older revisions become read-only | PROPOSED |
| Q-R07 | Statuses as in §4.2 | PROPOSED — PENDING APPROVAL (Q-Q8) |
| Q-R08 | Reference number format configurable (sample: `1/2025`) | PROPOSED — PENDING APPROVAL (Q-Q1) |
| Q-R09 | Amount in words on the PDF (Indian system) | PROPOSED — PENDING APPROVAL (Q-Q6) |
| — | Accepting a revision makes it the project's fee agreement; a payment schedule, if used, generates billing milestones | PROPOSED (`QUOTATION_ANALYSIS.md` §5) |
| — | Required capabilities: PDF + print, revision history, approval status | CONFIRMED (`CLAUDE.md` §7) |

### 4.4 Financial integrity rules — CONFIRMED in principle (`CLAUDE.md` §9; `DATABASE_RULES.md` §5–6)
- Financial transactions are never silently overwritten or deleted. Corrections are made by
  adding a reversal entry that references the original, plus a new correct entry, with a
  mandatory reason.
- Drafts can be edited. Once a document is issued or posted it cannot be changed, except for
  its status.
- Cancelled documents keep their number, and numbers are never reused.
- Optional "lock date": nothing dated on or before it can be added or reversed without ADM.
  PROPOSED.
- Ordinary master records are soft-deleted (kept but hidden). A record that has financial
  history is made inactive instead of deleted.

### 4.5 Other rules
- **Enquiry conversion** copies the data into a new Client + Project and keeps the link back
  to the enquiry. PROPOSED (`MODULES.md` §2).
- **Publishing to the portfolio** requires client consent, shows location only at city/area
  level, and shows no client names unless approved. PROPOSED (`SECURITY_RULES.md` §10).
  Consent process PENDING APPROVAL (Q-W5).
- **Services:** do not assume construction, contracting, procurement or turnkey work.
  CONFIRMED (`CLAUDE.md` §6). What the studio actually does is PENDING APPROVAL (Q-S1, Q-S2).

---

## 5. Database design requirements

Rules only — **no schema has been designed yet**. The table-by-table design and the diagram of
tables and their links are Stage 1 deliverables that do not exist yet. Source:
`DATABASE_RULES.md`.

| Area | Requirement | Status |
|---|---|---|
| Engine | MySQL 5.7+ / MariaDB 10.4+, InnoDB tables, `utf8mb4` text encoding (safe for Marathi/Devanagari) | PROPOSED; host versions PENDING APPROVAL (Q-H2) |
| Time | Asia/Kolkata (+05:30), with dates/times stored consistently in IST | ASSUMPTION (N-05) |
| Naming | Lowercase plural table names, numeric ID keys, real foreign-key constraints that block deleting referenced business records, `is_*` / `has_*` yes/no columns, indexes on all linking, status and date columns | PROPOSED |
| Status columns | Text columns checked against a fixed list in PHP, or a lookup table | PENDING APPROVAL (Stage 1 decision) |
| Standard columns | `created_at`, `created_by`, `updated_at`, `updated_by`; plus `deleted_at`, `deleted_by` where records are soft-deleted | PROPOSED |
| Money / area / rates | Exact decimal numbers only, **never floating point** (money DECIMAL(14,2), rates and area DECIMAL(12,2) + area unit, percentages DECIMAL(5,2), quantities DECIMAL(10,2)). PHP money arithmetic uses `bcmath` or whole paise | CONFIRMED (DECIMAL, `CLAUDE.md` §9); exact precisions PROPOSED |
| Totals | Saved on each document as a snapshot, and can be recalculated to check them | PROPOSED |
| Soft delete | For master records; hard delete only for spam enquiries and temporary files | CONFIRMED (`CLAUDE.md` §9) |
| Document numbers | Generated inside a transaction from a `number_sequences` table, with the row locked so two users never get the same number; numbers are unique | PROPOSED |
| Quotation revisions | `quotations` + `quotation_revisions` + `quotation_revision_items`, each revision a frozen snapshot | PROPOSED |
| Audit | `audit_logs` table: entries are only ever added, never changed or deleted by the application | CONFIRMED (audit log); structure PROPOSED |
| Files | The database stores file details only (original name, random stored name, file type, size, SHA-256 hash), not the files themselves | PROPOSED |
| Scripts | `database.sql` (table structure + starter data, **no real client data**); `sample_data.sql` (invented data only, no names or phone numbers from the sample); numbered migration files after first release | CONFIRMED (deliverables, `CLAUDE.md` §11); details PROPOSED |
| First admin | Created by an install step, with a password change forced at first login; no well-known default password | PROPOSED |
| Database-level locks on posted records | Optional database triggers that stop posted financial records being changed | PENDING APPROVAL (Stage 1 decision) |
| Database logins | Optional separate logins: `ajds_public` with limited rights, `ajds_erp` with full rights | PENDING APPROVAL (Stage 1 decision, depends on host) |

---

## 6. Security requirements

Source: `SECURITY_RULES.md`, summarized in `CLAUDE.md` §9. These rules are mandatory, and a
feature is not "done" until they are met.

| Area | Requirement |
|---|---|
| Public / ERP separation | Public code reads only published content and can only add enquiries. Every ERP request passes through the session / user-active / permission checks. ERP pages are marked `noindex` so search engines skip them |
| Files outside the website's public folder | `config/`, `app/` and `storage/` sit outside the web root. If the host forbids this, a weaker fallback is documented. Real credentials are never committed. Errors are logged, not displayed. Web access to `.sql`, `.md`, `.log`, `.env`, `.git` etc. is blocked |
| Authentication | Passwords stored only as secure hashes (`password_hash` / `password_verify`). Lockout after 5 failures for 15 minutes, plus limits per IP address. Same generic error for any wrong login. New session ID after login. Reset tokens stored only as hashes, valid 30–60 minutes and usable once. No default credentials in production |
| Password policy | Minimum 10+ characters — PROPOSED |
| Two-factor login (TOTP) for Admin | PENDING APPROVAL (Q-U3) |
| Sessions | ERP cookie `AJDS_ERP` limited to `/erp`, hidden from page scripts, sent only over HTTPS, protected from cross-site use (SameSite Lax or Strict — PENDING APPROVAL). Logout after 30 minutes idle and 10 hours maximum. Logout must be a POST request with a CSRF token |
| Uploads | Allowed file types checked by name, by actual content type, and by reading the image itself. Images re-saved to strip hidden content and location data. Random stored file names. No scripts can run in upload folders. File paths never built from user input |
| Upload storage | Public portfolio images in `public_html/uploads/portfolio/`. Private documents in `storage/documents/`, downloaded only after a permission check. Allowed private file types PENDING APPROVAL (Q-D1) |
| Requests | CSRF token on every request that changes data, including the public enquiry form. Data changes only through POST requests. Every field validated on the server. Database queries only through prepared statements. All output escaped. Rich text allowed only from a safe list of formatting |
| HTTP headers | HTTPS enforced (HSTS once HTTPS is confirmed), no content-type guessing, no framing by other sites, controlled referrer information, a content-security policy for each area, and restricted browser features. All HTTP traffic redirected to HTTPS |
| Authorization | Checked on the server for every action. Reversals, user changes, settings and backups are ADM-only |
| Public form abuse | Hidden spam-trap field, minimum time to fill in the form, rate limit per IP, limits on length and number of links. No CAPTCHA by default — PROPOSED (Q-W6) |
| Privacy | Enquiries stored with minimal data and visible only in the ERP. How long data is kept: PENDING APPROVAL (Q-G7). Privacy notice next to the form. India's DPDP Act 2023 to be reviewed with the client |
| Audit / backup | Audit log; error logs rotated; backups kept outside the public folder; backup downloads ADM-only and recorded in the audit log |
| Dependencies | Minimal: Bootstrap 5 plus a PDF library (choice PENDING APPROVAL, Q-T1), with fixed versions. ERP assets served locally rather than from a CDN — PROPOSED |
| WorkLedger (earlier CodInt app) | Do not copy its default passwords or its `fix_login.php` pattern (`CLAUDE.md` §4) |

---

## 7. UI/UX requirements

Source: `UI_UX_GUIDELINES.md`; `CLAUDE.md` §5.

### 7.1 Brand — CONFIRMED
- **Logo:** `reference/logo/Logo.jpeg` (1600×1034 JPEG, solid charcoal background).
  **Do not redraw, recolour, distort or add effects to it.** Header, sidebar, login, favicon
  and PDF versions are made only by cropping or resizing the supplied file.
- **Vector or transparent logo:** requested from the client — PENDING APPROVAL (Q-B1).

### 7.2 Colours and typography — PROPOSED; PENDING APPROVAL (Q-B2)

**Colours** (sampled from the logo):

| Name | Hex | Use |
|---|---|---|
| Charcoal | `#54545C` | Logo background, header/footer, ERP sidebar |
| Charcoal dark | `#3A3A40` | Text, hover states, footer |
| Copper | `#AF7B4C` | Main accent: buttons, links, highlights |
| Copper dark | `#8E5F36` | Button hover; small copper text |
| Tan | `#A78A5E` | Secondary accent, dividers |
| Ivory | `#F7F4EF` | Light page background |
| Stone | `#E8E3DB` | Alternating sections, cards, borders |
| White | `#FFFFFF` | Cards, forms |

- Copper is too light for small text on white, so small copper text uses copper dark.
- All text must meet the WCAG AA contrast standard.

**Typography:**
- **Headings:** Montserrat or Jost (sans-serif), or Cormorant Garamond (serif).
- **Body text:** Inter or Source Sans 3, 16 px.
- **Marathi (if approved):** Noto Sans Devanagari as the fallback font.

### 7.3 Public website — PROPOSED
- Image-first, generous white space, grid alignment.
- Header sticks to the top: transparent over the hero image, charcoal once the page scrolls.
- Mobile: slide-in menu.
- Floating WhatsApp button and tap-to-call.
- Only subtle motion, and none when the visitor's device asks for reduced motion.
- **No stock photos presented as studio work.** Placeholder images must be clearly marked and
  removed before launch.
- Layout adapts to screen size, designed for mobile first.
- Target: main content loads within 2.5 seconds on a 4G connection.

### 7.4 ERP — PROPOSED
- **Layout:** Bootstrap 5 admin layout with a charcoal sidebar, ivory content area, copper
  buttons, and status badges that look the same in every module.
- **Tables:** search, filter, sort, pagination and CSV export.
- **Forms:** grouped sections, validation messages next to the field, and a Save bar that
  stays visible on long forms.
- **Numbers and dates:** money in Indian format (₹1,10,000.00); dates DD/MM/YYYY — PENDING
  APPROVAL (Q-G8).
- **Safety:** confirmation dialogs before irreversible actions.
- **Devices:** works on tablet; key screens also work on mobile.

### 7.5 Print / PDF — PROPOSED
- A4 portrait, letterhead, footer with page numbers.
- The quotation follows the order of the sample: letterhead → reference/date → project title
  → scope → fee summary → signature block.
- Amount in words using lakh/crore.
- Letterhead style still to choose: the logo, or the red text heading + "श्री" used in the
  sample — PENDING APPROVAL (Q-Q2).
- Signature wording and whether to include a signature image or stamp — PENDING APPROVAL
  (Q-Q10).

### 7.6 Language — PENDING APPROVAL (Q-W8)
English for version 1 (ASSUMPTION A4). Marathi is optional.

---

## 8. Reports and financial calculations

### 8.1 Proposed reports — list PENDING APPROVAL (Q-R1) (`MODULES.md` §14)
Each report can be filtered by date range and exported to CSV or printed.

| Report | Necessity |
|---|---|
| Enquiry report (by source, status, conversion rate) | Core |
| Quotation register (status, value) | Core |
| Project status report | Core |
| Fees billed vs received; outstanding amounts by client/project | Core |
| Payment collection register (by payment mode) | Core |
| Expense report (by category, by project) | Core |
| Project profitability (fees received − project expenses) | Optional |

The dashboard shows totals (§3.2, module 1). Finance widgets are visible only to ADM and ACC.

### 8.2 Quotation calculation methods — PROPOSED (`MODULES.md` §6; `QUOTATION_ANALYSIS.md` §5)

| Method | Formula |
|---|---|
| Area-based | area × rate per unit (sq.ft / sq.m) |
| Area-based per category | area × rate for that category |
| Fixed fee | lump sum |
| Item-wise | quantity × rate |
| Custom charge | free text + amount |

- Methods can be combined in one quotation.
- **Optional blocks, all OFF by default:**
  - discount (amount or %)
  - tax lines (configurable rate, name and SAC code)
  - rounding rule
  - payment schedule
  - terms, exclusions, bank details, client acceptance block, amount in words

### 8.3 Calculation rules — PROPOSED (`DATABASE_RULES.md` §4)
- Exact decimal arithmetic only (`bcmath` or whole paise). Floating point is never used.
- Rounding rule configurable (none / nearest rupee / nearest 10). It is applied once, to the
  total, and the result is saved.
- Totals are saved on the document and can be recalculated to verify them.
- **Balance:**
  - normally: amount billed − amount received
  - if the studio does not issue bills: agreed fee − amount received (Q-F1)
- A single payment can be split across several bills. A payment received before billing is
  recorded as an advance against the client's account.

### 8.4 Not yet decided — PENDING APPROVAL
- **Order of calculation steps** when discount, tax and rounding are combined — not specified
  in any project file.
- **Area basis:** built-up, carpet, plot, or total of all floors; and whether sq.m is used (Q-Q3).
- **Rates:** one composite rate or separate rates per service (Q-Q4); fixed or item-wise fees (Q-Q5).
- **Tax:** GST registration status, GSTIN, rate and SAC code (Q-F3).
- **Payment stages and amounts** (Q-F2); discounts (Q-F4); extra charges (Q-F5).
- **Receipts:** format and numbering (Q-F6); payment modes (Q-F7).
- **Expenses:** what to track, and whether clients reimburse any (Q-F8).
- **Numbering:** quotation number format (Q-Q1); project code format (Q-P2); financial year
  start (April–March is ASSUMPTION A9, Q-G8).

---

## 9. Integrations and notifications

| Integration / notification | Description | Status |
|---|---|---|
| WhatsApp click-to-chat | `wa.me` link with a pre-filled message. Optionally counts clicks only (no personal data) | Core / CONFIRMED (W-05); number PENDING APPROVAL (Q-W4) |
| Enquiry email to studio | Email sent to the studio when a website enquiry arrives. Visitor input never goes into email headers | PROPOSED; recipient PENDING APPROVAL (Q-W6) |
| Auto-reply to visitor | None by default | PROPOSED (Q-W6) |
| Password reset email | Sent from the ERP | PROPOSED (`MODULES.md` §15) |
| Daily reminder digest | Sent by a scheduled job (cron) | Optional; PENDING APPROVAL (Q-G5) |
| Sending quotations by email from the ERP | Or only download the PDF and share it on WhatsApp | PENDING APPROVAL (Q-Q9) |
| Email sending method | PHP `mail()` or SMTP through a mailbox on the domain | PENDING APPROVAL (Q-H5) |
| Google Map on Contact page | Loaded only when needed | PROPOSED; PENDING APPROVAL (Q-W3) |
| Instagram link and search-engine business info (schema.org `sameAs`) | Link to the Instagram profile | PROPOSED |
| Google Business Profile / Search Console | Setup advice at launch, using the client's own account | PROPOSED |
| Scheduled jobs (cPanel cron) | Daily database backup; weekly backup of uploaded files; daily clean-up; reminder digest if approved | PROPOSED (`docs/TECHNICAL_REQUIREMENTS.md` §6) |
| Off-site backup copy | Where weekly copies are kept | PENDING APPROVAL (Q-H4) |
| **Not assumed** | SMS/WhatsApp Business API, payment gateway, Tally/GST filing, client portal | Out of scope (§1.6) |

---

## 10. Assumptions, missing information, and questions requiring your approval

### 10.1 Assumptions to validate — PENDING APPROVAL

| ID | Assumption | Source | Question |
|---|---|---|---|
| A1 | Small studio, 1–5 ERP users | `PROJECT_OVERVIEW.md` §6 | Q-U1 |
| A2 | Indian rupees only; Indian number format | `PROJECT_OVERVIEW.md` §6 | — |
| A3 | Area in sq.ft by default; sq.m possibly | `PROJECT_OVERVIEW.md` §6 | Q-Q3 |
| A4 | English website and ERP for v1; Marathi optional | `PROJECT_OVERVIEW.md` §6 | Q-W8 |
| A5 | Single office | `PROJECT_OVERVIEW.md` §6 | — |
| A6 | Design and supervision services only, no construction | `PROJECT_OVERVIEW.md` §6 | Q-S2 |
| A7 | Quotations are currently typed manually with a manual reference number | `BUSINESS_REQUIREMENTS.md` §1 | Q-G1 |
| A8 | Ar. Ajit Kumbhar has decision authority | `PROJECT_OVERVIEW.md` §2 | — |
| A9 | Dates DD/MM/YYYY; financial year April–March | `docs/PROJECT_SCOPE.md` §4 | Q-G8 |
| A10 | Time zone Asia/Kolkata | `BUSINESS_REQUIREMENTS.md` N-05 | — |
| A11 | The client supplies photos, descriptions, consent, service list, About text and terms | `docs/PROJECT_SCOPE.md` §4 | Q-W1, Q-W5, Q-W9, Q-S1, Q-Q7 |
| A12 | The host supports PHP 8.1+, cron, GD, bcmath, `finfo`, HTTPS, and folders outside `public_html` | `docs/TECHNICAL_REQUIREMENTS.md` §9 | Q-H2 |

### 10.2 Missing information
- **No client answers yet.** All 57 questions in `docs/CLIENT_QUESTIONS.md` are unanswered.
- **The developer brief is not in the project folder.** Items marked "CONFIRMED (brief)"
  cannot be checked against it.
- **Stage 1 deliverables not yet produced:**
  - diagram of tables and their links
  - table-by-table database design
  - role × module permission matrix
  - list of ERP page addresses
  - detailed quotation calculation spec, including the order of discount, tax and rounding
  - PDF library choice
  - page sketches (wireframes)
- **Brand and content:**
  - portfolio photos: `reference/portfolio/` is empty
  - vector or transparent logo
  - About text
  - final service descriptions
  - quotation terms
- **Hosting:** domain, hosting plan and its capabilities, budget and timeline.
- **Meaning of the Instagram highlight titles** "Temple Work", "कोकण शिल्प" and
  "Complete Project".

### 10.3 Inconsistencies in the project files to resolve — PENDING APPROVAL
1. **Stage naming.** The project files record Stage 0 (documentation). Stage 1 is defined as
   architecture & database design.
2. **When to set up Git.** `CLAUDE.md` §10 says at the start of Stage 1;
   `DEVELOPMENT_ROADMAP.md` §4 says at the start of Stage 2.
3. **Private document download address.** `SECURITY_RULES.md` §5 uses `erp/download.php?id=`;
   `docs/TECHNICAL_REQUIREMENTS.md` §2.2 uses `erp/index.php?route=documents/download`.
4. **WhatsApp clicks.** `MODULES.md` §12 lists "WhatsApp-click submissions" as enquiries, but
   the website plan only counts clicks, with no personal data.
5. **Backup retention.** `DATABASE_RULES.md` §11 says "7 daily, 4 weekly";
   `docs/TECHNICAL_REQUIREMENTS.md` §7 adds "3 monthly".

### 10.4 Questions requiring your approval

**A. Priority questions for the client** — needed before the architecture and database design
can be approved (`docs/CLIENT_QUESTIONS.md`):

| Area | IDs | Decision needed |
|---|---|---|
| Workflow | Q-G1, Q-G2, Q-G9 | How things are tracked today; the real business sequence; launch the website first or everything together |
| Services | Q-S1, Q-S2 | Final service list; design-only or also execution |
| Website & brand | Q-W1, Q-W3, Q-W4, Q-W5, Q-B1 | Portfolio content; address, map and hours; WhatsApp number and email to publish; consent to publish projects; vector logo |
| Quotation | Q-Q1, Q-Q2, Q-Q3, Q-Q4, Q-Q5, Q-Q7 | Number format; letterhead style; area basis; one rate or several; fixed/item-wise fees; standard terms |
| Fees | Q-F1, Q-F2, Q-F3, Q-F6 | Bills or payments only; payment stages; GST; receipts |
| Users | Q-U1 | Users, roles, who can see finances |
| Hosting | Q-H1, Q-H2 | Domain; hosting plan and capabilities |

**B. Developer decisions** — for you as the developer:
1. Approve the final module list and necessity ratings (§3).
2. Approve the proposed roles and permission model (§2).
3. PDF library: Dompdf or mPDF. mPDF is favoured if Devanagari text such as "श्री" is needed
   (Q-T1).
4. Status columns: text checked against a list in PHP, or lookup tables.
5. Whether to add database-level locks on posted financial records.
6. Whether to use one database login or two (limited public / full ERP).
7. Password minimum length (10+ proposed); SameSite setting Lax or Strict.
8. Whether to use the WorkLedger app as a reference for coding style or multilingual support
   (Q-G3).
9. When to set up Git, and how to resolve the other inconsistencies in §10.3.
10. Phased launch: website + portfolio management + website enquiries first, the full ERP
    later (Q-G9).

**C. Approval gate** (`DEVELOPMENT_ROADMAP.md` §1). The next stage needs **written approval of
the architecture and database design**, recorded in the decision log (§5). Until then:
- no PHP code, `database.sql`, `sample_data.sql`, interface pages or ERP modules are to be
  written (`CLAUDE.md` gate)
- no item is upgraded to CONFIRMED without a recorded decision

---

*End of document. Compiled from existing project files only; no source file was modified.*
