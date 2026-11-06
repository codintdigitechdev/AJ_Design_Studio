# Stage 1 Gap-Resolution Package — Index and Corrections

| | |
|---|---|
| Project | AJ Design Studio — Portfolio Website + ERP |
| Prepared | 2026-11-06 by CodInt Digitech (draft) |
| Status | **DRAFT — PENDING APPROVAL.** Nothing in this package is approved. |
| Inputs | `CLAUDE.md`, `project-context/*.md`, `docs/*.md`, `docs/STAGE1_REVIEW_PACKAGE.md`, `docs/STAGE1_REVIEW_PACKAGENew.md` |

## 0. Ground rules for this package

- **No original document was edited.** Corrections are written here as *proposed errata*
  with the exact change to make. The original files are updated only after the developer
  approves them and the approval is recorded in the decision log
  (`project-context/DEVELOPMENT_ROADMAP.md` §5). This follows `CLAUDE.md` §3 and §10.
- **No assumption is approved here.** Where this package has to pick a design to stay
  consistent, it says **PROPOSED DEFAULT** and **PENDING APPROVAL**. Each design is built so
  that it still works if the client answers differently.
- **No PHP, SQL or other application code.** The database diagram uses Mermaid notation, and
  the wireframes are text drawings.
- Status markers:
  - **CONFIRMED-REF** – stated in a supplied reference file (logo, sample quotation,
    Instagram).
  - **BRIEF-UNVERIFIED** – see §2.
  - **PROPOSED** – a developer recommendation, not yet approved.
  - **ASSUMPTION** – a working assumption that still has to be checked.
  - **PENDING APPROVAL** – needs a client or developer decision. `Q-…` IDs refer to
    `docs/CLIENT_QUESTIONS.md`; `D-…` IDs refer to the developer decisions in
    `docs/STAGE1_ROADMAP_AND_DECISIONS.md`.

## 1. Package contents

| # | Task | File |
|---|---|---|
| 1 | Fix inconsistencies between the business workflow and the module definitions | this file §3 |
| 2 | Re-qualify requirements marked CONFIRMED (brief) | this file §2 |
| 3 | Role × module permission matrix | `docs/PERMISSION_MATRIX.md` |
| 4 | Enquiry → project → quotation workflow | `docs/WORKFLOWS.md` Part A |
| 5 | Financial workflow (advances, allocation, refunds, reversals) | `docs/WORKFLOWS.md` Part B |
| 6 | Duplicate modules and optional-feature dependencies | this file §4–§5 |
| 7 | Database diagram and table-by-table design | `docs/DATABASE_DESIGN.md` |
| 8 | ERP page/URL list and field specifications per module | `docs/ERP_PAGES_AND_FIELDS.md` |
| 9 | Public website and ERP wireframes | `docs/WIREFRAMES.md` |
| 10 | Updated roadmap and all decisions still open | `docs/STAGE1_ROADMAP_AND_DECISIONS.md` |

---

## 2. Re-qualifying "CONFIRMED (brief)" requirements

### 2.1 Problem
Many requirements are tagged CONFIRMED because the **developer brief** says so, but the brief
itself is not in the project folder. A reviewer cannot check these requirements against their
source. The client has also never checked them against how the studio actually works
(`BUSINESS_REQUIREMENTS.md` header).

### 2.2 New tag — PROPOSED (D-01)

| Tag | Meaning | Can it be used as a basis for design? |
|---|---|---|
| **CONFIRMED-REF** | Stated in a supplied reference that is on disk | Yes |
| **BRIEF-UNVERIFIED** | Comes from the developer brief, which is not on file | Yes, provisionally. It becomes CONFIRMED only when (a) the brief is added to `reference/brief/`, or (b) the developer re-affirms it in writing in the decision log |
| **CLIENT-CONFIRMED** | The client approved it in writing | Yes |

### 2.3 Re-qualification table
Every item below changes from CONFIRMED / CONFIRMED (brief) to **BRIEF-UNVERIFIED — PENDING
APPROVAL (developer re-affirmation, D-01)**. The last column says whether the client also
has to confirm it.

