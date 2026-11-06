# AJ Design Studio — Stage Review Package

| | |
|---|---|
| Project | AJ Design Studio — Public Portfolio Website + Private ERP |
| Developer | CodInt Digitech |
| Client | AJ Design Studio (Principal Architect: Ar. Ajit Kumbhar) |
| Package compiled | 2026-11-06 |
| Purpose | Independent review of the project documentation by a third party (human or AI) |
| Source documents | 13 Markdown files, reproduced **verbatim** in Part B |

---

## How to use this package

- **Part A** (this section) is a reviewer's guide written by the compiler: document
  inventory, missing files, observed inconsistencies, a condensed view of the proposed
  architecture and roadmap, and consolidated registers of assumptions and pending decisions.
  Part A summarises and points; it does **not** change any requirement.
- **Part B** contains the full, unmodified text of each source document, each wrapped in a
  ```` ````markdown ```` block so its own headings and code blocks are preserved exactly.
  **Where Part A and Part B differ, Part B (the original) is authoritative.**
- Status tags used throughout the originals (defined in `CLAUDE.md` §3):
  **[CONFIRMED]** stated in a reference or the developer brief · **[PROPOSED]** our
  recommendation, needs approval · **[ASSUMPTION]** working assumption, must be validated ·
  **[PENDING]** client decision required (question IDs `Q-…` in `docs/CLIENT_QUESTIONS.md`).
- No source code, SQL, images, PDFs or ZIP contents are included. Reference assets are
  described only by name and the facts the documents record about them.

### Important note on stage status

The request that produced this package describes the work as **"Stage 1 completed"**.
The documents themselves record a different status, reproduced here without correction:

- `CLAUDE.md`: *"Current stage: Stage 0 – Documentation & requirements (awaiting client/developer approval)"*.
- `project-context/DEVELOPMENT_ROADMAP.md` §1 defines **Stage 0 = Discovery & documentation**
  and **Stage 1 = Architecture & database design** (ER diagram, table-by-table schema doc,
  role/permission matrix, wireframes, etc.). The decision log (§5) has one entry:
  *"Stage 0 documentation produced; awaiting review"*.

So the documents in this package are the **Stage 0 (discovery & documentation) set**, which
corresponds to the developer's "Stage 1" in the request. The reviewer should read it as such;
the Stage 1 design deliverables defined in the roadmap are not present (see A.2).

---

# PART A — REVIEWER'S GUIDE

## A.1 Document inventory

All 13 requested files were found and are included in full.

| # | File | Lines | Bytes | Role |
|---|---|---|---|---|
| 1 | `CLAUDE.md` | 163 | 8,635 | Project charter: vision, document map, tag rules, references, brand, business facts, quotation rules, stack, security summary, dev rules, deliverables |
| 2 | `project-context/PROJECT_OVERVIEW.md` | 100 | 4,884 | Facts, stakeholders, goals, constraints, key assumptions A1–A6 |
| 3 | `project-context/BUSINESS_REQUIREMENTS.md` | 117 | 6,176 | Requirement IDs W-01..13, E-01..20, Q-R01..09, N-01..06 with status |
| 4 | `project-context/MODULES.md` | 181 | 10,569 | 6 public-site modules (P1–P6) + 17 ERP modules with necessity ratings |
| 5 | `project-context/DATABASE_RULES.md` | 103 | 5,353 | Schema conventions, money/DECIMAL, soft delete, financial integrity, audit, scripts, backups |
| 6 | `project-context/SECURITY_RULES.md` | 96 | 5,948 | Mandatory security controls (12 sections) |
| 7 | `project-context/UI_UX_GUIDELINES.md` | 78 | 4,823 | Logo rules, colour tokens, typography, public/ERP look, print/PDF, accessibility |
| 8 | `project-context/DEVELOPMENT_ROADMAP.md` | 61 | 4,437 | Stages 0–12 with gates, testing, environments, version control, decision log, risks |
| 9 | `docs/PROJECT_SCOPE.md` | 71 | 3,843 | Confirmed / in-scope / out-of-scope / assumptions / pending / acceptance |
| 10 | `docs/QUOTATION_ANALYSIS.md` | 115 | 6,663 | Analysis of the dummy sample quotation; proposed configurable quotation model |
| 11 | `docs/CLIENT_QUESTIONS.md` | 95 | 7,845 | 57 open questions with priorities; answer column empty |
| 12 | `docs/PORTFOLIO_WEBSITE_PLAN.md` | 109 | 5,407 | Sitemap, URLs, page plans, enquiry form, SEO, content checklist |
| 13 | `docs/TECHNICAL_REQUIREMENTS.md` | 138 | 7,883 | Stack, hosting layout (website + ERP on one account), request flow, conventions, cron, backup, deployment |

Project folder contents at compile time: the 13 files above plus `reference/` (not reproduced).
No other documentation, code, SQL or configuration files exist. The folder is not a Git repository.

## A.2 Missing files and gaps

### A.2.1 Stage 1 deliverables defined in the roadmap but not present
`DEVELOPMENT_ROADMAP.md` §1 lists these as Stage 1 deliverables. None exists as a separate file:

| Deliverable | Current state |
|---|---|
| Final module list (after necessity review) | Only the *proposed* list with necessity ratings (`MODULES.md`) |
| ER diagram | Not present |
| Table-by-table schema document (or SQL draft) | Not present; only conventions (`DATABASE_RULES.md`) and table names mentioned in passing (e.g. `quotations`, `quotation_revisions`, `quotation_revision_items`, `number_sequences`, `audit_logs`, `settings`) |
| Role / permission matrix | Not present; roles ADM/STF/ACC/SITE proposed and PENDING Q-U1 |
| Folder structure | Present in `TECHNICAL_REQUIREMENTS.md` §2.2 / §2.4 |
| URL map | Public URLs in `PORTFOLIO_WEBSITE_PLAN.md` §2; ERP URLs limited to `/erp/`, `/erp/login`, `/erp/dashboard` and a document-download route — no per-module ERP URL map |
| Quotation calculation spec | Proposed model in `QUOTATION_ANALYSIS.md` §5 (methods, optional blocks); no worked rounding/tax/discount order-of-operations spec |
| PDF library choice | Not decided (Q-T1: Dompdf vs mPDF) |
| Wireframes for key pages | Not present |