| Source item | Requirement | Client check also needed? |
|---|---|---|
| OVERVIEW §1 | The studio has no existing website | Yes — trivial |
| OVERVIEW §5, CLAUDE §8 | Stack: Core PHP, MySQL/MariaDB, Bootstrap 5, XAMPP, cPanel | No (developer choice) |
| OVERVIEW §5, CLAUDE §1 | Website and ERP on one hosting account and one domain; `/erp/` URLs | Q-H1, Q-H2 |
| OVERVIEW G3, G4, G7 | Manage enquiries, clients and projects; quotations with revisions/approval; studio edits the website itself | Q-G1, Q-G2 |
| BUSINESS W-01..W-08 | Public pages, premium look, works on all screen sizes, galleries, WhatsApp, enquiry form into the ERP, SEO, content editable from the ERP | Q-W2, Q-W4 |
| BUSINESS E-01, E-02 | Separate secure login; role-based access | Q-U1 |
| BUSINESS E-03..E-16 | ERP modules: enquiries … settings | Yes — whether each module is needed (see §4) |
| BUSINESS E-17, E-18 | Audit log; financial corrections by reversal only | No (control requirement) |
| BUSINESS Q-R03, Q-R04 | No hardcoded rates; tax, discount, schedule and terms configurable and off by default | Q-Q*, Q-F* |
| BUSINESS N-03, N-04 | Backup/restore; set of guides | No |
| CLAUDE §7 | The sample quotation is a dummy | No — but the client should confirm it is not their real template (Q-Q2) |
| CLAUDE §11 | Final deliverables list and ZIP name | No |

**These stay CONFIRMED-REF** because they come from a reference file on disk:
- organization name, profession, address, phone, email, Instagram handle
- logo appearance and sampled colours
- the structure and content of the sample quotation
- the Instagram highlight titles

Even so, **publishing** any of these on the website stays PENDING APPROVAL (Q-W3, Q-W4,
`CLAUDE.md` §6).

### 2.4 Action needed
Either place the brief in `reference/brief/`, or re-affirm the BRIEF-UNVERIFIED rows above in
the decision log (D-01).

---

## 3. Inconsistencies between workflows and module definitions — proposed errata

Each item shows the conflict, the proposed correction, and the exact original files to update
once it is approved.