### A.2.2 Source material referenced but not in the folder
| Item | Referenced in | Note |
|---|---|---|
| The **developer brief** | Many "[CONFIRMED – developer brief]" / "CONFIRMED (brief)" tags | Not on disk. A reviewer cannot verify which requirements truly come from it. |
| `AJ_Design_Studio_Logo.jpeg` | `CLAUDE.md` §4 (brief's name) | On disk as `reference/logo/Logo.jpeg` (not renamed, by design) |
| `work_pfd_fees_structure.pdf` | `CLAUDE.md` §4 (brief's name) | On disk as `reference/quotation-samples/work pfd & fees structure.pdf` |
| Portfolio images | `reference/portfolio/` | Folder is **empty** |
| Vector / transparent logo | Q-B1 | Requested, not supplied |
| Client answers | `docs/CLIENT_QUESTIONS.md` | All 57 "Answer" cells are blank |

### A.2.3 Files referenced as future outputs (expected to be absent now)
`database.sql`, `sample_data.sql`, `migrations/…`, `config/config.sample.php`, `config/config.php`,
`docs/testing/` (Stage 2), installation / user / testing / deployment / backup guides,
`.gitignore`, final ZIP `AJ_Design_Studio_Portfolio_ERP.zip`. Their absence is consistent with the gate.

## A.3 Inconsistencies and ambiguities observed (not corrected)

These are reported for the reviewer; the original text in Part B has not been changed.

| # | Topic | Location A | Location B |
|---|---|---|---|
| 1 | Stage naming | Request calls this "Stage 1 completed" | `CLAUDE.md` and the roadmap say Stage 0, awaiting approval |
| 2 | When to initialise Git | `CLAUDE.md` §10: "initialise Git at the start of Stage 1" | `DEVELOPMENT_ROADMAP.md` §4: "Initialise at Stage 2 start (Stage 1 if docs should be versioned now)"; Stage 2 deliverables also list "Git init" |
| 3 | Private document download route | `SECURITY_RULES.md` §5: `erp/download.php?id=` | `TECHNICAL_REQUIREMENTS.md` §2.2: `erp/index.php?route=documents/download&id=…` |
| 4 | WhatsApp clicks as enquiries | `MODULES.md` module 12: inbox of "website form/WhatsApp-click submissions" | `PORTFOLIO_WEBSITE_PLAN.md` §3: WhatsApp click optionally logged as "count only, no personal data" — a click cannot become an enquiry record |
| 5 | Decision-log reference | Roadmap §5 entry references "this commit/set" | The folder is not a Git repository, so there is no commit |
| 6 | Status-column design | `DATABASE_RULES.md` §2: VARCHAR validated in PHP "(or lookup table) … Final choice in Stage 1" | Open decision, not listed in `CLIENT_QUESTIONS.md` (internal) |
| 7 | Separate DB users (public vs ERP) | `SECURITY_RULES.md` §1: "Decide in Stage 1" | `TECHNICAL_REQUIREMENTS.md` §2.5: "Optional" — open internal decision, no ID |
| 8 | Backup retention | `DATABASE_RULES.md` §11: "e.g. 7 daily, 4 weekly" | `TECHNICAL_REQUIREMENTS.md` §7: "7 daily, 4 weekly, 3 monthly" |
| 9 | "CONFIRMED (brief)" | `BUSINESS_REQUIREMENTS.md` header: brief requires it but client has not validated against workflow | Reviewer should treat "CONFIRMED (brief)" as weaker than CONFIRMED-from-reference |
| 10 | Logo on PDFs | `UI_UX_GUIDELINES.md` §1 plans a logo PDF letterhead | Sample quotation uses a red text heading + "श्री", not the logo — PENDING Q-Q2 |

## A.4 Proposed architecture (condensed — full text in Part B, docs 6, 5 and 13)

All items below are **[PROPOSED]** unless marked otherwise.

- **Deployment model [CONFIRMED]:** one hosting account, one domain; public site at `/`, ERP at `/erp/`
  (`/erp/login`, `/erp/dashboard`). Domain and host not yet chosen (Q-H1, Q-H2).
- **Stack [CONFIRMED]:** Core PHP (8.1+ proposed), MySQL/MariaDB, PDO prepared statements,
  Bootstrap 5, HTML5/CSS3/vanilla JS, AJAX; XAMPP dev, cPanel production. No framework.
  PDF via Dompdf or mPDF (Q-T1); GD/Imagick; bcmath for money.
- **One codebase, one database, two front controllers:** `public_html/index.php` and
  `public_html/erp/index.php` both load `ajds_app/app/core/bootstrap.php`.
- **Sensitive code outside the web root:** `/home/<user>/ajds_app/` holds `config/`, `app/core|public|erp|shared`,
  `storage/documents|logs|backups|cache|tmp`, `vendor/`, `database/`. Fallback inside web root with
  `Require all denied` is documented as weaker.
- **Request flow:** Apache `.htaccess` → front controller → bootstrap → Router →
  [ERP: Auth + Permission + CSRF] → Controller → Model (PDO) → View → HTML / JSON / PDF / file stream.
- **Isolation:** public code reads only published content and inserts enquiries; ERP session cookie
  `AJDS_ERP`, path `/erp`, HttpOnly/Secure/SameSite; optional separate DB users.
- **Uploads:** public portfolio images in `public_html/uploads/portfolio/` (re-encoded, EXIF stripped);
  private documents in `storage/documents/`, streamed only after permission checks.
- **Data rules:** InnoDB/utf8mb4; DECIMAL for money/area/rates; soft delete for masters;
  posted financial records immutable, corrected by linked reversal; document numbers from a
  locked `number_sequences` table; append-only `audit_logs`; quotation revisions as frozen snapshots.
- **Operations:** cPanel cron for daily DB backup, weekly file backup, cleanup, optional reminder digest;
  retention 7 daily / 4 weekly / 3 monthly (TECH §7; see A.3 #8); restore drill before go-live.
- **Modules:** public P1–P6 (pages, portfolio, gallery, enquiry form, WhatsApp, SEO); ERP 1–17
  (Dashboard, Enquiries, Clients, Projects, Services, Quotations, Fees & Billing, Payments, Expenses,
  Documents, Portfolio CMS, Website Enquiries, Follow-ups, Reports, Users & Roles, Settings, Audit Log).
  Core / Recommended / Optional split in `MODULES.md` "Necessity summary".

## A.5 Development roadmap (condensed — full text in Part B, doc 8)

| Stage | Name | Gate |
|---|---|---|
| 0 | Discovery & documentation | Developer review + client answers to priority questions |
| 1 | Architecture & database design | Written approval of architecture + DB design |
| 2 | Foundation (Git, skeleton, auth, roles, CSRF, layouts, audit, `database.sql` v1, installer) | Login + security checklist tested |
| 3 | Masters & settings | Module tests pass |
| 4 | Public website | Client review of design on staging |
| 5 | Portfolio CMS | Client uploads a real project end-to-end |
| 6 | CRM (enquiries, follow-ups, clients, dashboard v1) | Module tests pass |
| 7 | Projects & documents | Module tests pass |
| 8 | Quotations | Client approves PDF format with real example |
| 9 | Fees, payments, expenses | Financial test cases pass |
| 10 | Reports & dashboard v2 | Client sign-off |
| 11 | Hardening & QA | Test report |
| 12 | Deployment & handover (final ZIP) | Client acceptance |

Stages 4–5 and 6–9 may be reordered for a website-first "Phase 1" launch (PENDING Q-G9).
Current position per documents: end of Stage 0, gate not yet passed. Implementation is gated.

## A.6 Consolidated assumptions register

Collected from the originals; wording abbreviated. Source in brackets.

| ID | Assumption | Validating question |
|---|---|---|
| A1 | Studio is small, 1–5 ERP users [OVERVIEW §6; SCOPE §4] | Q-U1 |
| A2 | INR only; Indian number format (1,10,000) [OVERVIEW §6; SCOPE §4] | — |
| A3 | Area unit sq.ft by default, possibly sq.m [OVERVIEW §6] | Q-Q3 |
| A4 | English website/ERP for v1; Marathi optional [OVERVIEW §6; SCOPE §4] | Q-W8 |
| A5 | Single office / branch [OVERVIEW §6; SCOPE §4] | — |
| A6 | Studio provides design and supervision, not construction [OVERVIEW §6] | Q-S2 |
| A7 | Quotations are typed manually in Word/PDF with a manual ref number [BUSINESS §1] | Q-G1 |
| A8 | Ar. Ajit Kumbhar is the decision authority [OVERVIEW §2] | — |
| A9 | Dates DD/MM/YYYY; FY April–March [SCOPE §4; UI §5] | Q-G8 |
| A10 | Time zone Asia/Kolkata (N-05) [BUSINESS §6; DATABASE §1] | — |
| A11 | Client supplies photos, descriptions, publishing consent, service list, About text, quotation terms [SCOPE §4] | Q-W1, Q-W5, Q-W9, Q-S1, Q-Q7 |
| A12 | Host supports PHP 8.1+, MySQL/MariaDB, HTTPS, cron, GD, mbstring, bcmath, `finfo` [SCOPE §4; TECH §9] | Q-H2 |
| A13 | Host allows folders outside `public_html` (fallback documented) [TECH §2.2–2.3] | Q-H2 |
| A14 | Sample quotation is a dummy; its rate/area/total are not defaults [CLAUDE §7; QUOTATION §3] | (confirmed as dummy by brief) |

Explicitly **not assumed** (excluded unless the client confirms): construction execution/contracting,
material procurement or resale, turnkey interiors, vendor/contractor payments, payroll, inventory,
GST filing, payment gateway, client portal, mobile app, multi-branch, multi-currency,
SMS/WhatsApp API automation, content writing/photography, domain/hosting purchase, historical data migration.
[BUSINESS §7; SCOPE §3]

## A.7 Pending decisions

### A.7.1 Client questions — summary
`docs/CLIENT_QUESTIONS.md` contains **57** questions: **23 P1** (needed before architecture/DB approval),
**26 P2** (before the module is built), **8 P3** (can wait). **None is answered.**

**P1 questions (block the Stage 1 gate):**

| Area | IDs | Subject |
|---|---|---|
| Workflow | Q-G1, Q-G2, Q-G9 | Current tracking method; real business sequence; website-first or together |
| Services | Q-S1, Q-S2 | Final service list; meaning of Temple Work / कोकण शिल्प / Complete Project; construction or design-only |
| Website & brand | Q-W1, Q-W3, Q-W4, Q-W5, Q-B1 | Portfolio content; address/map/hours; WhatsApp & email to publish; client publishing consent; vector logo |
| Quotation | Q-Q1, Q-Q2, Q-Q3, Q-Q4, Q-Q5, Q-Q7 | Number format; letterhead style; area basis/unit; composite vs split rates; fixed/item-wise fees; standard terms |
| Fees | Q-F1, Q-F2, Q-F3, Q-F6 | Bills vs payments only; payment stages; GST registration; receipts |
| Users | Q-U1 | Users, roles, visibility of finances |
| Hosting | Q-H1, Q-H2 | Domain; hosting plan and capabilities |

`docs/PROJECT_SCOPE.md` §5 ranks the highest-priority decisions as: (1) final service list and meaning
of the Instagram highlight categories, (2) fee/billing model, (3) users and roles, (4) portfolio content
and consent, (5) domain and hosting, (6) website-first phased launch or all together.

### A.7.2 Internal (developer) decisions still open
| Decision | Where |
|---|---|
| PDF library: Dompdf vs mPDF | Q-T1; SECURITY §12; TECH §1 |
| Use of WorkLedger app as a style reference | Q-G3 |
| Status columns: VARCHAR + PHP constants vs lookup tables | DATABASE §2 |
| Optional DB triggers for financial immutability | DATABASE §6 |
| Two DB users (public limited / ERP full) | SECURITY §1; TECH §2.5 |
| Password policy minimum (10+ chars proposed) | SECURITY §3 |
| SameSite Lax vs Strict | SECURITY §4 |
| Git initialisation timing | CLAUDE §10 vs ROADMAP §4 |

### A.7.3 Decision log status
Only one entry is recorded (2026-11-06, Stage 0 documentation produced). Placeholders exist for service
list, quotation format & fee rules, roles & users, hosting/domain. No tag has been upgraded to CONFIRMED by a
recorded client decision.

## A.8 Suggested review focus

Questions the compiler suggests an independent reviewer consider (no answers implied):

1. Is the module list right-sized for a 1–5 person studio, or should some Core modules move to Recommended/Optional?
2. Is merging website enquiries into the main enquiry module (Q-G4) the better default?
3. Is the financial model (bills + allocations + reversals + lock date) proportionate if the studio only
   collects payments against a quoted total (Q-F1)?
4. Are the security controls achievable on typical Indian cPanel shared hosting (files above web root,
   separate DB users, CSP, cron)?
5. Are any requirements tagged CONFIRMED actually unverifiable because the developer brief is not available?
6. Do the 23 P1 questions cover everything needed before database design, and are any P1 items missing?
7. Is the website-first phased launch (Q-G9) the lower-risk path given that no portfolio photos exist yet?

---

# PART B — SOURCE DOCUMENTS (VERBATIM)

Each document below is reproduced exactly as it exists on disk at compile time.
Paths inside the documents are relative to the project root.

---

## B.1 `CLAUDE.md`

````markdown

# PROJECT: AJ DESIGN STUDIO
## Public Portfolio Website + Private ERP System

| | |
|---|---|
| Developer | CodInt Digitech |
| Client organization | AJ Design Studio |
| Principal Architect | Ar. Ajit Kumbhar (Instagram profile shows "Ar. Ajit Arjun Kumbhar") |
| Current stage | **Stage 0 – Documentation & requirements (awaiting client/developer approval)** |
| Last updated | 2026-11-06 |

> **GATE:** Do not start implementation (PHP code, `database.sql`, `sample_data.sql`,
> UI pages, ERP modules) until requirements, architecture and database design have
> been reviewed and approved. Current approval status is tracked in
> `project-context/DEVELOPMENT_ROADMAP.md`.

---

## 1. PROJECT VISION

One integrated web application, deployed on **one hosting account and one domain**,
with two independent user experiences:

**A. Public portfolio website** (new — the client has **no existing website**)
- Open to everyone, no login. Premium architecture/interior portfolio.
- Projects, services, galleries, contact, enquiry form, WhatsApp enquiry.
- Responsive, SEO-friendly. Content managed from the ERP.

**B. Private ERP**
- Separate secure login, authorized organization users only.
- Enquiries, clients, projects, quotations, fees, payments, expenses,
  documents, follow-ups, reports, users/roles, settings, portfolio CMS.
- Public visitors must never reach ERP data, files or configuration.

URL structure (domain to be configured later):

| Area | URL |
|---|---|
| Public website | `https://<domain>/` |
| ERP root | `https://<domain>/erp/` |
| ERP login | `https://<domain>/erp/login` |
| ERP dashboard | `https://<domain>/erp/dashboard` |

How both run on the same hosting account: see `docs/TECHNICAL_REQUIREMENTS.md` §2.

## 2. DOCUMENT MAP (read before working)

| File | Purpose |
|---|---|
| `project-context/PROJECT_OVERVIEW.md` | Facts, stakeholders, confirmed vs. assumed |
| `project-context/BUSINESS_REQUIREMENTS.md` | Business requirements with status tags |
| `project-context/MODULES.md` | Proposed ERP + website module specifications |
| `project-context/DATABASE_RULES.md` | Schema conventions, money, soft delete, audit |
| `project-context/SECURITY_RULES.md` | Mandatory security controls |
| `project-context/UI_UX_GUIDELINES.md` | Brand, colours, typography, layout rules |
| `project-context/DEVELOPMENT_ROADMAP.md` | Stages, approval gates, decision log |
| `docs/PROJECT_SCOPE.md` | In scope / out of scope / pending |
| `docs/QUOTATION_ANALYSIS.md` | Analysis of the sample quotation |
| `docs/CLIENT_QUESTIONS.md` | Open questions for the client (master list) |
| `docs/PORTFOLIO_WEBSITE_PLAN.md` | Public website sitemap and page plans |
| `docs/TECHNICAL_REQUIREMENTS.md` | Stack, hosting layout, folder structure, deployment |

## 3. STATUS TAGS (use consistently in every document)

- **[CONFIRMED]** – stated in a supplied reference (logo, sample quotation, public Instagram profile) or by the developer brief.
- **[PROPOSED]** – our recommendation; needs approval.
- **[ASSUMPTION]** – working assumption; must be validated.
- **[PENDING]** – client decision required; see `docs/CLIENT_QUESTIONS.md`.

Never upgrade a tag to CONFIRMED without a written client/developer decision
recorded in the decision log (`project-context/DEVELOPMENT_ROADMAP.md` §5).

## 4. REFERENCE MATERIAL (actual file names on disk)

| Reference | Actual path | Notes |
|---|---|---|
| Logo | `reference/logo/Logo.jpeg` | 1600×1034 JPEG, opaque charcoal background. Brief calls it `AJ_Design_Studio_Logo.jpeg`; file was **not renamed**. |
| Sample quotation | `reference/quotation-samples/work pfd & fees structure.pdf` | 2 pages, dummy/sample. Brief calls it `work_pfd_fees_structure.pdf`. |
| Portfolio images | `reference/portfolio/` | **Empty.** No project photos supplied yet. |
| WorkLedger | `reference/WorkLedger/WorkLedger_Multilingual_EN_HI_MR.zip` | Earlier CodInt Digitech PHP app (staff work/wages, EN/HI/MR). Not mentioned in the brief; treated only as a possible coding-style reference. Do not copy its default passwords or `fix_login.php` pattern. |
| Instagram | https://www.instagram.com/ar.ajkumbhar | Public profile header only (posts need login). |

Do not modify, rename or delete anything under `reference/`.

## 5. BRAND IDENTITY

- Logo: copper triangular "AJ" monogram above "DESIGN STUDIO" in bold condensed
  capitals, on charcoal grey, with a decorative copper dot column on the left.
- Sampled colours (from the JPEG, approximate): charcoal `#54545C`, copper `#AF7B4C`,
  secondary tan accent `#A78A5E`.
- Direction: charcoal grey + copper/bronze, light neutral backgrounds, premium
  architectural presentation, clean typography, elegant galleries.
- **Do not replace, redraw, recolour or distort the logo.** Derivatives (header,
  ERP sidebar, login, favicon) are crops/resizes of the supplied file only.
  A vector/transparent original has been requested from the client.
- Details: `project-context/UI_UX_GUIDELINES.md`.

## 6. BUSINESS PROFILE (confirmed facts only)

From the sample quotation letterhead and the public Instagram profile:
- AJ Design Studio — **Architect, Interior Designer**.
- Address on letterhead: Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan.
- Instagram location line: Patan, Karad, Satara.
- Contact on both: 8806956877, ar.ajitkumbhar16@gmail.com.
- Reference work categories from the quotation: floor plans, working drawings
  (sections, elevations, municipal drawing), exterior 3D, interior design layouts,
  interior 3D, construction-stage site visits, material & colour selection.
- Instagram highlight titles (labels only, not confirmed services): Bunglow Project,
  Temple Work, कोकण शिल्प, Mini Bunglow, Complete Project, Interior Site.

Do **not** assume construction execution, contracting, material procurement,
turnkey work or any other service without written approval. Do not publish
contact details, project names or client names on the website until approved.

## 7. QUOTATION RULES

The sample (`Ref 1/2025`, 1100 sq.ft × ₹100/sq.ft = ₹1,10,000) is a **dummy**.
- Never hardcode ₹100/sq.ft, the area, or the total.
- Do not assume GST, payment schedule, discounts, terms, validity, extra-visit
  charges or revision limits. All are configurable and pending approval.
- Proposed calculation methods: area-based, fixed fee, item-wise, custom charges.
- Required capabilities: PDF + print, revision history, approval status.
- Full analysis: `docs/QUOTATION_ANALYSIS.md`.

## 8. TECHNICAL STACK

Core PHP (8.1+ proposed) · MySQL/MariaDB · PDO prepared statements · Bootstrap 5 ·
HTML5/CSS3/vanilla JS · AJAX where useful · XAMPP for development · cPanel deployment.
Avoid frameworks and unnecessary dependencies. Modular PHP. Details and the
proposed folder layout: `docs/TECHNICAL_REQUIREMENTS.md`.

## 9. SECURITY AND DATA RULES (summary — full text in `project-context/SECURITY_RULES.md`)

- `password_hash()`/`password_verify()`; role-based authorization on every ERP request.
- CSRF token on every state-changing request; server-side validation always.
- PDO prepared statements only; no string-built SQL with user input.
- Application code, config, private documents and backups live **outside the web root**.
- Uploads: whitelist + MIME sniffing, random file names, no script execution in upload dirs.
- Separate ERP session cookie (path `/erp`, HttpOnly, Secure, SameSite).
- Audit log for important business operations.
- Soft delete for ordinary master records; financial transactions are never silently
  overwritten — use corrections/reversals. DECIMAL for money, area and rates.

## 10. DEVELOPMENT RULES

- Inspect existing files before changing them; do not delete existing files.
- Keep documentation, schema and SQL scripts synchronized.
- No duplicate files. Build and test module by module.
- Never claim tests passed unless actually executed (PHP/MySQL are not on the
  shell PATH of this machine; XAMPP location to be confirmed).
- Do not invent client requirements, services, projects or company claims.
- Record unresolved decisions in `docs/CLIENT_QUESTIONS.md` and the decision log.
- The project folder is **not yet a Git repository**; initialise Git at the start of
  Stage 1 and commit at each milestone.

## 11. FINAL DELIVERABLE

Complete running application: public website, ERP, full PHP source, `database.sql`,
`sample_data.sql` (fictitious data only), assets/branding, installation guide, user
guide, testing documentation, deployment instructions, backup & restore instructions.

Final ZIP: `AJ_Design_Studio_Portfolio_ERP.zip`
````

---

## B.2 `project-context/PROJECT_OVERVIEW.md`

````markdown
# Project Overview — AJ Design Studio Portfolio Website + ERP

Status tags: **[CONFIRMED] [PROPOSED] [ASSUMPTION] [PENDING]** (see `CLAUDE.md` §3).
Last updated: 2026-11-06 · Stage 0 (documentation).

## 1. Summary

AJ Design Studio is an architecture and interior design practice led by
Ar. Ajit Kumbhar. The studio **has no website today** [CONFIRMED – developer brief].
CodInt Digitech will build, on one hosting account and one domain:

1. A new **public portfolio website** at `/`.
2. A **private ERP** at `/erp/` for running the studio's office work
   (enquiries → quotations → projects → fees → payments → reports).

The ERP is also the content-management back office for the website's portfolio.

## 2. Stakeholders

| Role | Name / Org | Status |
|---|---|---|
| Client | AJ Design Studio | CONFIRMED |
| Principal Architect / decision maker | Ar. Ajit Kumbhar | CONFIRMED (decision authority ASSUMPTION) |
| Developer | CodInt Digitech | CONFIRMED |
| ERP users other than the principal | Unknown (staff, accountant, site engineer?) | PENDING – Q-U1 |
| Website visitors | Prospective clients, public | CONFIRMED |

## 3. Facts gathered from references

### 3.1 Organization details [CONFIRMED]
| Item | Value | Source |
|---|---|---|
| Name | AJ Design Studio | Logo, quotation, Instagram |
| Profession | Architect, Interior Designer | Quotation letterhead, Instagram bio |
| Address | Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan | Quotation letterhead |
| Area line | Patan, Karad, Satara | Instagram bio |
| Phone | 8806956877 | Quotation, Instagram |
| Email | ar.ajitkumbhar16@gmail.com | Quotation, Instagram |
| Instagram | @ar.ajkumbhar (display name "AJ DESIGN STUDIO") | Instagram |

Whether these are the details to publish on the website (and whether the phone is
also the WhatsApp number) is **[PENDING – Q-W3, Q-W4]**.

### 3.2 Instagram (public, without login, checked 2026-11-06)
- Bio: "Architect & Interior Designer", email, phone, "Patan, Karad, Satara".
- Story-highlight titles: *Bunglow Project, Temple Work, कोकण शिल्प, Mini Bunglow,
  Complete Project, Interior Site*.
- Posts and images were not readable without login. **No project names, photos or
  descriptions have been taken from Instagram.** Highlight titles are recorded only
  as hints for questions (e.g. is temple work a service? what does "Complete Project" mean?).

### 3.3 Logo
- `reference/logo/Logo.jpeg`, 1600×1034 px JPEG, no transparency.
- Copper (~`#AF7B4C`) triangular "AJ" monogram, "DESIGN STUDIO" wordmark, charcoal
  (~`#54545C`) background, dotted column ornament on the left.

### 3.4 Sample quotation
- 2-page dummy quotation, `Ref: 1/2025`, dated 15/12/2025, for a bungalow project
  at Karad, area-based fee 1100 sq.ft × ₹100 = ₹1,10,000. Treated as **reference only**.
- Full analysis: `docs/QUOTATION_ANALYSIS.md`.

### 3.5 Other material in the folder
- `reference/portfolio/` is empty — **no portfolio photos supplied yet**.
- `reference/WorkLedger/…zip` — an earlier CodInt Digitech PHP/MySQL app (staff,
  work entries, wages, payments, EN/HI/MR translations). Not referenced in the brief.
  Possible use: house coding style and multilingual approach. **[PENDING – Q-G3]**

## 4. Goals

| # | Goal | Status |
|---|---|---|
| G1 | Establish a premium online presence with a portfolio | CONFIRMED |
| G2 | Capture enquiries from the website (form + WhatsApp) | CONFIRMED |
| G3 | Manage enquiries, clients and projects in one place | CONFIRMED (brief) |
| G4 | Produce consistent, professional quotations with revisions/approval | CONFIRMED (brief) |
| G5 | Track fees billed, payments received and expenses per project | PROPOSED |
| G6 | Store project documents privately | PROPOSED |
| G7 | Let the studio update the website without a developer | CONFIRMED (brief) |

## 5. Constraints

- Core PHP + MySQL/MariaDB + Bootstrap 5, no heavy frameworks [CONFIRMED].
- XAMPP for development, cPanel shared hosting for production [CONFIRMED].
- Website and ERP on the same hosting account and domain [CONFIRMED].
- Domain and hosting provider not yet chosen [PENDING – Q-H1, Q-H2].
- Budget/timeline not supplied [PENDING].

## 6. Key assumptions (to validate)

- A1: The studio is small (1–5 ERP users). [ASSUMPTION]
- A2: Currency is INR only; Indian number formatting (1,10,000). [ASSUMPTION]
- A3: Area unit is sq.ft by default, possibly sq.m too. [ASSUMPTION]
- A4: English is the website language; Marathi may be wanted. [ASSUMPTION → Q-W8]
- A5: Single office/branch. [ASSUMPTION]
- A6: The studio provides design and supervision services, not construction. [ASSUMPTION → Q-S2]

## 7. Where things stand

Stage 0 documentation is complete and awaiting review. Next: client answers to
`docs/CLIENT_QUESTIONS.md`, then Stage 1 (architecture + database design for approval).
````

---

## B.3 `project-context/BUSINESS_REQUIREMENTS.md`

````markdown
# Business Requirements

Status tags: **[CONFIRMED]** (in brief or references) · **[PROPOSED]** (our recommendation) ·
**[ASSUMPTION]** · **[PENDING]** (question ID in `docs/CLIENT_QUESTIONS.md`).

"CONFIRMED (brief)" means the developer brief requires it; the client has not yet
validated it against their workflow.

---

## 1. Current situation (as understood)

- No website; online presence is the Instagram profile @ar.ajkumbhar. [CONFIRMED]
- Quotations appear to be typed as documents (Word/PDF) with a letterhead and a
  manually numbered reference ("Ref: 1/2025"). [ASSUMPTION from the sample]
- How enquiries, payments, expenses and documents are tracked today is unknown. [PENDING – Q-G1]

## 2. Proposed core business flow [PROPOSED]

```
Website form / WhatsApp / phone / walk-in / referral
          │
          ▼
     ENQUIRY ──► follow-ups ──► (lost / dropped)
          │ converted
          ▼
     CLIENT ──► PROJECT (site, type, area)
                   │
                   ▼
              QUOTATION (draft → revision n → sent → accepted/rejected)
                   │ accepted
                   ▼
              FEE SCHEDULE / BILLS ──► PAYMENTS & RECEIPTS
                   │
                   ├── project stages & site visits
                   ├── documents (drawings, 3D, municipal)
                   ├── expenses
                   └── (optional) publish to PORTFOLIO
```

Whether this matches the studio's real sequence (e.g. are projects opened before
the quotation?) is **[PENDING – Q-G2]**.

## 3. Public website requirements

| ID | Requirement | Status |
|---|---|---|
| W-01 | Public pages without login: Home, About Studio, Services, Portfolio, Project Details, Gallery, Contact, Enquiry | CONFIRMED (brief) |
| W-02 | Premium, professional look aligned with logo colours | CONFIRMED |
| W-03 | Responsive: mobile, tablet, desktop | CONFIRMED |
| W-04 | High-quality project galleries | CONFIRMED |
| W-05 | Contact details + WhatsApp enquiry button | CONFIRMED (number PENDING – Q-W4) |
| W-06 | Enquiry form saved into ERP | CONFIRMED |
| W-07 | SEO-friendly URLs, meta tags, sitemap | CONFIRMED |
| W-08 | Portfolio and selected page content editable from ERP | CONFIRMED |
| W-09 | Email notification to studio on new enquiry | PROPOSED (PENDING – Q-W6) |
| W-10 | Google Map of office | PROPOSED (PENDING – Q-W3) |
| W-11 | Testimonials | PROPOSED, only with real client consent (PENDING – Q-W7) |
| W-12 | Marathi language version | PENDING – Q-W8 |
| W-13 | Spam protection on forms (honeypot + rate limit; no CAPTCHA by default) | PROPOSED |

## 4. ERP requirements

| ID | Requirement | Status |
|---|---|---|
| E-01 | Separate secure login at `/erp/login` | CONFIRMED |
| E-02 | Role-based access for authorized users only | CONFIRMED |
| E-03 | Enquiry management (website + manual) with status and follow-ups | CONFIRMED (brief) |
| E-04 | Client master | CONFIRMED (brief) |
| E-05 | Project management (site, type, area, status, stages) | CONFIRMED (brief) |
| E-06 | Service / work-category master (configurable, not hardcoded) | CONFIRMED (brief) |
| E-07 | Quotations: configurable calculation, PDF, print, revisions, approval status | CONFIRMED (brief) |
| E-08 | Design fees and billing | CONFIRMED (brief); billing model PENDING – Q-F1..F5 |
| E-09 | Payments and receipts | CONFIRMED (brief); receipt format PENDING – Q-F6 |
| E-10 | Expenses | CONFIRMED (brief); scope PENDING – Q-F8 |
| E-11 | Project documents and attachments (private) | CONFIRMED (brief) |
| E-12 | Portfolio and gallery management | CONFIRMED |
| E-13 | Follow-ups and reminders | CONFIRMED (brief); channel PENDING – Q-G5 |
| E-14 | Reports | CONFIRMED (brief); list PENDING – Q-R1 |
| E-15 | User and role management | CONFIRMED (brief); roles PENDING – Q-U1 |
| E-16 | Organization settings (letterhead, numbering, tax, terms) | CONFIRMED (brief) |
| E-17 | Audit log of important operations | CONFIRMED |
| E-18 | Financial corrections via reversal, never silent overwrite | CONFIRMED |
| E-19 | Site-visit log against a project (date, stage, notes, photos) | PROPOSED (sample lists many visit stages) – PENDING Q-P3 |
| E-20 | Client portal / client login | NOT IN SCOPE unless requested – Q-G6 |

## 5. Quotation business rules

| ID | Rule | Status |
|---|---|---|
| Q-R01 | Calculation methods: area-based, fixed fee, item-wise, custom charges | PROPOSED |
| Q-R02 | Rate, area unit, rounding are entered per quotation, with optional defaults in settings | PROPOSED |
| Q-R03 | No hardcoded ₹100/sq.ft or 1100 sq.ft | CONFIRMED |
| Q-R04 | GST/tax, discounts, payment schedule, validity, terms: configurable, default **off/blank** until approved | CONFIRMED (brief) |
| Q-R05 | Scope of work built from service categories with editable sub-items (as in sample sections 1–6) | PROPOSED |
| Q-R06 | Every change after "sent" creates a new revision; old revisions read-only | PROPOSED |
| Q-R07 | Statuses: Draft, Sent, Revised, Accepted, Rejected, Expired, Cancelled | PROPOSED – Q-Q8 |
| Q-R08 | Reference number format configurable (sample: `1/2025`) | PROPOSED – Q-Q1 |
| Q-R09 | Amount in words on PDF (Indian system) | PROPOSED – Q-Q6 |

## 6. Non-functional requirements

| ID | Requirement | Status |
|---|---|---|
| N-01 | Works on cPanel shared hosting (PHP 8.1+, MySQL 5.7+/MariaDB 10.4+) | PROPOSED |
| N-02 | Pages load fast on mobile data; images optimized, lazy-loaded | PROPOSED |
| N-03 | Documented backup and restore | CONFIRMED |
| N-04 | Installation, user, testing and deployment guides | CONFIRMED |
| N-05 | Time zone Asia/Kolkata, INR, Indian number format | ASSUMPTION |
| N-06 | Accessibility: WCAG 2.1 AA contrast and keyboard navigation for public site | PROPOSED |

## 7. Explicitly not assumed

The following are **not** requirements unless the client confirms them:
construction execution/contracting, material procurement or resale, turnkey
interiors, vendor/contractor payments, payroll, inventory, GST filing, online
payment gateway, client portal, mobile app, multi-branch, multi-currency.
````

---

## B.4 `project-context/MODULES.md`

````markdown
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
````

---

## B.5 `project-context/DATABASE_RULES.md`

````markdown
# Database Rules

These rules govern the future `database.sql` and `sample_data.sql`.
**No schema is created in Stage 0.** The schema design is a Stage 1 deliverable
that must be approved before implementation.

## 1. Engine and encoding
- MySQL 5.7+ / MariaDB 10.4+ (to be checked against the chosen host — Q-H2).
- `ENGINE=InnoDB`, `CHARSET utf8mb4`, `COLLATE utf8mb4_unicode_ci` (Marathi/Devanagari safe).
- Connection time zone `+05:30`; PHP `date_default_timezone_set('Asia/Kolkata')`.
- Store `DATETIME` values in IST consistently (single-region business).

## 2. Naming
- Tables: lowercase snake_case, plural (`clients`, `projects`, `quotation_items`).
- Primary key: `id INT UNSIGNED AUTO_INCREMENT` (BIGINT for audit/log tables).
- Foreign keys: `<singular>_id` (`client_id`), real `FOREIGN KEY` constraints, `ON DELETE RESTRICT`
  for business data.
- Booleans: `TINYINT(1)` named `is_*` / `has_*`.
- Statuses: `VARCHAR(30)` validated in PHP against constants (or lookup table), not ENUM, so
  new statuses don't need ALTER TABLE. Final choice in Stage 1.
- Indexes on every FK, status columns, date columns used in reports, and unique business numbers.

## 3. Standard columns
Every master and transaction table:
```
created_at  DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
created_by  INT UNSIGNED NULL
updated_at  DATETIME NULL ON UPDATE CURRENT_TIMESTAMP
updated_by  INT UNSIGNED NULL
```
Soft-deletable tables additionally:
```
deleted_at  DATETIME NULL
deleted_by  INT UNSIGNED NULL
```

## 4. Money, area and rates
- **DECIMAL only. Never FLOAT/DOUBLE.**
  - Money: `DECIMAL(14,2)`.
  - Rates: `DECIMAL(12,2)` (rate per sq.ft/sq.m or per item).
  - Area: `DECIMAL(12,2)` + `area_unit` (`sqft` / `sqm`).
  - Percentages: `DECIMAL(5,2)`.
  - Quantities: `DECIMAL(10,2)`.
- PHP arithmetic on money uses `bcmath` (or integer paise) — never float. Check `bcmath` availability on host (Q-H2).
- Rounding rule configurable (none / nearest rupee / nearest 10). Applied once, at total level, and stored.
- Totals are **stored** on the document (snapshot), and recomputable for verification.

## 5. Soft deletion
- Ordinary master records (clients, projects, services, users, portfolio items, masters)
  use `deleted_at`. Default queries filter `deleted_at IS NULL`.
- A record referenced by financial transactions cannot be soft-deleted without ADM override
  and audit entry; normally it is made **inactive** instead.
- Hard delete is only for: spam website enquiries (after retention), temp upload files.

## 6. Financial integrity
- Financial records: bills/invoices, payments/receipts, payment allocations, expenses,
  credit notes, reversals.
- **Never silently overwrite or delete** a posted financial record.
- Correction = reversal record (negative amount, `reverses_id` → original) + new correct record,
  with mandatory reason.
- Drafts may be edited; once **issued/posted** the row is immutable except status fields
  (enforced in PHP; optional DB triggers decided in Stage 1).
- Optional "lock date": nothing dated on/before it can be added or reversed without ADM.
- Document numbers (quotation, bill, receipt) are generated inside a transaction from a
  `number_sequences` table with `SELECT … FOR UPDATE`; unique index on the number;
  numbers are never reused, cancelled documents keep their number.

## 7. Quotation revisions
- `quotations` (header, current status, current revision no.) + `quotation_revisions`
  (frozen snapshot: dates, scope text, lines, area, rate, method, totals, terms) +
  `quotation_revision_items`.
- A sent revision is read-only. Editing creates revision n+1.
- Accepted revision ID is stored on the project fee agreement.

## 8. Audit log
- `audit_logs`: `id, user_id, action, module, record_type, record_id, summary,
  old_values JSON NULL, new_values JSON NULL, ip_address, user_agent, created_at`.
- Written by a single helper; append-only (no UPDATE/DELETE from the app).
- Login success/failure, password changes, role changes, financial postings/reversals,
  quotation status changes, portfolio publish/unpublish, document downloads (optional), backups.

## 9. Files
- DB stores metadata only: original name, stored (random) name, relative path, MIME,
  size, SHA-256 hash, uploader, linked record. File bytes stay on disk.
- Public portfolio images and private documents use different storage roots
  (see `SECURITY_RULES.md` §5).

## 10. Scripts
- `database.sql`: full schema + required seed (roles, permissions, default settings,
  number sequences, masters marked as reference). **No real client data.**
- `sample_data.sql`: fictitious demo data only — no real names from the sample
  quotation (e.g. not "Uttekar"), no real phone numbers.
- First admin user created by an install step or documented one-time procedure, with a
  forced password change; no well-known default password in production.
- Schema changes after first release: numbered migration files
  (`migrations/2027_01_15_001_add_x.sql`) and `database.sql` kept in sync.
- XAMPP version includes `CREATE DATABASE`; cPanel instructions explain importing
  into the pre-created database.

## 11. Backups
- Daily automated `mysqldump` via cPanel cron to a non-public folder, rotated (e.g. 7 daily, 4 weekly).
- Weekly off-site copy (method PENDING Q-H4).
- Restore procedure documented and **tested** before go-live.
````

---

## B.6 `project-context/SECURITY_RULES.md`

````markdown
# Security Rules

Mandatory for all code. A feature is not "done" until these are satisfied.

## 1. Separation of public site and ERP
- One codebase, one database, **two entry areas**: public (`/`) and ERP (`/erp/`).
- Public code may read **only published portfolio/content data** and may **insert** website
  enquiries. It never includes ERP controllers or queries ERP tables.
- Every ERP request passes through a single bootstrap that enforces: session valid →
  user active → permission for this module/action. No ERP page is reachable without it.
- ERP pages send `X-Robots-Tag: noindex, nofollow`; `/erp/` is disallowed in `robots.txt`
  (defence in depth only — not a security control).
- Optional (PROPOSED): two DB users — `ajds_public` (SELECT on published content, INSERT on
  enquiries) and `ajds_erp` (full DML). Decide in Stage 1 based on host limits.

## 2. Files outside the web root
- `config/` (DB credentials, secrets), `app/` (PHP classes/includes), `storage/`
  (private documents, logs, backups, temp) live **above** `public_html`.
- If a host forbids this, fallback: same folders inside the web root with `Require all denied`
  `.htaccess` + an index guard — documented as the weaker option.
- Never commit real credentials; `config/config.sample.php` in repo, real `config.php` excluded.
- `display_errors=Off` in production; errors logged to `storage/logs/`.
- Block web access to `*.sql, *.md, *.log, *.ini, *.bak, *.zip, .env, .git` and directory listing.

## 3. Authentication
- `password_hash()` (PASSWORD_DEFAULT) / `password_verify()`; rehash when needed.
- Minimum password policy: 10+ chars (PROPOSED), not equal to username.
- Lockout / throttling: e.g. 5 failures → 15-minute lock per account + per-IP throttling.
- Generic error message ("Invalid username or password").
- `session_regenerate_id(true)` on login and privilege change.
- Password reset: random 32-byte token, store **hash** of token, 30–60 min expiry, single use.
- No default credentials in production; no `fix_login.php`-style reset scripts deployed.
- Optional 2FA (TOTP) for Admin — PENDING Q-U3.

## 4. Sessions and cookies
- ERP session name e.g. `AJDS_ERP`, cookie path `/erp`, `HttpOnly`, `Secure` (HTTPS),
  `SameSite=Lax` (Strict if no cross-site links needed), `session.use_strict_mode=1`.
- Idle timeout (e.g. 30 min, configurable) and absolute timeout (e.g. 10 h).
- Public site uses no login session; if a session is needed (CSRF on enquiry form) it uses
  a different cookie name scoped to `/`.
- Logout via POST with CSRF; destroy session and cookie.

## 5. Uploads
| | Public portfolio images | Private project documents |
|---|---|---|
| Storage | `public_html/uploads/portfolio/` (web-served) | `storage/documents/` (outside web root) |
| Delivery | Direct URL | `erp/download.php?id=` after permission check, `Content-Disposition: attachment` |
| Allowed | JPG, PNG, WebP | PDF, JPG, PNG, WebP, DWG? DOCX? XLSX? (Q-D1) |
- Validate extension whitelist **and** MIME via `finfo`, and for images `getimagesize()`.
- Re-encode images with GD/Imagick (removes payloads and EXIF/GPS).
- Random stored file names (`bin2hex(random_bytes(16))`); original name kept only in DB.
- Size limits configurable; check `upload_max_filesize`/`post_max_size` on host.
- Upload dirs: `.htaccess` disabling PHP/script execution (`RemoveHandler`, `php_flag engine off`
  where supported, `Require all denied` for `*.php*`), no directory listing.
- Never use user input in file paths; resolve and verify paths stay inside the storage root.

## 6. Requests and output
- **CSRF** token (per session, `hash_equals`) on every POST/PUT/DELETE incl. AJAX and the public enquiry form.
- State changes only via POST.
- **Server-side validation** of every field (type, length, range, allowed values); client-side is convenience only.
- **PDO prepared statements** only; `ATTR_EMULATE_PREPARES=false`; whitelist column names for sorting.
- **Output escaping**: `htmlspecialchars(…, ENT_QUOTES, 'UTF-8')` by default; rich text from
  ERP (About page etc.) sanitized with an allow-list.
- AJAX endpoints return JSON, check auth + permission + CSRF, never leak stack traces.

## 7. HTTP headers (both areas)
`Strict-Transport-Security` (after HTTPS confirmed), `X-Content-Type-Options: nosniff`,
`X-Frame-Options: SAMEORIGIN` / CSP `frame-ancestors 'self'`, `Referrer-Policy: strict-origin-when-cross-origin`,
a Content-Security-Policy appropriate to each area, `Permissions-Policy`. Force HTTPS redirect.

## 8. Authorization
- Permission checks server-side on every action (not just hiding menu items).
- Record-level checks where needed (e.g. SITE role sees only assigned projects — PENDING).
- Financial reversals, user/role changes, settings, backups: ADM only (default).

## 9. Public form abuse
- Honeypot field, minimum fill time, per-IP rate limit, length limits, strip links count.
- No CAPTCHA by default (PROPOSED); add only if spam becomes a problem (Q-W6).
- Notification emails: never use visitor input in headers.

## 10. Privacy
- Website enquiries contain personal data: store only what is needed, ERP access only,
  retention period PENDING (Q-G7). Privacy notice link near the form.
- Portfolio publishes only with client consent; location shown at city/area level, not
  full address; no client names unless approved.
- India's DPDP Act 2023 considerations to be reviewed with the client — not legal advice.

## 11. Audit, logging, backup
- Audit log per `DATABASE_RULES.md` §8.
- Application error log in `storage/logs/`, rotated; never displayed to users.
- Backups stored outside web root; DB backup downloads ADM-only and audited.

## 12. Dependencies
- Minimal: Bootstrap 5, (optional) a PDF library such as Dompdf or mPDF bundled with the
  release (decision in Stage 1 — Q-T1). Pin versions; record them in the docs.
- No CDN for ERP assets (PROPOSED) — bundle locally; public site may use local copies too.
````

---

## B.7 `project-context/UI_UX_GUIDELINES.md`

````markdown
# UI / UX Guidelines

## 1. Brand source
- Only source: `reference/logo/Logo.jpeg` (1600×1034, JPEG, opaque charcoal background).
- **Do not redraw, recolour, re-typeset, stretch or add effects to the logo.**
- Request from client: original vector (AI/SVG/PDF/CDR) or a transparent PNG (Q-B1).
  Until then, derivatives are made **only by cropping/resizing** the supplied JPEG,
  keeping its charcoal background.

### Planned logo derivatives (made in implementation stage, not now)
| Use | Plan |
|---|---|
| Website header | Full logo crop (monogram + wordmark) on charcoal header band, ~48–64 px tall |
| ERP sidebar | Same crop on charcoal sidebar; collapsed state = monogram-only crop |
| Login screen | Full logo, larger, centred on charcoal panel |
| Favicon / app icon | Monogram-only square crop on charcoal, 32/180/192/512 px + `favicon.ico` |
| PDF letterhead | High-res crop; on white paper either keep charcoal block or use vector once supplied |
| Open Graph image | 1200×630 on charcoal with logo centred |

Note: the sample quotation letterhead uses a **red** text heading ("A J D E S I G N S T U D I O")
and "श्री" at top, not the logo. Which letterhead style the client wants on generated
PDFs is PENDING (Q-Q2).

## 2. Colour palette (PROPOSED; sampled from logo, to be approved — Q-B2)
| Token | Hex | Use |
|---|---|---|
| `--ajds-charcoal` | `#54545C` | Logo background, header/footer, ERP sidebar |
| `--ajds-charcoal-dark` | `#3A3A40` | Text on light, hover states, footer |
| `--ajds-copper` | `#AF7B4C` | Primary accent, buttons, links, highlights |
| `--ajds-copper-dark` | `#8E5F36` | Button hover, small text on light backgrounds (contrast) |
| `--ajds-tan` | `#A78A5E` | Secondary accent (from logo detail), dividers |
| `--ajds-ivory` | `#F7F4EF` | Light neutral page background |
| `--ajds-stone` | `#E8E3DB` | Section alternation, cards, borders |
| `--ajds-white` | `#FFFFFF` | Cards, forms |
| Status colours | Bootstrap success/warning/danger/info, slightly desaturated | ERP badges only |

Contrast rule: copper `#AF7B4C` on white is below 4.5:1 for body text — use it for large
text, icons and buttons with white/charcoal text checked; use `--ajds-copper-dark` for small copper text.
All text must meet WCAG AA.

## 3. Typography (PROPOSED — Q-B2)
- Headings: a clean geometric/architectural sans or elegant serif — candidates
  *Montserrat* / *Jost* (sans) or *Cormorant Garamond* (serif) — self-hosted, max 2 families.
- Body: *Inter* / *Source Sans 3*, 16 px base, 1.6 line-height.
- Uppercase + letter-spacing for small section labels echoes the logo's spaced capitals.
- Devanagari fallback (*Noto Sans Devanagari*) if Marathi content is approved (Q-W8).

## 4. Public website look & feel
- Image-first, generous white space, restrained copy, thin lines and grid alignment.
- Full-bleed hero image/slider (real project photos only — none supplied yet).
- Portfolio grid with consistent aspect-ratio crops; hover reveals title + category.
- Project details: large cover, facts strip (category, location, year, services), story,
  gallery with lightbox (keyboard + swipe).
- Sticky header, transparent over hero then charcoal on scroll; mobile off-canvas menu.
- Floating WhatsApp button (bottom-right), click-to-call on mobile.
- Subtle motion only (fade/slide on scroll), respect `prefers-reduced-motion`.
- No stock photos presented as studio work. Placeholder images during development must be
  clearly marked and removed before launch.

## 5. ERP look & feel
- Bootstrap 5 admin layout: charcoal left sidebar with logo, light ivory content area, white cards.
- Copper primary buttons; status badges consistent across modules.
- Data tables: search, filter, sort, pagination (server-side for large lists), CSV export.
- Forms: grouped sections, required-field markers, inline validation messages, sticky Save bar on long forms.
- Money right-aligned, Indian grouping (₹1,10,000.00); dates `DD/MM/YYYY` (matches sample) — Q-G8.
- Confirmation dialogs for destructive/irreversible actions (cancel bill, reverse payment).
- Fully usable on tablet; key screens (enquiries, follow-ups, site visits) usable on mobile.

## 6. Print / PDF documents
- A4 portrait, letterhead header, footer with contact line and page numbers.
- Quotation layout mirrors sample order: letterhead → Ref/Date → project title → scope sections
  → fee summary → signature block. Improvements (table for fees, client block, terms) PROPOSED.
- Amount in words (Indian system: lakh/crore).

## 7. Accessibility & performance
- Semantic HTML, alt text required on every published image (ERP enforces).
- Keyboard focus visible, form labels, colour not the only status indicator.
- Responsive images (`srcset`, WebP + JPEG fallback), lazy loading, target LCP < 2.5 s on 4G.
````

---

## B.8 `project-context/DEVELOPMENT_ROADMAP.md`

````markdown
# Development Roadmap

Each stage ends with an **approval gate**. Do not start a stage before the previous gate
is approved and recorded in §5.

## 1. Stages

| Stage | Name | Deliverables | Gate |
|---|---|---|---|
| **0** | Discovery & documentation | `CLAUDE.md`, `project-context/*`, `docs/*`, client question list | Developer review + client answers to priority questions |
| **1** | Architecture & database design | Final module list (after necessity review), ER diagram, table-by-table schema doc (no SQL yet or SQL draft for review), role/permission matrix, folder structure, URL map, quotation calculation spec, PDF library choice, wireframes for key pages | Written approval of architecture + DB design |
| **2** | Foundation | Git init, folder skeleton, config, bootstrap, DB helper, auth (login/logout/reset), roles/permissions, CSRF, layout (public + ERP), audit log helper, `database.sql` v1, installer/first-admin procedure | Login + security checklist tested |
| **3** | Masters & settings | Organization settings, website content settings, service categories/items, project types, sources, payment modes, expense categories, users & roles UI | Module tests pass |
| **4** | Public website | All public pages, portfolio listing/details, gallery, enquiry form → DB, WhatsApp, SEO basics | Client review of design on staging |
| **5** | Portfolio CMS | Portfolio projects, image upload/processing, ordering, featured, publish | Client uploads a real project end-to-end |
| **6** | CRM | Enquiries (incl. website), follow-ups, clients, dashboard v1 | Module tests pass |
| **7** | Projects & documents | Projects, stages, site-visit log (if approved), private documents | Module tests pass |
| **8** | Quotations | Builder, calculation methods, revisions, status, print/PDF | Client approves PDF format with real example |
| **9** | Fees, payments, expenses | Fee agreement/schedule, bills, payments, allocation, receipts, reversals, expenses | Financial test cases pass |
| **10** | Reports & dashboard v2 | Agreed report list, exports | Client sign-off |
| **11** | Hardening & QA | Security review, cross-browser/device tests, performance, backup/restore drill, `sample_data.sql` | Test report |
| **12** | Deployment & handover | cPanel deployment, SSL, cron backups, user training, guides, final ZIP `AJ_Design_Studio_Portfolio_ERP.zip` | Client acceptance |

Stages 4–5 (website) and 6–9 (ERP) can be reordered if the client wants the website
live first (PENDING Q-G9). A **Phase 1 launch** of website + portfolio CMS + website
enquiries before the full ERP is a reasonable option.

## 2. Testing approach (per module)
- Manual test checklist per module stored in `docs/testing/` (to be created in Stage 2).
- Security checks: auth bypass, CSRF, SQLi, XSS, upload abuse, direct file URL access.
- Financial calculation test cases (area × rate, rounding, tax on/off, revisions, reversals).
- Results recorded with date and environment. **No test is reported as passed unless executed.**

## 3. Environment
- Dev: XAMPP on Windows (PHP and MySQL not on shell PATH; XAMPP path to confirm).
- Staging: optional subfolder/subdomain on client hosting, password-protected (Q-H3).
- Production: cPanel on client's hosting, HTTPS.

## 4. Version control
- Folder is **not yet a Git repo**. Initialise at Stage 2 start (Stage 1 if docs should be versioned now).
- `.gitignore`: `config/config.php`, `storage/*` (except `.gitkeep`), `public_html/uploads/*`, backups, ZIPs.
- Commit at each stage gate; tag releases.

## 5. Decision log

| Date | Decision | Decided by | Reference |
|---|---|---|---|
| 2026-11-06 | Stage 0 documentation produced; awaiting review | CodInt Digitech | this commit/set |
| — | Final service list | Client | Q-S1 |
| — | Quotation format & fee rules | Client | Q-Q*, Q-F* |
| — | Roles & users | Client | Q-U1 |
| — | Hosting / domain | Client | Q-H1, Q-H2 |

## 6. Risks
| Risk | Mitigation |
|---|---|
| No portfolio photos yet | Collect early (Q-W1); website can launch with fewer, high-quality projects |
| Logo only as JPEG | Request vector; use careful crops meanwhile |
| Scope creep (construction/contracting features) | Out-of-scope list in `docs/PROJECT_SCOPE.md`; change requests |
| Shared hosting limits (PHP version, file size, cron, bcmath, GD) | Verify host capabilities in Stage 1 (Q-H2) |
| Financial data errors | Reversal-only corrections, audit log, test cases |
````

---

## B.9 `docs/PROJECT_SCOPE.md`

````markdown
# Project Scope

Project: AJ Design Studio – Portfolio Website + ERP Management System
Developer: CodInt Digitech · Client: AJ Design Studio · Principal Architect: Ar. Ajit Kumbhar
Version: 0.1 draft (2026-11-06) – **not approved**

## 1. Confirmed information
- The client has **no existing website**; a new public portfolio website will be built. (brief)
- A private ERP will be built; both on the **same hosting account and domain**:
  `/` public, `/erp/` ERP, `/erp/login` login. Domain to be configured later. (brief)
- Stack: Core PHP, MySQL/MariaDB, PDO, Bootstrap 5, HTML5/CSS3/JS, AJAX where required,
  XAMPP dev, cPanel deployment. (brief)
- Studio identity: Architect, Interior Designer; Patan (Karad–Chiplun Road), Satara district;
  phone 8806956877; email ar.ajitkumbhar16@gmail.com. (quotation letterhead, Instagram)
- Reference work categories (from sample quotation): floor plans, working drawings,
  municipal drawings, exterior 3D, interior design layouts, interior 3D, construction-stage
  site visits, material and colour selection.
- Sample quotation is a **dummy**, not the final template or pricing policy. (brief)
- Final deliverable list and ZIP name. (brief)

## 2. In scope (proposed, subject to approval)

### 2.1 Public website
Home · About Studio · Services · Portfolio · Project Details · Gallery · Contact · Enquiry form ·
WhatsApp enquiry · SEO (meta, sitemap, schema) · responsive design · content from ERP.

### 2.2 ERP
Dashboard · Enquiries (incl. website) · Clients · Projects (+ site-visit log) · Services &
work categories · Quotations (configurable, revisions, approval, PDF/print) · Fees & billing ·
Payments & receipts · Expenses · Project documents (private) · Portfolio & gallery CMS ·
Follow-ups & reminders · Reports · Users & roles · Organization settings · Audit log.
Module necessity ratings: `project-context/MODULES.md`.

### 2.3 Non-functional
Security controls (`project-context/SECURITY_RULES.md`), backups and restore, documentation set,
installation on XAMPP and cPanel, sample data (fictitious).

## 3. Out of scope (unless the client requests and approves a change)
- Construction execution, contracting, material procurement/resale, vendor/contractor
  billing, labour/payroll, inventory.
- GST return filing / accounting ledger / Tally integration.
- Online payment gateway.
- Client login portal.
- Native mobile apps.
- SMS/WhatsApp Business API automation.
- Content writing and professional photography (client supplies texts and photos; we can
  structure and proof-read).
- Domain purchase, hosting purchase, business email setup (we can advise).
- Migration of historical data (unless provided as spreadsheets — Q-G10).

## 4. Assumptions
- Small team (1–5 ERP users); single office.
- INR only; Indian number format; dates DD/MM/YYYY; FY April–March.
- English website and ERP for v1; Marathi optional.
- The client provides: photos, project descriptions, approval to publish each project,
  final service list, about-studio text, quotation terms.
- Hosting supports PHP 8.1+, MySQL/MariaDB, HTTPS, cron, GD, mbstring, bcmath, `finfo`.

## 5. Pending client decisions
All tracked in `docs/CLIENT_QUESTIONS.md`. Highest priority:
1. Final service list and what "Temple Work", "कोकण शिल्प" and "Complete Project" mean for the website.
2. Fee/billing model (area rate vs fixed, stages, GST registration, receipts).
3. Users and roles.
4. Portfolio content availability and publishing consent.
5. Domain and hosting.
6. Website-first phased launch or everything together.

## 6. Acceptance (proposed)
Each stage gate in `project-context/DEVELOPMENT_ROADMAP.md` is accepted in writing.
Final acceptance: running application on production hosting, documents delivered,
backup/restore demonstrated, final ZIP handed over.
````

---

## B.10 `docs/QUOTATION_ANALYSIS.md`

````markdown
# Quotation Analysis

Source: `reference/quotation-samples/work pfd & fees structure.pdf` (2 pages).
**Status: dummy/sample supplied for reference. Not an approved template or pricing policy.**
Client-identifying content from the sample (e.g. the project/client surname) must not be
used in demo data or on the website.

## 1. Structure of the sample (as read)

| # | Element | Content in sample | Notes |
|---|---|---|---|
| 1 | Invocation | "श्री" (Devanagari, red) at top centre | Cultural header; keep as configurable option |
| 2 | Letterhead title | "A J D E S I G N S T U D I O" in red spaced capitals | Not the logo; logo not used |
| 3 | Profession line | "ARCHITECT / INTERIOR DESIGNER" | |
| 4 | Address | AJ Design Studio, Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan | |
| 5 | Contact | Contact no. 8806956877, E-mail ar.ajitkumbhar16@gmail.com | |
| 6 | Reference | "Ref: 1/2025" | Format appears `{sequence}/{year}` |
| 7 | Date | 15/12/2025 | DD/MM/YYYY |
| 8 | Title | "<Surname> BUNGLOW PROJECT" (underlined) | Project name; "Buglow" typo in title |
| 9 | Sub-title | "DESIGN WORK" | Document type |
| 10 | Intro line | "This is drawings for <Surname> Bunglow at Karad." | Project + location |
| 11 | Scope sections 1–6 | Numbered categories with bullet sub-items (see §2) | Core of the document |
| 12 | Inclusion statement | "This works & visits are includes design fees" | All scope included in one fee |
| 13 | Fee block | Total area 1100 sq.f; design fees 100 ru. per square foot; total 1,10,000 | Area-based |
| 14 | Signature | "Ar. Ajit kumbhar (Principal Architect)" | No signature image/stamp |

## 2. Work categories and items in the sample

1. **All floor plans** — Ground floor plan; First floor plan; Second floor plan; Terrace plan.
2. **Working drawings** — Sections; Elevations; Municipal drawing.
3. **3D work** — Exterior 3D.
4. **Interior design** — Floor plan with furniture layout; Ceiling layout; Electrical layout;
   Tiles layout; Plumbing layout; Room-wise sectional elevation; Furniture working drawings.
5. **Interior 3D** — Living room, Kitchen, Bedrooms.
6. **Site visits** — Centerline layout; Footing layout checking; PCC level; Wall construction level;
   7′ construction level; Slab checking; Plaster work checking; Tiles fitting checking;
   Interior work; Ceiling design; Electrical layout checking; Furniture layout explanation visit;
   Material selection; Colour selection; Surprise visits.

Observations:
- Floor-plan items depend on the number of floors → should be generated/edited per project, not fixed.
- Interior 3D rooms vary per project → editable list.
- Site visits are listed as **stages**, without a number of visits → visit count/limits unknown.
- "Municipal drawing" sits under working drawings; whether municipal **approval liaison** is included is unknown.
- Spelling in sample (Buglow, Muncipal, explaination, "sq.f", "ru.") — the system should use
  corrected standard text; the client should confirm wording.

## 3. Fee calculation in the sample

```
Total area        = 1100 sq.ft          (which area? built-up / carpet / plot — unknown)
Rate              = ₹100 per sq.ft       (single rate covering ALL six sections)
Design fee total  = 1100 × 100 = ₹1,10,000
```
- One composite rate covers architecture + interiors + 3D + site visits.
- No per-category break-up, no tax, no discount, no rounding visible.
- Amount written with Indian grouping (1,10,000), no "₹" symbol, no amount in words.

**These figures are sample values only. Nothing in the system will default to 1100 or ₹100.**

## 4. What is missing from the sample

| Missing item | Why it matters |
|---|---|
| Client name, address, contact | Needed for a formal quotation and later billing |
| Site address / plot details | Only "at Karad" |
| Area basis (built-up / carpet / plot / per floor) | Directly drives the fee |
| Area unit choice (sq.ft vs sq.m) | |
| Per-category fee break-up | Needed if client may accept only part of the scope |
| GST / tax treatment, GSTIN, SAC code | Depends on registration status |
| Payment schedule / stages | Needed for billing and reminders |
| Validity of quotation | |
| Number of design revisions included | Common dispute area |
| Number of site visits included; extra-visit charge | Sample lists stages but no count |
| Exclusions (structural design, MEP design, liaison fees, printing, travel, govt. fees) | |
| Additional-area / scope-change rule | |
| Terms & conditions, cancellation, ownership/copyright of drawings | |
| Bank / UPI details | If wanted on quotation |
| Acceptance section (client signature) | For approval tracking |
| Amount in words | Common on Indian commercial documents |
| Page numbers / quotation version | Needed for revisions |
| Logo on letterhead | Sample uses text heading only |

## 5. Proposed configurable quotation model [PROPOSED]

**Header:** quotation no. (format configurable, sample-like `{seq}/{yyyy}`), revision no., date,
validity (optional), client, project, site location, area + area basis + unit, subject, intro text.

**Scope:** categories → items, picked from Service master, all text editable per quotation,
add/remove/reorder, optional per-item "included / optional / excluded" marker.

**Fee lines — methods (combinable):**
| Method | Formula | Example usage (illustrative only) |
|---|---|---|
| Area-based | area × rate per unit | Composite design fee as in sample |
| Area-based per category | area × category rate | Architecture rate + interior rate |
| Fixed fee | lump sum | Small renovation, temple work |
| Item-wise | qty × rate | n interior 3D views, n extra visits |
| Custom charge | free text + amount | Travel, plotting |

**Optional blocks (all OFF by default until approved):** discount (amount / %), tax lines
(configurable rate, name, SAC), rounding rule, payment schedule (stage, %, or amount),
terms & conditions, exclusions, bank details, client acceptance block, amount in words.

**Lifecycle:** Draft → Sent → (Revised n) → Accepted / Rejected / Expired / Cancelled.
Each sent revision frozen; history and comparison available; who/when/remark on each status change.

**Output:** print-ready HTML + PDF (A4), letterhead from Settings, signature block configurable
(default text "Ar. Ajit Kumbhar, Principal Architect" — pending confirmation of exact wording).

**After acceptance:** accepted revision becomes the project's fee agreement; payment schedule
(if used) generates expected milestones for billing and reminders.

## 6. Questions for the client
See `docs/CLIENT_QUESTIONS.md` §4 (Q-Q*) and §5 (Q-F*).
````

---

## B.11 `docs/CLIENT_QUESTIONS.md`

````markdown
# Client Questions (master list)

For: Ar. Ajit Kumbhar, AJ Design Studio · Prepared by CodInt Digitech · 2026-11-06
Priority: **P1** = needed before architecture/DB approval · **P2** = needed before the module is built · **P3** = can wait.
Record answers in the "Answer" column and copy decisions into the decision log
(`project-context/DEVELOPMENT_ROADMAP.md` §5).

## 1. General workflow (G)
| ID | Pri | Question | Answer |
|---|---|---|---|
| Q-G1 | P1 | How do you track enquiries, quotations, payments, expenses and drawings today (register, Excel, WhatsApp, Tally)? | |
| Q-G2 | P1 | What is your usual sequence: enquiry → site visit → quotation → advance → design…? When do you consider something a "project"? | |
| Q-G3 | P3 | The folder contains `WorkLedger_Multilingual_EN_HI_MR.zip` (an earlier CodInt app). Should it be used as a reference (style / Marathi-Hindi support), or is it unrelated? *(internal question for CodInt)* | |
| Q-G4 | P2 | Should website enquiries go into the same enquiry list as phone/walk-in enquiries (recommended) or a separate inbox? | |
| Q-G5 | P2 | How should reminders reach you: ERP dashboard only, daily email, or other? | |
| Q-G6 | P3 | Do clients need to log in to see their drawings/payments (client portal)? (Currently out of scope.) | |
| Q-G7 | P3 | How long should enquiry data of non-converted leads be kept? | |
| Q-G8 | P3 | Date format DD/MM/YYYY and financial year April–March — correct? | |
| Q-G9 | P1 | Launch the website first (with portfolio management) and the ERP later, or everything together? | |
| Q-G10 | P2 | Do you have existing data to import (client list, ongoing projects, payments)? In what format? | |

## 2. Services (S)
| ID | Pri | Question | Answer |
|---|---|---|---|
| Q-S1 | P1 | Please confirm the final list of services and sub-items. The sample shows: floor plans, working drawings, municipal drawings, exterior 3D, interior design layouts, interior 3D, site visits, material & colour selection. Anything to add/remove (e.g. landscape, renovation, structural coordination, valuation, vastu)? | |
| Q-S2 | P1 | Instagram highlights mention **Temple Work**, **कोकण शिल्प** and **Complete Project**. What do these mean? Do you undertake construction/execution or turnkey work, or only design and supervision? | |
| Q-S3 | P2 | Project types to use (Bungalow, Mini bungalow, Residential apartment, Commercial, Interior only, Temple, Other)? | |
| Q-S4 | P2 | Which services should appear on the website, and with what description? | |

## 3. Website (W) and brand (B)
| ID | Pri | Question | Answer |
|---|---|---|---|
| Q-W1 | P1 | Which completed projects can be shown? Please provide photos/renders (high resolution), title, category, location (city), year, short description. | |
| Q-W2 | P2 | Keep a separate "Gallery" page in addition to "Portfolio", or merge them? | |
| Q-W3 | P1 | Exact office address and Google Maps location to publish; office hours. | |
| Q-W4 | P1 | WhatsApp number for the website (same as 8806956877?). Which email to publish? | |
| Q-W5 | P1 | Do you have permission from clients to publish their projects? Should client names be shown or hidden? | |
| Q-W6 | P2 | Who receives website enquiry email notifications? Accept CAPTCHA if spam occurs? | |
| Q-W7 | P3 | Any testimonials (with client permission)? Awards, registrations (e.g. Council of Architecture registration no.) to display? | |
| Q-W8 | P2 | Website language: English only, or English + Marathi? ERP language? | |
| Q-B1 | P1 | Do you have the logo as a vector (AI/SVG/PDF/CDR) or transparent PNG? | |
| Q-B2 | P2 | Approve proposed colours (charcoal `#54545C`, copper `#AF7B4C`, ivory background) and font style (modern sans vs elegant serif). | |
| Q-W9 | P2 | About Studio text: profile, experience, team, philosophy, photo of the principal — please supply or approve a draft we write from your notes. | |

## 4. Quotation (Q)
| ID | Pri | Question | Answer |
|---|---|---|---|
| Q-Q1 | P1 | Quotation number format: keep `1/2025` style (resets yearly? calendar or financial year?) or another format? | |
| Q-Q2 | P1 | Letterhead: use the logo, or the red text heading as in the sample? Keep "श्री" at the top? | |
| Q-Q3 | P1 | Which area is the fee based on: built-up, carpet, plot, or total of all floors? sq.ft only or also sq.m? | |
| Q-Q4 | P1 | Is the rate usually one composite rate for everything, or separate rates for architecture, interiors, 3D, site visits? | |
| Q-Q5 | P1 | Do you also quote fixed lump-sum fees or item-wise charges (e.g. per 3D view, per extra visit)? | |
| Q-Q6 | P2 | Show amount in words? Show client address/contact? Add client acceptance signature block? | |
| Q-Q7 | P1 | Standard terms: validity, revisions included, number of site visits included, extra-visit charges, exclusions, cancellation, drawing ownership. Please share your standard text if any. | |
| Q-Q8 | P2 | Statuses you need (Draft, Sent, Revised, Accepted, Rejected, Expired, Cancelled)? Who can approve/send a quotation? | |
| Q-Q9 | P2 | Should a quotation be sendable by email from the ERP, or only downloaded as PDF and shared on WhatsApp? | |
| Q-Q10 | P3 | Signature image/stamp on PDF? Exact signature wording ("Ar. Ajit Kumbhar, Principal Architect")? | |

## 5. Fees, billing, payments, expenses (F)
| ID | Pri | Question | Answer |
|---|---|---|---|
| Q-F1 | P1 | Do you issue bills/invoices, or only collect payments against the quoted total? | |
| Q-F2 | P1 | Payment stages you usually use (e.g. advance, after plans, after working drawings, during construction)? % or amounts? | |
| Q-F3 | P1 | Is the studio GST-registered? If yes: GSTIN, rate, SAC code, invoice format needs. | |
| Q-F4 | P2 | Discounts: do you give them? Should discount need approval? | |
| Q-F5 | P2 | Are extra charges billed separately (extra visits, travel, printing/plotting)? | |
| Q-F6 | P1 | Do you give payment receipts? Format and numbering? | |
| Q-F7 | P2 | Payment modes used (Cash, UPI, bank transfer, cheque, others)? | |
| Q-F8 | P2 | Which expenses to track: office expenses, project-wise expenses, or both? Any reimbursement from clients? | |

## 6. Projects & documents (P, D)
| ID | Pri | Question | Answer |
|---|---|---|---|
| Q-P1 | P2 | Project stages/statuses you want to see. | |
| Q-P2 | P2 | Project code format (e.g. `AJ-2026-001`)? | |
| Q-P3 | P2 | Should site visits be logged in the ERP (date, stage, notes, photos)? Are visits limited per project? | |
| Q-D1 | P2 | File types to store (PDF, JPG, DWG, SKP, DOCX, XLSX…) and largest typical file size. | |

## 7. Users & reports (U, R)
| ID | Pri | Question | Answer |
|---|---|---|---|
| Q-U1 | P1 | Who will use the ERP (names/roles: principal, office staff, accountant, site engineer, junior architects)? What may each see/do? Can staff see fees and payments? | |
| Q-U2 | P2 | Will users access the ERP on mobile at site? | |
| Q-U3 | P3 | Want two-step login (authenticator app) for the admin account? | |
| Q-R1 | P2 | Which reports do you need most (enquiries, outstanding fees, collections, expenses, project status, profitability)? | |

## 8. Hosting & technical (H, T)
| ID | Pri | Question | Answer |
|---|---|---|---|
| Q-H1 | P1 | Domain name: already owned? Preferred name? | |
| Q-H2 | P1 | Hosting provider/plan (cPanel)? PHP version, MySQL/MariaDB version, storage limit, cron and SSL availability. | |
| Q-H3 | P3 | Allow a password-protected staging copy for review? | |
| Q-H4 | P2 | Off-site backup destination (Google Drive download by admin, email, second server)? Who is responsible for backups after handover? | |
| Q-H5 | P2 | Business email on the domain (e.g. info@domain) for sending notifications? | |
| Q-T1 | P2 | *(internal)* PDF library choice — Dompdf vs mPDF (Devanagari support favours mPDF). | |
````

---

## B.12 `docs/PORTFOLIO_WEBSITE_PLAN.md`

````markdown
# Portfolio Website Plan

Status: **[PROPOSED]** — no UI pages are created in Stage 0.
Content rule: **no invented projects, services, statistics, awards or testimonials.**
All copy and images come from the client or from approved drafts.

## 1. Goals
1. Present AJ Design Studio as a premium architecture & interior practice.
2. Showcase real work through strong photography and renders.
3. Convert visitors into enquiries (form, WhatsApp, call).
4. Be found in local search (Patan, Karad, Satara region — keywords to confirm).

## 2. Sitemap and URLs (pretty URLs via `.htaccess`)

| Page | URL | Source of content |
|---|---|---|
| Home | `/` | Settings → Website content + featured portfolio |
| About Studio | `/about` | Settings → About (client text, Q-W9) |
| Services | `/services` | Service categories with "show on website" flag |
| Portfolio | `/portfolio` (+ `?category=`) | Published portfolio projects |
| Project Details | `/portfolio/{slug}` | One portfolio project + gallery |
| Gallery | `/gallery` | Published gallery images (may merge with Portfolio — Q-W2) |
| Contact | `/contact` | Settings → contact block, map |
| Enquiry | `/enquiry` (also embedded on Contact/Home) | Form → ERP enquiries |
| Thank you | `/enquiry/thank-you` | Static, noindex |
| Privacy notice | `/privacy` | Approved text |
| 404 | — | Branded page |
| System | `/sitemap.xml`, `/robots.txt` | Generated |

## 3. Page plans

### Home
- Hero: full-width real project image(s), studio name, one-line positioning (client-approved), CTA "Start your project" + WhatsApp.
- Short intro (2–3 lines) → link to About.
- Services overview (icons/cards for approved categories).
- Featured projects grid (3–6, from ERP "featured").
- Process strip (e.g. Consultation → Design → Drawings → Site supervision) — only if client confirms process.
- Enquiry CTA band; footer.

### About Studio
- Studio profile, principal's profile and photo, philosophy, (registration no. if provided),
  service area. No made-up numbers ("100+ projects") unless the client supplies them.

### Services
- One section per approved category with sub-items (e.g. from sample: architectural plans,
  working & municipal drawings, exterior 3D, interior design layouts, interior 3D, site supervision,
  material & colour selection) — **only after Q-S1 confirmation**.
- CTA to enquiry with service pre-selected.

### Portfolio
- Category filter (categories configurable, e.g. Bungalow, Interior, Temple… pending Q-S3).
- Grid of cover images, title, location (city), year. Pagination or "load more".

### Project Details
- Cover image, title, facts strip (category, location, year, services, optional area),
  description, gallery with lightbox, previous/next project, enquiry CTA.
- Schema.org `CreativeWork`/`ImageGallery` markup, OG image = cover.

### Gallery
- Masonry/grid of all published images with category filter and lightbox, each linking to its project.

### Contact
- Address, phone (click-to-call), WhatsApp, email, map embed (lazy-loaded), office hours, enquiry form.

### Enquiry form (fields — PROPOSED)
Name*, Mobile*, Email, City/site location, Project type, Services interested (multi-select),
Approx. area + unit, Message, preferred contact method; consent tick for privacy notice.
Hidden honeypot + timestamp; CSRF token. On submit → saved as enquiry (source = Website),
optional email notification to studio, thank-you page. No auto-reply to visitor by default (Q-W6).

### WhatsApp enquiry
Floating button + Contact page button: `https://wa.me/91XXXXXXXXXX?text=<encoded message>`;
number from Settings (Q-W4). Optionally logs a "WhatsApp click" event (count only, no personal data).

## 4. Content managed from ERP
| Content | ERP location |
|---|---|
| Portfolio projects, images, order, featured, publish | Portfolio module |
| Gallery images | Portfolio module (images flagged for gallery) |
| Services text | Service master (website fields) |
| Home hero, intro, about text, contact block, social links, SEO defaults | Settings → Website content |
| Enquiries | Enquiry module |

## 5. SEO plan
- Unique `<title>` and meta description per page/project (editable, with defaults).
- Clean slugs, canonical URLs, HTTPS only, one H1 per page.
- `sitemap.xml` generated from published content; `robots.txt` disallows `/erp/`.
- Schema.org `LocalBusiness`/`ProfessionalService` (name, address, phone, geo, sameAs Instagram).
- Open Graph + Twitter cards (cover images).
- Image alt text mandatory; WebP + responsive sizes; lazy loading.
- Google Business Profile & Search Console setup advice at launch (client's account).

## 6. Responsive behaviour
- Mobile first; breakpoints per Bootstrap 5.
- Mobile: off-canvas menu, single-column grids, sticky call/WhatsApp bar.
- Tablet: 2-column grids. Desktop: 3–4 column grids, wide hero.

## 7. Content checklist for launch (client to provide)
- [ ] 4–10 best projects with 5–20 good images each, details and publishing consent
- [ ] About text and principal photo
- [ ] Final services list and descriptions
- [ ] Address, map pin, phone, WhatsApp, email, office hours
- [ ] Logo vector/transparent file
- [ ] Privacy notice approval
- [ ] Domain and hosting

## 8. Design direction
Per `project-context/UI_UX_GUIDELINES.md`: charcoal + copper on light neutrals, image-first,
architectural grid, restrained typography, subtle motion.
````

---

## B.13 `docs/TECHNICAL_REQUIREMENTS.md`

````markdown
# Technical Requirements

Status: **[PROPOSED]** for approval in Stage 1. No code is written in Stage 0.

## 1. Stack
| Layer | Choice |
|---|---|
| Language | Core PHP 8.1+ (8.2/8.3 preferred), no framework |
| Database | MySQL 5.7+/8.0 or MariaDB 10.4+, InnoDB, utf8mb4 |
| DB access | PDO, prepared statements, `ERRMODE_EXCEPTION`, no emulated prepares |
| Front end | Bootstrap 5 (bundled locally), HTML5, CSS3 (custom properties), vanilla JS, `fetch()` AJAX |
| PDF | Dompdf or mPDF bundled in `vendor/` (decision Q-T1; mPDF if Devanagari text like "श्री" is needed) |
| Images | GD (or Imagick if available) for resize/re-encode/WebP |
| Math | `bcmath` for money (fallback: integer paise) |
| PHP extensions required | pdo_mysql, mbstring, fileinfo, gd, bcmath, openssl, json, intl (optional) |
| Dev | XAMPP (Windows) |
| Prod | cPanel shared hosting, Apache, HTTPS (AutoSSL/Let's Encrypt), cron |

Composer is used only to fetch the PDF library during development; the release ZIP ships
`vendor/` so cPanel needs no Composer.

## 2. Same hosting account: how the website and ERP coexist

### 2.1 Principle
One hosting account, one domain, **one codebase and one database**, with two front
doors. Only small entry scripts and public assets sit inside the web root; everything
sensitive sits beside it, unreachable by URL.

### 2.2 Production layout on cPanel (recommended)
```
/home/<cpaneluser>/
├── ajds_app/                      ← NOT web-accessible
│   ├── config/
│   │   └── config.php             DB credentials, secrets, paths, env = production
│   ├── app/
│   │   ├── core/                  bootstrap, DB, Router, Auth, Csrf, Validator, Audit, Upload, Money
│   │   ├── public/                public-site controllers + views
│   │   ├── erp/                   ERP module controllers + views (one folder per module)
│   │   └── shared/                helpers, layouts, PDF templates
│   ├── storage/
│   │   ├── documents/             private project documents
│   │   ├── logs/
│   │   ├── backups/               cron mysqldump output
│   │   ├── cache/  tmp/
│   ├── vendor/                    PDF library
│   └── database/                  database.sql, migrations/ (reference copy)
│
└── public_html/                   ← web root (https://<domain>/)
    ├── index.php                  public front controller → requires ../ajds_app/app/core/bootstrap.php
    ├── .htaccess                  HTTPS, pretty URLs, security headers, deny sensitive extensions
    ├── assets/                    css, js, fonts, images, logo variants, favicon
    ├── uploads/portfolio/         PUBLIC processed images only (.htaccess: no script execution)
    ├── robots.txt   (sitemap.xml generated dynamically)
    └── erp/
        ├── index.php              ERP front controller → same bootstrap, ERP mode
        └── .htaccess              rewrite /erp/login, /erp/dashboard … to index.php; noindex header
```
- `/erp/login` and `/erp/dashboard` are clean URLs rewritten to `erp/index.php`.
- Both front controllers locate the app via a single path constant (`APP_ROOT`) — the only
  line to change if the host layout differs.
- Private documents are streamed by `erp/index.php?route=documents/download&id=…` after
  authentication and permission checks — never by direct URL.
- If the domain is an **addon domain** with its own document root (e.g. `/home/user/domain.com/`),
  `ajds_app/` still sits in `/home/user/`, outside that root.

### 2.3 Fallback if the host forbids files above the web root
`public_html/ajds_app/` with `Require all denied` in its `.htaccess`, plus a startup check that
refuses to run if `config/` is web-reachable. Documented as weaker; avoid if possible.

### 2.4 XAMPP development layout
```
C:\xampp\htdocs\ajds\              (= public_html)  → http://localhost/ajds/ and /ajds/erp/login
C:\xampp\ajds_app\                 (= ajds_app, outside htdocs)
```
A `BASE_URL` setting supports running in a sub-folder locally and at domain root in production.

### 2.5 Shared vs separate
| Concern | Shared | Separate |
|---|---|---|
| Database | One DB | Optional separate DB users for public (limited) vs ERP (full) |
| Config | One `config.php` | Area-specific settings (session name, CSP) in bootstrap |
| Code | Core libs, models, settings, layouts partials | Public controllers/views vs ERP controllers/views |
| Sessions | — | ERP cookie `AJDS_ERP`, path `/erp`; public has no login session |
| Assets | Bootstrap, fonts, logo | `assets/public/*` vs `assets/erp/*` |
| Uploads | — | Public portfolio in web root; private docs in `storage/` |
| Errors/logs | One log dir | Tagged by area |

## 3. Request flow
```
Browser → Apache (.htaccess: HTTPS, rewrite, headers)
        → public_html/index.php or public_html/erp/index.php
        → ajds_app/app/core/bootstrap.php (config, error handling, session per area, DB)
        → Router → [ERP: Auth + Permission + CSRF middleware] → Controller → Model (PDO) → View
        → Response (HTML / JSON for AJAX / PDF / file stream)
```

## 4. Coding conventions
- PSR-12 style, `declare(strict_types=1)`, simple PSR-4-like autoloader (no framework).
- One folder per ERP module: controller, model/repository, views, validation rules.
- All SQL in model/repository classes; no SQL in views.
- Escape output by default (`e()` helper); CSRF field helper in forms.
- Money via a `Money` helper (bcmath, Indian formatting, amount in words).
- Constants for statuses; settings read from DB `settings` table with cache.
- No secrets, real client data or generated uploads in Git.

## 5. Email
- PHP `mail()` via host or SMTP (domain mailbox, Q-H5) through a small mailer class;
  used for password reset, enquiry notification, optional reminder digest.

## 6. Cron jobs (cPanel)
| Job | Frequency |
|---|---|
| DB backup (`mysqldump` → `storage/backups/`, gzip, rotate) | Daily |
| Files backup of `storage/documents` + `uploads/` (tar.gz, rotate) | Weekly |
| Reminder digest email (if approved) | Daily morning |
| Cleanup temp files, expired reset tokens, old spam enquiries | Daily |

## 7. Backup and restore strategy
- **What:** database; `storage/documents/`; `public_html/uploads/`; `config/config.php` (kept securely, not in normal backups shared by email).
- **Where:** `storage/backups/` (outside web root) + weekly off-site copy (Q-H4) + cPanel's own backups if the plan has them.
- **Retention (proposed):** 7 daily, 4 weekly, 3 monthly.
- **Restore:** documented steps for (a) full restore to new hosting, (b) DB-only restore via phpMyAdmin/`mysql`, (c) single-file document recovery. Restore drill performed before go-live.
- ERP Settings → "Download backup" for ADM (audited).

## 8. Deployment (outline; full guide in Stage 12)
1. Create MySQL DB + user(s) in cPanel; import `database.sql`.
2. Upload `ajds_app/` to home directory and `public_html/` contents to web root.
3. Copy `config.sample.php` → `config.php`; set DB, base URL, mail, environment.
4. Set folder permissions (755 dirs / 644 files; `storage` and `uploads` writable by PHP).
5. Run first-admin setup; force password change; remove/lock installer.
6. Enable AutoSSL, force HTTPS; set cron jobs; verify security headers and that
   `/ajds_app/…`, `.sql`, `config` are not reachable.
7. Smoke test public site, enquiry form, ERP login, upload, PDF.

## 9. Host capability checklist (to verify in Stage 1 — Q-H2)
PHP ≥ 8.1 selectable · required extensions · MySQL/MariaDB version · ability to place
folders outside `public_html` · `upload_max_filesize`/`post_max_size` · `memory_limit` (PDF) ·
cron · AutoSSL · disk quota for documents and backups · outgoing mail limits.
````

---

*End of review package. Source documents were not modified in producing it.*