| # | Conflict | Where | Proposed correction | Status |
|---|---|---|---|---|
| C-01 | The business flow puts CLIENT → PROJECT **before** QUOTATION, but the quotation module says it is "created from an enquiry or project", and the enquiry status list has "Quotation sent" **before** "Converted". So a quotation can exist before there is a client or project | BUSINESS §2; MODULES §2, §6 | A quotation may be created from an **enquiry** (a prospect) or from a **project**. When an enquiry's quotation is accepted, the enquiry is converted into a client + project and the quotation is linked to that project. A project can also be opened first (for example, a repeat client). Full detail in `WORKFLOWS.md` A | PROPOSED — PENDING APPROVAL (Q-G2) |
| C-02 | The project status "Enquiry stage" duplicates the enquiry module | MODULES §4 | Replace it with **"Proposal"** — a project opened for an existing client before acceptance. Prospects stay in the enquiry module | PROPOSED — PENDING APPROVAL (Q-P1) |
| C-03 | The enquiry status "Site visit / meeting" happens before a project exists, but the site-visit log is tied to a project | MODULES §2, §4 | Pre-project meetings and site visits are logged as **enquiry activities** (type = meeting / site visit). The project site-visit log starts only after the project exists | PROPOSED |
| C-04 | "Revised" is listed as a quotation **status**, but revisions are also numbered R0, R1… | MODULES §6; BUSINESS Q-R07 | Drop "Revised" as a status. The header shows the current revision number, and the status applies to the current revision: Draft, Sent, Accepted, Rejected, Expired, Cancelled, plus **Superseded** for older revisions | PROPOSED — PENDING APPROVAL (Q-Q8) |
| C-05 | Module 12 says its inbox holds "WhatsApp-click submissions", but the website plan counts WhatsApp clicks only, with no personal data | MODULES §12; PORTFOLIO_PLAN §3 | A WhatsApp click is **never** an enquiry record — it only adds to a daily counter. WhatsApp conversations are entered **by hand** as enquiries with source = WhatsApp | PROPOSED |
| C-06 | Website enquiries (module 12) duplicate the enquiry module (module 2) | MODULES §2, §12 | Merge them (see §4, R-01) | PROPOSED — PENDING APPROVAL (Q-G4) |
| C-07 | Accepting a quotation "generates the fee schedule" and bills are a Core module, but whether the studio issues bills at all is unknown | MODULES §6, §7, §8; Q-F1 | Add a setting **billing mode**: (a) *Bills* — demand notes/invoices are issued and payments are allocated to them, or (b) *Agreement only* — payments are recorded against the project's fee agreement with no bills. Both modes are designed (`WORKFLOWS.md` B). The default stays PENDING | PROPOSED — PENDING APPROVAL (Q-F1) |
| C-08 | The dashboard and reports show "fees billed vs received", which has no meaning in *Agreement only* mode | MODULES §1, §14 | Show **Agreed / Billed / Received / Outstanding**. In *Agreement only* mode, Outstanding = Agreed − Received, and Billed is hidden | PROPOSED |
| C-09 | The enquiry form fields (preferred contact method, privacy-consent tick, services multi-select) are missing from the enquiry module's fields | PORTFOLIO_PLAN §3; MODULES §2 | Add `preferred_contact`, `consent_at`, and a link between enquiries and services to the enquiry module | PROPOSED |
| C-10 | The dashboard is open to "all roles", but the security rules say "SITE sees only assigned projects" | MODULES §1; SECURITY §8 | Dashboard widgets are filtered by permission and by record-level rules (`PERMISSION_MATRIX.md` §3) | PROPOSED — PENDING APPROVAL (Q-U1) |
| C-11 | The private document download URL is written two ways | SECURITY §5; TECH §2.2 | Use one ERP route: `/erp/documents/{id}/download`, served by the ERP front controller. Remove the separate `download.php` | PROPOSED (D-05) |
| C-12 | Git timing: Stage 1 (CLAUDE §10) vs Stage 2 (ROADMAP §4) | — | Set up Git **now (Stage 1)** so that these design documents are versioned | PENDING APPROVAL (D-02) |
| C-13 | Backup retention: "7 daily, 4 weekly" vs "7 daily, 4 weekly, 3 monthly" | DATABASE §11; TECH §7 | 7 daily / 4 weekly / 3 monthly, subject to the host's disk quota | PENDING APPROVAL (Q-H2, Q-H4) |
| C-14 | Payment reversal and refund: "reversal" covers bounced cheques and wrong entries, but nothing covers **money returned** to a client | MODULES §8 | Add a separate **refund** document type (`WORKFLOWS.md` B.6) | PROPOSED — PENDING APPROVAL (Q-F9, new) |
| C-15 | An advance "on account" can be recorded, but there is no rule for applying it to bills later | MODULES §8 | Add a client **credit balance** and a "allocate credit to bill" action (`WORKFLOWS.md` B.4) | PROPOSED |
| C-16 | An expense is flagged "reimbursable to client", but nothing turns it into a charge to the client | MODULES §9 | A reimbursable expense can be added as a line on the next bill. It is disabled unless both Q-F5 and Q-F8 are confirmed | PROPOSED — PENDING APPROVAL |
| C-17 | A site visit has a "chargeable flag", but nothing turns it into a charge | MODULES §4 | The same pattern as C-16: a chargeable visit can become a bill line. Disabled until Q-F5 and Q-P3 are answered | PROPOSED — PENDING APPROVAL |
| C-18 | Stage naming: the review packages say "Stage 1", the roadmap says Stage 0 | ROADMAP §1 | This package is the **Stage 1 (architecture & database design)** set. The decision log should record "Stage 0 accepted" before Stage 1 is reviewed | PENDING APPROVAL (D-03) |

---

## 4. Duplicate modules — resolution

| # | Duplicate or overlap | Resolution | Status |
|---|---|---|---|
| R-01 | Module 12 Website Enquiries vs module 2 Enquiries | **One enquiry module.** Website submissions arrive with status **"New – unreviewed"** and a "Website" badge. A review queue filter replaces the separate inbox. Mark-as-spam and mark-as-duplicate actions are kept | PROPOSED — PENDING APPROVAL (Q-G4) |
| R-02 | P3 Gallery vs P2 Portfolio | **One set of images.** A gallery image is a portfolio image with "show in gallery" switched on. The `/gallery` page stays optional | PROPOSED — PENDING APPROVAL (Q-W2) |
| R-03 | Project site visits vs enquiry meetings | Kept separate by stage (C-03) | PROPOSED |
| R-04 | "Website content" settings (module 16) vs Pages module (P1) | **One place to edit:** Settings → Website content holds the hero, intro, About, contact and SEO defaults. P1 only displays them | PROPOSED |
| R-05 | Notes on enquiries, the project timeline, and follow-ups | **One activity log** (notes, calls, meetings, status changes) per record, plus a separate **follow-ups** table for future tasks with due dates | PROPOSED |
| R-06 | Audit log vs activity log | The audit log is the technical record (append-only, ADM only). The activity log is business notes that users write. Both are kept, with different purposes | PROPOSED |
| R-07 | Simple master lists (sources, project types, payment modes, expense categories, document categories, visit stages, area units) | Stored in **one generic lookup table**, not seven separate tables. Services stay a dedicated two-level master | PROPOSED — PENDING APPROVAL (D-06) |
| R-08 | Status lists (enquiry, project, quotation, bill) | Fixed workflow statuses are defined in the code. Labels can be renamed in Settings, but statuses cannot be added (adding one would change the workflow) | PROPOSED — PENDING APPROVAL (D-07) |

---

## 5. Optional features and what they depend on

Each optional feature must have a setting that switches it on or off. The system must work
correctly with the feature off.

| Feature | Rating | Depends on | Effect when OFF | Decision |
|---|---|---|---|---|
| Bills / invoices | Core (mode) | Fee agreement, numbering, Q-F3 (tax) | *Agreement only* mode: payments are recorded against the agreement, receipts are still issued | Q-F1 |
| GST / tax lines | Optional | Bills mode, GSTIN in settings | No tax columns on quotations or bills | Q-F3 |
| Payment schedule / milestones | Optional | Fee agreement | No milestones; reminders use follow-ups only | Q-F2 |
| Discounts | Optional | Quotations | Discount line hidden | Q-F4 |
| Approval of discounts / quotations | Optional | Permission "approve", discounts | No approval step: Draft → Sent directly | Q-Q8, Q-F4 |
| Refunds | Optional | Payments, client credit | Overpayment stays as client credit | Q-F9 |
| Expenses | Recommended | Lookups | Module hidden; profitability report unavailable | Q-F8 |
| Reimbursable expenses → bill | Optional | Expenses + Bills mode + Q-F5 | Flag hidden | Q-F5, Q-F8 |
| Site-visit log | Recommended | Projects, file storage | Tab hidden | Q-P3 |
| Chargeable visits → bill | Optional | Site visits + Bills mode + Q-F5 | Flag hidden | Q-F5, Q-P3 |
| Follow-ups & reminders | Recommended | Enquiries / quotations / projects / bills | Dashboard due-list empty | — |
| Daily email digest | Optional | Follow-ups, mail settings, cron | No emails | Q-G5, Q-H5 |
| Enquiry email notification | Proposed | Mail settings | Dashboard count only | Q-W6, Q-H5 |
| Send quotation by email | Optional | Mail settings, PDF | Download / print only | Q-Q9 |
| Profitability report | Optional | Expenses with a project link, Bills or Agreement | Report hidden | Q-R1 |
| Gallery page | Recommended | Portfolio images | `/gallery` returns "page not found"; menu item hidden | Q-W2 |
| Marathi website | Optional | Translatable content fields, Devanagari font, mPDF | English only | Q-W8 |
| Two-factor login for Admin | Optional | Users | Password only | Q-U3 |
| Lock date | Proposed | Financial modules | No lock | D-08 |
| Separate database logins | Proposed | Host support | One login | D-04 |
| Client portal, payment gateway, SMS/WhatsApp API | Out of scope | — | — | Q-G6 |

**Order to build in:**
- **Core:** Settings / lookups → Users → Services → Enquiries → Clients → Projects →
  Quotations → Fee agreement → Payments/receipts.
- **Optional add-ons:** Bills, tax, schedule, expenses, refunds, reports.
- Each optional add-on is built only after its decision has been made.
