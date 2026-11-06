# Stage 1 Consolidated Documentation Audit — Correction Report

| | |
|---|---|
| Project | AJ Design Studio — Public Portfolio Website + Private ERP |
| Developer | CodInt Digitech |
| Client | AJ Design Studio · Principal Architect: Ar. Ajit Kumbhar |
| Report date | 2026-11-06 |
| Report status | **AUDIT FINDINGS — NOT AN APPROVAL.** No existing document was modified. Stage 1 is **not** approved. |
| Scope | Every Markdown document in the working folder, the reference files, and the latest client decisions supplied with the audit brief |

**How to read the issue tables.** Every issue has an ID, the affected document(s), the existing
situation, the required correction, a priority (**Critical / High / Medium / Low**) and the
reason. ID prefixes:

| Prefix | Section | Prefix | Section |
|---|---|---|---|
| INC | §3 Document inconsistencies | PM | §8 Permission matrix |
| MR | §4 Missing requirements | PG | §9 ERP pages and fields |
| CD | §5 Client decisions | CM | §10 Contractor commission |
| DB | §6 Database design | RCD | §11 Remaining client decisions |
| WF | §7 Workflows | DD | §12 Developer decisions |

Priority meaning: **Critical** = Stage 1 cannot be approved until fixed · **High** = must be fixed
before the affected module is designed in detail · **Medium** = fix during document update ·
**Low** = editorial or minor.

---

## 1. Executive summary

1. **The Stage 1 design set exists and is mostly sound**, but it was written **before** the latest
   client decisions. Of 26 client decisions checked (§5), **6 are reflected, 10 are partly
   reflected, 6 are not reflected, and 4 are contradicted** by the current documents.
2. **Contractor / referral commission is completely absent** from the database design, workflows,
   permission matrix, pages, wireframes and reports. Two scope documents still say
   "vendor/contractor payments" are **out of scope** (CM-01). This is the largest single gap.
3. **"Financial information and decisions are Admin-only" is contradicted** throughout. The
   permission matrix, workflows, wireframes and module list give the ACC role full finance
   rights, let STF price and send quotations, and let STF/SITE post expenses (§8).
4. **Billing is designed as one studio-wide mode chosen once before go-live.** The client asked
   for a flexible design that is not limited to agreement-only billing (WF-01). GST is tied to
   "Bills" mode and set studio-wide, not per quotation or project (WF-02).
5. **Several calculation and data-model defects** would cause wrong balances if built as written:
   - an ambiguous outstanding formula (WF-05)
   - write-offs left out of balances (WF-06)
   - no credit definition in agreement-only mode (WF-07)
   - possible double counting of allocations to a milestone and to the bill made from it (DB-06)
   - a credit-note rule that blocks the main credit-note use case (WF-08)
   - a fee agreement created before its project exists (WF-04)
   - one-agreement-per-project uniqueness that blocks replacing a cancelled agreement (DB-08)
6. **Portfolio draft and unpublished images are publicly reachable**, because they are stored in
   the public uploads folder before consent and publishing (DB-16 / MR-09).
7. **Housekeeping debt:**
   - Errata C-01…C-18 from `STAGE1_GAP_RESOLUTION.md` were never applied to the original documents.
   - Two review packages are stale; one says the Stage 1 deliverables "do not exist" (INC-02, INC-03).
   - `CLAUDE.md` does not list 10 of the 22 documents (INC-05).
   - The decision log records no decisions (INC-07).
   - The folder is not a Git repository (INC-12).
8. **Readiness verdict: NOT READY for Stage 1 approval** (§14). There are **33 Critical**
   issues (grouped into 10 Critical checklist items in §13), plus P1 client decisions that
   are still open (§11), in particular the commission rules and GST status.

---

## 2. Repository files inspected

**Repository note.** The audit brief names the repository `codintdigitechdev/AJ_Design_Studio`,
but the working folder `R:\CID\Clients\AJ_Design_Studio` is **not a Git repository** (no `.git`),
and the GitHub CLI is not installed on this machine. The remote repository was therefore **not**
inspected. This audit covers the working folder only (INC-12).

| # | File | Lines | Last modified | Inspected | Notes |
|---|---|---|---|---|---|
| 1 | `CLAUDE.md` | 163 | 2026-11-06 18:26 | Full | Stage 0 charter; document map lists only 12 docs |
| 2 | `project-context/PROJECT_OVERVIEW.md` | 100 | 18:27 | Full | |
| 3 | `project-context/BUSINESS_REQUIREMENTS.md` | 117 | 18:27 | Full | |
| 4 | `project-context/MODULES.md` | 181 | 18:28 | Full | |
| 5 | `project-context/DATABASE_RULES.md` | 103 | 18:28 | Full | |
| 6 | `project-context/SECURITY_RULES.md` | 96 | 18:28 | Full | |
| 7 | `project-context/UI_UX_GUIDELINES.md` | 78 | 18:29 | Full | |
| 8 | `project-context/DEVELOPMENT_ROADMAP.md` | 61 | 18:29 | Full | |
| 9 | `docs/PROJECT_SCOPE.md` | 71 | 18:30 | Full | |
| 10 | `docs/QUOTATION_ANALYSIS.md` | 115 | 18:30 | Full | |
| 11 | `docs/CLIENT_QUESTIONS.md` | 95 | 18:36 | Full | 57 questions, all answer cells blank |
| 12 | `docs/PORTFOLIO_WEBSITE_PLAN.md` | 109 | 18:36 | Full | |
| 13 | `docs/TECHNICAL_REQUIREMENTS.md` | 138 | 18:36 | Full | |
| 14 | `docs/STAGE1_REVIEW_PACKAGE.md` | 1,779 | 18:54 | Part A full; Part B compared mechanically | Part B's 13 "verbatim" copies were checked: **all 13 are identical** to the current source files |
| 15 | `docs/STAGE1_REVIEW_PACKAGENew.md` | 576 | 19:04 | Full | Stale (INC-03) |
| 16 | `docs/STAGE1_GAP_RESOLUTION.md` | 175 | 19:08 | Full | Errata C-01…C-18, R-01…R-08 |
| 17 | `docs/PERMISSION_MATRIX.md` | 97 | 19:09 | Full | |
| 18 | `docs/WORKFLOWS.md` | 354 | 19:10 | Full | |
| 19 | `docs/DATABASE_DESIGN.md` | 537 | 19:12 | Full | 49 tables |
| 20 | `docs/ERP_PAGES_AND_FIELDS.md` | 440 | 19:15 | Full | |
| 21 | `docs/WIREFRAMES.md` | 383 | 19:15 | Full | |
| 22 | `docs/STAGE1_ROADMAP_AND_DECISIONS.md` | 176 | 19:15 | Full | D-01…D-23 |
| R1 | `reference/logo/Logo.jpeg` | — | 17:32 | Viewed | |
| R2 | `reference/quotation-samples/work pfd & fees structure.pdf` | 2 pp | 17:33 | Read earlier, rechecked against `QUOTATION_ANALYSIS.md` | |
| R3 | `reference/Visiting Card.jpeg` | — | 17:32 | Viewed | **Not mentioned in any document** (INC-09) |
| R4 | `reference/WorkLedger/WorkLedger_Multilingual_EN_HI_MR.zip` | — | — | File list only | Unrelated earlier app; nothing taken from it |
| R5 | `reference/portfolio/` | empty | — | Listed | Still no portfolio photos |

**Not in the folder:**
- `docs/STAGE1_GAP_RESOLUTION.md` is present, but no other "Stage 1 review package" exists
  beyond #14 and #15.
- The developer brief is not in the folder.
- No written record of the latest client decisions exists in the folder (INC-08).
- Nothing was taken from the separate CID Civil Site Inventory project.

---

## 3. Existing document inconsistencies

| ID | Affected document(s) | Existing situation | Required correction | Priority | Reason |
|---|---|---|---|---|---|
| INC-01 | `STAGE1_GAP_RESOLUTION.md` §3 vs `MODULES.md`, `BUSINESS_REQUIREMENTS.md`, `DATABASE_RULES.md`, `SECURITY_RULES.md`, `QUOTATION_ANALYSIS.md`, `CLIENT_QUESTIONS.md` | Errata C-01…C-18 and R-01…R-08 are proposed but **not applied**. The originals still contain the following: "Revised" as a quotation status (`MODULES` §6, `BUSINESS` Q-R07, `QUOTATION_ANALYSIS` §5, Q-Q8); "Enquiry stage" as a project status (`MODULES` §4); the separate Module 12 inbox; `erp/download.php` (`SECURITY` §5); "7 daily, 4 weekly" retention (`DATABASE_RULES` §11); and `quotation_revision_items` (`DATABASE_RULES` §7), whereas `DATABASE_DESIGN` uses `quotation_scope_items` + `quotation_fee_lines` | After approval, apply every accepted erratum to the originals in one pass, then mark `STAGE1_GAP_RESOLUTION.md` as "applied on <date>" | Critical | Two sources of truth: a developer building from `MODULES.md` would build the wrong statuses and tables |
| INC-02 | `STAGE1_REVIEW_PACKAGE.md` | Part A says the ER diagram, schema, permission matrix, URL map and wireframes are "not present". They now exist. Part B duplicates 13 source files (1,779 lines), identical today but bound to drift | Add a "SUPERSEDED by STAGE1_CONSOLIDATED_CORRECTION_REPORT.md — historical snapshot" banner. Do not use it as a reference. Do not delete it (rule) | High | A reviewer reading it would conclude Stage 1 has not started |
| INC-03 | `STAGE1_REVIEW_PACKAGENew.md` | Says "No schema has been designed yet" and the permission matrix "has not been produced yet". Lists "Revised", "Enquiry stage" and the ADM/ACC finance widgets. The file name is non-standard ("New") | Same SUPERSEDED banner. Future packages use dated names (`STAGE1_REVIEW_YYYY-MM-DD.md`) | High | Stale and contradicts the current design set |
| INC-04 | `STAGE1_GAP_RESOLUTION.md` §2 vs `CLAUDE.md` §3 | The gap package introduces new tags (CONFIRMED-REF, BRIEF-UNVERIFIED, CLIENT-CONFIRMED). `CLAUDE.md` §3 still defines only CONFIRMED / PROPOSED / ASSUMPTION / PENDING. The Stage 1 documents use "PENDING APPROVAL" | Adopt one tag set in `CLAUDE.md` §3: **CONFIRMED-REF**, **CLIENT-DECISION (date, source)**, **BRIEF**, **PROPOSED**, **ASSUMPTION**, **PENDING** — and apply it to every document | High | The latest client decisions need their own tag. Mixed tags make status unreliable |
| INC-05 | `CLAUDE.md` §2 | The document map lists 12 files and omits the 10 Stage 1 files (`DATABASE_DESIGN`, `PERMISSION_MATRIX`, `WORKFLOWS`, `ERP_PAGES_AND_FIELDS`, `WIREFRAMES`, `STAGE1_*` ×4, and this report). The "Current stage" line still says Stage 0 | Update the document map, the stage line and "Last updated" | High | `CLAUDE.md` is the entry point for every future session |
| INC-06 | `CLAUDE.md` §4, §6 · `PROJECT_OVERVIEW.md` §3, §5 · `PROJECT_SCOPE.md` §5 · `CLIENT_QUESTIONS.md` Q-H1 · `TECHNICAL_REQUIREMENTS.md` · `STAGE1_ROADMAP_AND_DECISIONS.md` Q-H1 | The domain is "to be configured later / PENDING Q-H1" everywhere | Record `ajdesignstudios.in` as a client decision (CD-01); keep the `<domain>` placeholder in config examples. See RCD-15 on spelling | High | Client decision not reflected |
| INC-07 | `DEVELOPMENT_ROADMAP.md` §5 | The decision log has one entry ("Stage 0 documentation produced", reference "this commit/set" — no commit exists). D-03 (accept Stage 0) is not recorded | Record Stage 0 acceptance (if given), each client decision CD-01…CD-26 with date and source, and each approved D-xx | Critical | `CLAUDE.md` §3 forbids treating anything as confirmed without a log entry; the gate cannot be evidenced |
| INC-08 | All | The latest client decisions exist only in the audit brief. There is no dated record in the folder of who said what, when, and how (meeting, call, WhatsApp) | Create one client-decision record (e.g. a new §6 "Client decisions received" in `CLIENT_QUESTIONS.md`, or a dated minutes file) with date, channel, and decision text. Fill the "Answer" column for the questions they settle | Critical | Prevents later disputes; required before tags can change |
| INC-09 | `CLAUDE.md` §4 · `PROJECT_OVERVIEW.md` §3 · `UI_UX_GUIDELINES.md` §1 | `reference/Visiting Card.jpeg` is in the folder but referenced nowhere. It contains facts that differ from the documents: **second phone 7796877369**; **"Sai Arked Building"** (quotation: "Sai Arcade Building"); full name "Ar. Ajit Arjun Kumbhar"; title "Architect & Interior Designer"; an Instagram QR code; a letter-spaced wordmark on the front; a copper back | Add it to the reference table. Record the discrepancies as RCD-04/05. Use it as the quotation letterhead reference (CD-13) | High | The client named the visiting card as a contact and design reference |
| INC-10 | `BUSINESS_REQUIREMENTS.md` §7 · `PROJECT_SCOPE.md` §3 · `STAGE1_REVIEW_PACKAGENew.md` §1.6 · `MODULES.md` necessity summary ("contractor/vendor tracking — Optional") | Contractor payments are explicitly out of scope | Re-scope: **commission to contractors / referral sources is in scope** (CM module). Construction-contractor payments, labour and procurement stay out of scope | Critical | Direct contradiction with the new requirement |
| INC-11 | `PROJECT_SCOPE.md` §3 ("content writing … out of scope; client supplies texts") · `PROJECT_SCOPE.md` §4 / review package A11 · `PORTFOLIO_WEBSITE_PLAN.md` §3 About ("client text") | The client now wants detailed website content based on the Instagram presence, with the client reviewing later | Re-scope: CodInt **drafts** website text from Instagram and the reference documents. Every draft is marked "pending client review" and is not published without the client's review (MR-07) | High | Scope and responsibility have changed |
| INC-12 | `CLAUDE.md` §10 vs `DEVELOPMENT_ROADMAP.md` §4 vs the audit brief | Git: "Stage 1" vs "Stage 2". The brief names a GitHub repository, but the local folder is not a Git repository | Decide D-02. If the GitHub repository exists, clone it or link this folder to it before any edit, and confirm which copy is authoritative (DD-01) | High | The audit cannot verify that the remote matches the local files; risk of divergent copies |
| INC-13 | `MODULES.md` §1 · `PERMISSION_MATRIX.md` row 1a · `WIREFRAMES.md` W-E2/W-E5 · `STAGE1_REVIEW_PACKAGENew.md` §2.2 | Finance widgets and the "Money" panel are shown to "ADM/ACC" | ADM only (PM-01) | Critical | Contradicts CD-25 |
| INC-14 | `WORKFLOWS.md` B.7 vs `ERP_PAGES_AND_FIELDS.md` §2.11 | Credit note: workflow says it is used "when a bill already has payments … if fully paid, the excess becomes credit". The field spec limits the amount to "≤ the bill's open value", which is 0 on a paid bill | See WF-08 | High | The two documents cannot both be implemented |
| INC-15 | `WORKFLOWS.md` A.6 vs `ERP_PAGES_AND_FIELDS.md` §2.10 | Quotation schedule lines "must add up to exactly 100% or the grand total". Fee milestones "must add up to the agreed fee — a warning, not a block" | One rule for both (WF-11) | Medium | Inconsistent validation |
| INC-16 | `DATABASE_DESIGN.md` §0 ("lookup FK … checked by the application") vs `DATABASE_RULES.md` §2 ("real FOREIGN KEY constraints") | It is unclear whether lookup references have a database FK | State: a real FK to `lookups.id`, **plus** an application check that the lookup row has the right `list_type` | Medium | Integrity rule ambiguity |
| INC-17 | `CLIENT_QUESTIONS.md` vs `STAGE1_ROADMAP_AND_DECISIONS.md` §4.1 | Q-F9, Q-F10, Q-F11 and Q-P4 are defined only in the roadmap file, "to be added once approved". Many questions are now partly answered by client decisions | Add the new questions. Mark answered or partly answered questions (see §5). Add the commission questions (RCD-01…RCD-08) | High | The client question list is the master list |
| INC-18 | `UI_UX_GUIDELINES.md` §1 · `WIREFRAMES.md` W-E7 · Q-Q2 | The letterhead is still "logo or red text heading — Q-Q2" | Record CD-13: the quotation uses the logo plus the visiting-card style. The "श्री" invocation stays an optional setting (RCD-11) | Medium | Decision received |

---

## 4. Missing requirements

| ID | Affected document(s) | Existing situation | Required correction | Priority | Reason |
|---|---|---|---|---|---|
| MR-01 | All design docs | No project source (Direct / Contractor), no contractor or referral master, no commission | Add the Contractor & Commission module (§10) to `BUSINESS_REQUIREMENTS`, `MODULES`, `DATABASE_DESIGN`, `WORKFLOWS`, `PERMISSION_MATRIX`, `ERP_PAGES_AND_FIELDS`, `WIREFRAMES` and the reports | Critical | New client requirement |
| MR-02 | `BUSINESS_REQUIREMENTS.md` §4 · `PERMISSION_MATRIX.md` | No requirement states "financial information and decisions are Admin-only". No definition of what counts as "financial" | Add a requirement (e.g. **E-21**) and a **financial-data definition**: fees, rates, quotation amounts and totals, discounts, tax amounts, agreements, variations, milestones, bills, credit notes, payments, allocations, credit, refunds, write-offs, expenses, commission (all fields), partner bank details, balances, profitability, finance settings, financial document categories, financial exports. RCD-09 confirms the edge cases | Critical | Without a definition, "Admin-only" cannot be enforced consistently |
| MR-03 | `BUSINESS_REQUIREMENTS.md` §5 · `WORKFLOWS.md` A.4 | "Admin must be able to modify rates" is not stated. The rate source and who may change a rate on a quotation line are not defined | Requirement: default rates live in the service master (Admin-only edit). Every quotation or bill line rate is editable **by Admin only**. Rates are snapshotted on the revision. No rate is mandatory or pre-filled unless the Admin sets a default | High | CD-17 |
| MR-04 | `BUSINESS_REQUIREMENTS.md` · `WORKFLOWS.md` B.3 | No requirement that billing must be flexible and not agreement-only | Requirement: the billing method is chosen **per project**, with a studio default. Bills may be issued with or without a fee agreement. Payments may be recorded with or without bills (WF-01) | Critical | CD-18 |
| MR-05 | `BUSINESS_REQUIREMENTS.md` · `DATABASE_DESIGN.md` · `WORKFLOWS.md` A.5 | GST is a global switch and is unavailable in agreement-only mode | Requirement: GST is configured at studio level (registered yes/no, GSTIN, state, default rates, SAC) and **applied per quotation, fee agreement and bill** (apply GST yes/no), never compulsory (WF-02) | Critical | CD-19, CD-20 |
| MR-06 | `BUSINESS_REQUIREMENTS.md` · `WORKFLOWS.md` B.4 | "Partial payments must always be allowed" is implied but not stated as a rule. Staged payments are optional (◇) | State: (a) any payment amount > 0 is accepted against a project, bill or milestone; (b) no rule may block a partial payment; (c) staged payment schedules are a **supported core feature, used per project when wanted** | High | CD-22, CD-23 |
| MR-07 | `PORTFOLIO_WEBSITE_PLAN.md` · `ERP_PAGES_AND_FIELDS.md` §2.18 · `DATABASE_DESIGN.md` A8 | No content-review status for website text. No tone guideline | Add: (a) a content status per page or block: Draft → Pending client review → Approved; (b) a launch checklist item "all public text client-reviewed"; (c) a tone guideline: professional, formal, ethical; no superlatives, no unverifiable claims, no invented numbers, awards or testimonials | High | CD-03, CD-04, CD-05 |
| MR-08 | `PORTFOLIO_WEBSITE_PLAN.md` · `MODULES.md` §11 | No defined display sequence. No "major project" concept. Featured is a single flag | Add a **display rule**: (1) highlighted/major projects first, by manual order; (2) other published projects by manual order, then completion year (newest first), then title. Add a `display_priority` (manual number) and keep `is_featured` for the home page | Medium | CD-10 |
| MR-09 | `SECURITY_RULES.md` §5 · `DATABASE_DESIGN.md` G3 · `TECHNICAL_REQUIREMENTS.md` §2.2 | Portfolio uploads go straight into public `uploads/portfolio/`, before consent or publishing. Unpublishing leaves the image URLs live | Store originals and drafts **privately**. Copy the processed web versions to the public folder **on publish**. Remove them (or block them) **on unpublish or delete**. Change the slug only with a 301 redirect | High | CD-09, CD-11; private client information could leak |
| MR-10 | `MODULES.md` §5 · `DATABASE_DESIGN.md` B1/B2 | The services seed is flagged `is_reference_seed`. There is no concept of "demo" services, and no rule on whether demo services appear on the public website | Add a `content_origin` (reference-seed / demo / client-confirmed) to categories and items. Demo items are badged in the ERP. Public display of demo services is gated by RCD-12 | High | CD-06 conflicts with the "do not invent services" rule unless demo content is visibly controlled |
| MR-11 | `ERP_PAGES_AND_FIELDS.md` §1.7 · `DATABASE_DESIGN.md` A11 | Only project documents have a download route. Site-visit photos and expense attachments (private files) have none. `files` has no owner reference, so the permission check cannot be resolved generically | One private-file route that resolves the **owning record** (document / site-visit photo / expense / commission payment proof) and applies that record's permission, including Admin-only for financial owners. Add an `owner_type` + `owner_id` to `files`, or keep a strict per-owner route | High | Private files must never be reachable without a matching permission |
| MR-12 | `TECHNICAL_REQUIREMENTS.md` §7 · `DATABASE_RULES.md` §11 | Off-site backup copies hold all financial, commission and personal data unencrypted. Restore does not check that files and database match | Encrypt off-site copies (password-protected archive; key kept off-server). Add a restore check: every `files` row has its file and vice versa. Run a restore drill per release | Medium | Backups now contain commission and partner bank data |
| MR-13 | `SECURITY_RULES.md` §10 | Partner (contractor) personal and bank data is not covered by the privacy rules | Add: partner identity and contact data are minimal; bank details are optional, Admin-only and masked in lists; retention follows RCD-08 | Medium | New personal and financial data category |
| MR-14 | Reports (`MODULES.md` §14, `ERP_PAGES_AND_FIELDS.md` §1.14) | No source or commission reports | Add the reports listed in §10.6 | High | CD-26 |

---

## 5. Latest client decisions incorporated

Status: **Reflected** (documents already match) · **Partly** · **Not reflected** · **Contradicted**
(a document says the opposite). "Action" points to the correcting issue.

| ID | Client decision | Status in current documents | Action |
|---|---|---|---|
| CD-01 | Domain `ajdesignstudios.in` | Not reflected (Q-H1 "pending" everywhere) | INC-06, RCD-15 |
| CD-02 | Same domain: public `/`, ERP `/erp/` | Reflected (`CLAUDE.md` §1, `TECHNICAL_REQUIREMENTS.md` §2) | Re-tag as CLIENT-DECISION |
| CD-03 | Detailed website content based on Instagram | Contradicted ("client supplies texts; content writing out of scope") | INC-11, MR-07, RCD-13 |
| CD-04 | Professional, formal and ethical tone | Not reflected | MR-07 |
| CD-05 | Client reviews website content later | Partly (Q-W9) | MR-07 — review status and launch gate |
| CD-06 | Suitable demo services and categories initially | Contradicted (`CLAUDE.md` §6 "do not invent services"; website plan "only after Q-S1") | MR-10, RCD-12 |
| CD-07 | Admin can add, update and soft-delete services and categories | Reflected (`PERMISSION_MATRIX` row 5 ADM V C E D; `[SD]` on B1/B2) | Add "soft-deleted items are kept on existing quotations and portfolio items, hidden from new selection and from the website" (PG-08) |
| CD-08 | Include all major projects and available photographs | Partly (portfolio module exists; no photos in folder; Instagram posts not readable without login) | RCD-13 (source of photos) |
| CD-09 | Projects may be removed later | Partly (unpublish route; soft delete) | MR-09, WF-14 |
| CD-10 | Sensible display sequence; major projects prioritized and highlighted | Partly (`is_featured`, `sort_order`) | MR-08, DB-17 |
| CD-11 | No invented details; no private client information without approval | Reflected (consent check, city-level location, no client names) | Keep. Strengthen with MR-09 |
| CD-12 | Contact from Instagram and reference documents; visiting card later | Partly (card already in folder but unused; second number and address spelling differ) | INC-09, RCD-04, RCD-05 |
| CD-13 | Professional quotation format using the logo and the visiting-card reference | Not reflected (Q-Q2 open; W-E7 "logo or text heading") | INC-18, PG-07 |
| CD-14 | Developer may propose quotation numbering | Not reflected (Q-Q1 still a client question) | DD-05 |
| CD-15 | Area-based and item-wise quotations | Reflected (`WORKFLOWS` A.5; fee line types) | Re-tag |
| CD-16 | Fixed pricing not mandatory | Reflected (no default rates; lines optional) | Re-tag. State explicitly that no rate is ever required to be pre-set |
| CD-17 | Admin can modify rates | Partly (Admin edits service default rates, but STF can edit quotation line rates) | MR-03, PM-05 |
| CD-18 | Billing not restricted to agreement-only; flexible | Contradicted in effect (one studio-wide mode, "chosen once", change blocked once bills exist) | WF-01, MR-04, DB-04 |
| CD-19 | GST optional and configurable | Partly (global switch; coupled to Bills mode) | WF-02, DB-11 |
| CD-20 | GST not compulsory for every quotation or project | Not reflected (no per-document switch) | WF-02 |
| CD-21 | Actual tax treatment to be confirmed | Reflected (Q-F3 pending) | Keep pending (RCD-10) |
| CD-22 | Staged payments supported | Partly (milestones ◇ optional) | MR-06 — make the schedule a core capability, used per project |
| CD-23 | Partial payments always allowed | Partly (implied by allocations and "Partly paid") | MR-06, WF-09 |
| CD-24 | Advances and allocations handled correctly | Partly (designed, with defects) | WF-05…WF-10, DB-06, DB-07 |
| CD-25 | Financial information and decisions Admin-only, everywhere | Contradicted (ACC and STF finance rights) | §8, MR-02 |
| CD-26 | Direct / Contractor projects with commission | Not reflected; contradicted by out-of-scope text | §10, INC-10, MR-01 |

**Tally (26 decisions):**

| Status | Count | Decisions |
|---|---|---|
| Reflected | 6 | CD-02, 07, 11, 15, 16, 21 |
| Partly | 10 | CD-05, 08, 09, 10, 12, 17, 19, 22, 23, 24 |
| Not reflected | 6 | CD-01, 04, 13, 14, 20, 26 (CD-26 is also contradicted by the out-of-scope text, INC-10) |
| Contradicted | 4 | CD-03, 06, 18 (in effect), 25 |

None of these decisions has been written into the decision log yet (INC-07, INC-08). This report
**records** them; it does not approve anything else.

---

## 6. Database design corrections required

All references are to `docs/DATABASE_DESIGN.md` unless stated otherwise.

| ID | Table / area | Existing situation | Required correction | Priority | Reason |
|---|---|---|---|---|---|
| DB-01 | New group I — Referral partners & commission | Absent | Add `referral_partners`, `project_commissions`, `commission_adjustments`, `commission_payments` and `commission_status_history` (full spec §10.3). Add the sequences `commission` and `commission_payment` to A9 | Critical | CD-26 |
| DB-02 | D1 `projects` | No source fields | Add `source_type` (direct / contractor; required, no silent default — see RCD-02 for "referral"), `referral_partner_id` FK NULL. Rule: required when `source_type` = contractor, must be NULL when direct | Critical | CD-26 |
| DB-03 | C2 `enquiries` | Source is a lookup only | Add `referral_partner_id` FK NULL, copied to the project on conversion. Add `contractor` / `referral` to the `enquiry_source` lookup values | High | Contractor projects usually start as contractor enquiries |
| DB-04 | A8 `settings` (`billing_mode`) · D1 `projects` | One studio-wide billing mode | Replace with `default_billing_method` in settings, plus `projects.billing_method` (agreement / bills — values per WF-01), changeable by ADM while the project has no issued bills, or as decided in DD-03 | Critical | CD-18 |
| DB-05 | F1 `fee_agreements` | `tax_amount` only; no flag for whether GST applies | Add `gst_applicable` (Y/N), `taxable_amount`, and a link to tax lines (`fee_agreement_tax_lines`, or reuse a polymorphic tax-line table). F2 `fee_variations` needs the same taxable/tax split | High | CD-19/20; variation tax is otherwise undefined |
| DB-06 | F9 `payment_allocations` | `bill_id` NULL and `fee_milestone_id` NULL, with no rule. In Bills mode an allocation can go to a milestone **and** to the bill created from that milestone → double count | Rule: **exactly one** target per allocation row (bill XOR milestone XOR fee agreement). In bills mode allocations target bills only; milestones are tracked through their bill. Add a CHECK-style application rule and a test case | Critical | Calculation correctness |
| DB-07 | F9 / WORKFLOWS B.4 (credit transfer) | Credit transfer is "two linked allocation rows", but an allocation row has no target project or credit target | Add a `credit_transfers` table (number, date, from_project, to_project, client, amount, reason, approved_by ADM, reverses_id) — only if RCD/Q-F11 = yes | High | The model cannot represent a transfer |
| DB-08 | F1 `fee_agreements` UQ(`project_id`) | Unique per project, yet the status allows "cancelled" | Replace the unique index with "one **active** agreement per project" (enforced in the application, or by a generated column `active_project_id` with a unique index) | High | A cancelled agreement would block a replacement |
| DB-09 | F7 `credit_notes` | No lines and no tax lines, yet "tax on credit notes follows the bill's tax lines" | Add `credit_note_tax_lines` (or use a polymorphic tax-line table) and a `taxable_amount` | High (if GST used) | GST credit notes need a tax breakdown |
| DB-10 | F8 `payments` | Both `client_id` and `project_id` are required. There is no way to record an advance received **before** conversion (enquiry stage) | Decide RCD-07. If allowed: `project_id` NULL with `enquiry_id`, re-linked on conversion. Add the rule that the project's client must equal `payments.client_id` | Medium | Token advances are common. A consistency rule is needed either way |
| DB-11 | A8 `settings` · C1 `clients` | No GST registration fields. No client state, so CGST+SGST vs IGST cannot be decided | Settings: `gst_registered`, `gstin`, `gst_state_code`, default SAC, default rate(s). Clients: `state`, `state_code`. Bill and agreement: `place_of_supply_state_code` snapshot. All dormant until RCD-10 | High | CD-19; required for any correct GST document |
| DB-12 | D5 `site_visits.bill_line_id` and F5 `bill_lines.site_visit_id` | The link is stored in both directions | Keep only `bill_lines.site_visit_id` (UQ where not null) | Medium | Two-way duplicate links drift apart |
| DB-13 | A11 `files` | No owner reference | Add `owner_type` + `owner_id` (or document strict per-owner join tables) and `is_financial` for permission and audit (MR-11) | High | Generic private download authorization |
| DB-14 | E1 `quotations.status` and E2 `quotation_revisions.status` | Both store status. "Mirrors the current revision" | Keep one source of truth: revision status; the header status is derived (view or query). If stored, update both in the same transaction and test it | Low | Risk of disagreement |
| DB-15 | A10 `lookups` | Lookup FK enforcement is unclear (INC-16). Types lack `referral_partner_type` and `commission_*` reasons | Add a real FK. Add list types `partner_type`, `commission_reversal_reason`, `commission_cancel_reason` | Medium | Integrity |
| DB-16 | G1/G3 portfolio + `files.storage_area` | Drafts are stored in the public area | `files.storage_area` = private for originals and drafts. Public derivatives are created on publish (MR-09). Add `unpublished_at`, `unpublished_by`, `unpublish_reason` to G1 | High | CD-09, CD-11 |
| DB-17 | G1 `portfolio_projects` | Featured flag + sort order only | Add `is_highlighted` (major project) and `display_priority`. Keep `is_featured` for the home page. Add a `content_review_status` (MR-07) | Medium | CD-10, CD-05 |
| DB-18 | G1 `portfolio_projects.cover_image_id` ↔ G3 | Circular FK (project → image → project) | Allowed only as NULLable, set after the images exist. Document the insert order. Or use `portfolio_images.is_cover` with a "one per project" rule | Low | Install and restore order; FK cycles complicate imports |
| DB-19 | B1/B2 services | `is_reference_seed` only | Replace with `content_origin` (reference / demo / client-confirmed) per MR-10 | Medium | CD-06 |
| DB-20 | [STD] columns | `created_by` / `updated_by` FKs not stated | State FK → `users.id` (NULL allowed for system and public rows such as website enquiries) | Low | Integrity |
| DB-21 | C2 `enquiries.area_unit`, D1 `projects.area_unit`, E2 | Free column, while `area_unit` is also a lookup list | Use the lookup FK consistently (or a fixed code list) | Low | Consistency |
| DB-22 | §4 integrity rules | Missing rules: allocation XOR (DB-06); allocations net of allocation reversals; write-offs in balances (WF-06); commission rules (§10); refund ≤ credit as defined per billing method (WF-07); project–client consistency (DB-10) | Extend §4 with these rules and give each a test case in WORKFLOWS B.12 | High | Correctness |
| DB-23 | Table count | "49 tables in 8 groups" | Update after corrections. Expected about **55–57** (+5 commission, +`credit_transfers` ◇, +tax-line tables or one polymorphic tax-line table) | Low | Accuracy |

---

## 7. Workflow corrections required

All references are to `docs/WORKFLOWS.md` unless stated otherwise.

| ID | Section | Existing situation | Required correction | Priority | Reason |
|---|---|---|---|---|---|
| WF-01 | B.3 Billing modes | "The mode is a studio-wide setting, chosen once before go-live. Changing it later … only when no bills exist" | Per-project billing method with a studio default (DB-04). Both methods run side by side. Specify: (a) **Agreement method** — outstanding = current agreed fee − net received − write-offs + net refunds; bills optional; receipts always; (b) **Bills method** — outstanding from issued bills. Also allow **ad-hoc bills without a fee agreement** (e.g. small item-wise jobs). Final option set: DD-03 | Critical | CD-18 |
| WF-02 | A.5 step 5 · B.3 "Tax … Not supported in Mode B" · `STAGE1_GAP_RESOLUTION` §5 ("GST depends on Bills mode") | GST is global and tied to Bills mode | GST is applied **per document** (quotation revision, fee agreement and variations, bill, credit note) via `gst_applicable`. It defaults from settings and is never compulsory. Supported in both billing methods. Tax treatment of advances under GST and the place-of-supply split stay **PENDING RCD-10 (confirm with the client's tax adviser)**; the design must not assume them | Critical | CD-19, CD-20, CD-21 |
| WF-03 | A.4 "Send" · A.4 "Accepted" | STF may send and record acceptance (PERMISSION 6a) | Sending a priced quotation and recording acceptance are **financial decisions → ADM only**, unless RCD-09 allows STF to send an Admin-approved revision | Critical | CD-25 |
| WF-04 | A.1 / A.4 / B.2 | Path 1: "Accepted → fee agreement created", but the project is created only at conversion **after** acceptance. `fee_agreements.project_id` is required | Order: Accept (ADM) → system forces conversion (client + project) in the same step → fee agreement created for the new project → commission prompt if the source is contractor | High | As written, the agreement has no project |
| WF-05 | B.4 Formulas — "Outstanding, Mode A = Issued bills − cancelled bills − credit notes − active allocations" | "Issued bills − cancelled bills" double-subtracts if "issued" already excludes cancelled | Define precisely: Σ grand_total of bills in status Issued (not cancelled) − Σ issued credit notes (not cancelled) − Σ net allocations to those bills − Σ write-offs against them | High | Wrong balances |
| WF-06 | B.4 formulas · B.8 | Write-offs are recorded but appear in no formula | Add write-offs (net of reversals) to every outstanding formula and to the reports | High | Balances never close after a write-off |
| WF-07 | B.4 credit · B.6 refunds | Credit = net received − allocations − refunds. This is meaningful only for the bills method. In the agreement method "credit" is undefined, yet refunds need "available credit" | Define for the agreement method: credit = max(0, net received − net refunds − current agreed fee). Refund ≤ credit in both methods | High | Refunds cannot be validated |
| WF-08 | B.7 vs `ERP_PAGES` §2.11 | The credit-note amount limit conflicts with the "fully paid" use case (INC-14) | Limit = bill grand total − earlier credit notes − write-offs (not "open value"). If the amount exceeds the open value, the excess becomes project credit | High | Main credit-note use case is blocked |
| WF-09 | B.4 / B.1 | Partial payments are possible but not stated as protected | Add the rule "no validation may reject a payment for being less than the amount due". Allocation of a partial amount leaves the bill or milestone Partly paid | High | CD-23 |
| WF-10 | B.5 payment reversal | Allocations are auto-reversed. Commission effect is not covered. Reversal is "ADM (or another role, if approved)" | Reversal is ADM-only. Add: if a commission's base is "received amounts", reversing a payment recalculates commission due but **never** edits a paid commission — any overpaid commission shows as recoverable (RCD-03) | High | CD-25, CD-26 |
| WF-11 | A.6 vs `ERP_PAGES` §2.10 | Two different schedule validation rules (INC-15) | One rule: the schedule must equal 100% / the total **before saving as final**; drafts may be incomplete with a warning. Specify whether stages are on the pre-tax or post-tax total (RCD-14) | Medium | Consistency |
| WF-12 | A.2 conversion · A.3 | No source or commission step | On conversion copy `source_type` and the partner. If contractor: create the project commission record in **Draft** (applicability not assumed) for ADM to complete and approve | Critical | CD-26 |
| WF-13 | New Part C | No commission workflow | Add Part C — Commission lifecycle (§10.4) | Critical | CD-26 |
| WF-14 | Portfolio (new section) | Publish and unpublish exist only as routes. No full workflow | Add the portfolio workflow: Draft → (consent recorded + cover + alt text + content reviewed) → Published → Unpublished (reason) → Re-published, or Removed (soft delete). On publish: copy derivatives to public storage and update the sitemap. On unpublish or remove: withdraw public files, take it off the sitemap and listings, return HTTP 410/404. On slug change: 301 redirect | High | CD-08…CD-11 |
| WF-15 | B.9 expenses · `PERMISSION_MATRIX` row 9 | STF/SITE may create expenses | Expenses are ADM-only unless RCD-09 allows staff "expense claims" that ADM approves. If allowed, a claim has no posting effect until Admin approval | High | CD-25 |
| WF-16 | B.12 test cases | No GST-per-document, per-project billing, commission, write-off or partial-payment cases | Add test cases: GST on/off on two quotations of the same project; agreement-method and bills-method projects side by side; partial payment below the amount due; allocation XOR violation blocked; commission percentage and fixed amount, approval, partial commission payment, commission payment reversal, commission on a direct project blocked; write-off then balance; credit note on a fully paid bill | High | Execution evidence for Stage 9 |

---

## 8. Permission matrix corrections required

Applies to `docs/PERMISSION_MATRIX.md`, and through it to `MODULES.md`, `ERP_PAGES_AND_FIELDS.md`,
`WIREFRAMES.md`, and reports. **Principle (CD-25):** every financial view, entry, decision, report,
dashboard widget, export, document category and API response is **ADM only**. Non-Admin roles
get **no financial data in server responses** — not merely hidden on screen.

| ID | Matrix row(s) | Existing | Required | Priority | Reason |
|---|---|---|---|---|---|
| PM-01 | 1a Dashboard financial widgets | ADM V, ACC V | ADM only. Non-ADM dashboard queries never compute or return financial aggregates | Critical | CD-25 |
| PM-02 | 3a Client financial summary · 4b Project fee & payment tabs | ADM, ACC | ADM only. Tabs not rendered and routes return 403 for others | Critical | CD-25 |
| PM-03 | 7, 7a, 7b, 7c Fee agreement, bills, credit notes | ADM + ACC (C E S R) | ADM only | Critical | CD-25 |
| PM-04 | 8, 8a, 8b, 8c, 8d Payments, allocation, reversal, refund, receipts | ADM + ACC | ADM only | Critical | CD-25 |
| PM-05 | 6, 6a, 6b, 6c Quotations | STF: V C E X and S (send/decide); ACC: V | Pricing fields (rates, amounts, discount, tax, totals), send, accept/reject and discount approval: **ADM only**. STF scope-only drafting is allowed **only if RCD-09 says so**; then STF sees no amounts in lists, PDFs or exports | Critical | Quotations carry fees; acceptance creates a financial commitment |
| PM-06 | 9, 9a Expenses | STF / SITE / ACC create; ACC reverse | ADM only (or claim-and-approve per RCD-09 / WF-15) | Critical | CD-25 |
| PM-07 | 14a Financial reports | ADM, ACC | ADM only, including CSV export and print | Critical | CD-25 |
| PM-08 | 16 Settings — finance (billing method, tax, rounding, lock date, numbering of financial documents) | ADM V E; ACC V | ADM only | High | CD-25 |
| PM-09 | 5 Services | Default rate visible to all roles (V) | Default rates hidden from non-ADM. Categories and items (names, descriptions) remain viewable | High | Rates are financial |
| PM-10 | 10 Project documents | ACC sees "agreement / financial categories" | Document categories carry an `is_financial` flag; financial categories (agreements, bills, receipts, payment proofs, commission documents) are ADM-only for view, upload and download | High | CD-25 |
| PM-11 | 13 Follow-ups | ACC: payment follow-ups | Follow-ups linked to bills, payments or commissions are ADM-only. Their notes may contain amounts | High | Leak path |
| PM-12 | New rows — Referral partners | — | Partner master: ADM V C E D. STF may **select** a partner on an enquiry or project and see name and phone only, if RCD-06 allows; partner bank, tax and commission defaults are ADM only | Critical | CD-26 |
| PM-13 | New rows — Commission | — | Commission terms, approval, payments, reversals, reports, dashboard widget, exports: **ADM only**. A project's "commission applicable" flag is itself financial → ADM only | Critical | CD-26 |
| PM-14 | ACC role (all rows) | Defined as the finance role | With finance Admin-only, ACC has no purpose. **Remove ACC from the default roles** (keep the permission system so it can be added later if the client delegates) — DD-07 | High | Avoids a role that contradicts CD-25 |
| PM-15 | §3 record-level rules — "Financial fields … removed from the server response for roles without financial view … STF (pending), SITE" | Pending for STF | Applies to **all non-ADM roles**, without exception. Extend it explicitly to: AJAX endpoints (`/erp/api/quotation-preview-totals`, `/erp/api/open-bills`), search results, list columns, timelines and activity entries, follow-up notes, PDFs, CSV exports, email digests and notifications, error messages | Critical | Every leak path must be named |
| PM-16 | Activities / timeline (C4) | Status-change entries are visible to anyone who can see the record (e.g. W-E4 shows "3/2026 R1 Sent ₹…") | System-generated activity text must not contain amounts. Financial events are written to the audit log (ADM only), not to the shared timeline, or are written without amounts | High | Leak path |
| PM-17 | 11a Portfolio publish | ADM S; STF pending | Keep ADM; confirm (RCD-12). Not financial, but consent-sensitive | Low | Clarity |
| PM-18 | 17 Audit log | ADM V X | Unchanged. Note that `old_values` / `new_values` hold financial data → export is ADM only and audited | Low | Confirmation |

---

## 9. ERP page and field corrections required

All references are to `docs/ERP_PAGES_AND_FIELDS.md` unless stated otherwise.

| ID | Page / field | Existing | Required | Priority | Reason |
|---|---|---|---|---|---|
| PG-01 | §1 URL list | No partner or commission pages | Add the pages in §10.5 | Critical | CD-26 |
| PG-02 | §2.2 Enquiry · §2.5 Project | No source or partner fields | Add Source type (Direct / Contractor), Partner (search/select; required when Contractor). On the project, the "Source & Commission" panel is visible to ADM only | Critical | CD-26 |
| PG-03 | §2.18 Settings — Finance · §1.15 `/erp/settings/finance` | "Billing mode", "tax enabled" | Replace with: default billing method; GST registration block (registered, GSTIN, state, default rate lines, SAC); "apply GST by default on new quotations" (default **off**); rounding; lock date. ADM only | Critical | CD-18…CD-20 |
| PG-04 | §2.9 Quotation builder | Tax shown "only if tax is enabled" (global) | Add an **Apply GST** switch per revision (visible only when the studio is GST-registered). Rate cells are editable by ADM only (MR-03). No pre-filled rate unless the Admin set a default | Critical | CD-17, CD-20 |
| PG-05 | §2.10 Fee agreement · §2.11 Bill | Tax fields are not switchable per document | Add Apply GST + tax lines + taxable amount. Add a per-project billing method on the project form (ADM) | High | CD-18, CD-19 |
| PG-06 | §2.12 Payment | Allocation grid "Mode A" only | The grid adapts to the project's billing method. Allow allocation to milestones in the agreement method (DB-06 XOR rule). Show "Advance — no allocation" explicitly. No minimum-amount validation (WF-09) | High | CD-23, CD-24 |
| PG-07 | `WIREFRAMES.md` W-E7 Quotation PDF | "[LOGO] or ‹text heading›" | Letterhead from the supplied logo and the visiting-card layout (name, title, phones, address, email, optional Instagram QR, if approved). Never print commission or partner data. "श्री" optional (RCD-11) | High | CD-13, CD-26 |
| PG-08 | §1.8 Services · §2.8 | No delete route; soft-delete behaviour not stated | Add `/erp/services/categories/{id}/delete` and `/erp/services/items/{id}/delete` (POST, soft delete, ADM). Add a "demo" badge and `content_origin`. Soft-deleted items stay on old quotations and are hidden from new selection and from the public site | High | CD-06, CD-07 |
| PG-09 | §1.13 Portfolio · §2.15 | No reorder, highlight or unpublish reason. Consent is a checkbox only | Add `/erp/portfolio/reorder` (POST). Add fields `is_highlighted` / `display_priority`, an unpublish reason, a consent evidence file (optional) and a content review status. Delete = soft delete with public files withdrawn (WF-14) | High | CD-08…CD-11 |
| PG-10 | §1.7 Documents | One route for project documents only | One private-file route resolved by owner (MR-11). Downloads of financial categories are always audited (not "optional") | High | Private files |
| PG-11 | §1.14 Reports | No source or commission reports | Add the §10.6 reports (ADM) plus a non-financial "enquiries/projects by source" report (STF allowed if RCD-06 allows) | High | CD-26 |
| PG-12 | §2.18 Settings — Website · §2.18 Studio | No content review status. Studio phone is a single field | Add a review status per content block. Add phone 2 (visiting card) and a "WhatsApp number" choice (RCD-04) | Medium | CD-05, CD-12 |
| PG-13 | `WIREFRAMES.md` W-E2, W-E4, W-E5, W-E8 | "ADM/ACC" finance panels; the enquiry detail shows a quotation amount to all | ADM only; remove amounts from non-ADM views. Add a "Commission" panel (ADM) on W-E5 and an Admin "Commission outstanding" dashboard tile | Critical | CD-25, CD-26 |
| PG-14 | §2.4 Client | GSTIN shown "only if tax is enabled" | Add state and state code (DB-11). GSTIN visible and editable by ADM only | Medium | GST place of supply |
| PG-15 | §1.16 AJAX | Endpoints return totals and open bills | Mark ADM-only and add to the PM-15 response-filter rule | High | Leak path |

---

## 10. Contractor commission module requirements

Status: **PROPOSED** design from client decision CD-26. Items marked **PENDING** depend on
§11 decisions and must not be built as assumptions.

### 10.1 Business rules (from the client decision — CLIENT-DECISION)
1. Every project has a **source**: Direct or Contractor (RCD-02: whether "Referral (non-contractor)" is a separate value).
2. Contractor projects record the **contractor / referral source details**.
3. **Commission applicable:** Yes / No, recorded per project. **Never assumed**, never automatic, and **never allowed on Direct projects**.
4. **Commission type:** Percentage or Fixed amount, with the rate or amount and the calculated commission amount.
5. **Commission approval status**; commission is payable only after approval.
6. **Commission paid** and **outstanding** amounts, from commission payment records with dates.
7. Remarks and full **audit history**.
8. All commission financial information is **Admin-only**.

### 10.2 Proposed additional rules (PROPOSED — approval needed)
- Commission data never appears on client-facing output: quotation, bill or receipt PDFs, the
  website, or client emails.
- Approved terms are immutable. Changes go through an **adjustment** (signed, reason, ADM) or
  through cancellation and a new record.
- Commission payments are immutable. Corrections are made by **reversal** (`reverses_id`, reason), as for client payments.
- Paid ≤ payable (approved commission + adjustments). Overpayment is blocked; if a later recalculation makes paid exceed payable, show it as **recoverable** (no automatic clawback).
- The lock date and numbering rules apply (`CP/{fy}/{seq4}` proposed for commission payments).
- Commission payments are **not** also recorded as expenses (no double counting). The profitability report subtracts them once.
- A partner cannot be deactivated while they have outstanding commission.

### 10.3 Data model (proposed)

| Table | Key columns |
|---|---|
| `referral_partners` | `partner_type` (lookup: contractor / referral / other), `name`, `firm_name`, `mobile` IX, `alt_mobile`, `email`, `address`, `city`, `notes`, `is_active`; **ADM-only:** `bank_details_enc` NULL, `pan` NULL (only if RCD-05 requires it for tax), `default_commission_type` NULL, `default_commission_value` NULL (a suggestion only, never auto-applied) · [STD] [SD] |
| `projects` (change) | `source_type` (direct / contractor), `referral_partner_id` FK NULL |
| `enquiries` (change) | `referral_partner_id` FK NULL |
| `project_commissions` | `project_id` FK · `referral_partner_id` FK · `is_applicable` (Y/N) · `commission_type` (percentage / fixed) · `rate_pct` PCT NULL · `fixed_amount` MONEY NULL · `base_type` (**PENDING RCD-03**: agreed fee excl. GST / amounts received / other) · `base_amount` MONEY (snapshot at approval) · `commission_amount` MONEY (calculated: base × rate, rounded to the paisa; or the fixed amount) · `status` (Draft / Pending approval / Approved / Rejected / Cancelled) · `approved_by`, `approved_at`, `approval_remark` · `cancelled_by`, `cancelled_at`, `cancel_reason` · `remarks` · [STD]. UQ(`project_id`, `referral_partner_id`) unless RCD-01 allows several commissions per project |
| `commission_adjustments` | `project_commission_id` FK · `adjustment_date` · `amount` (signed MONEY) · `reason` · `approved_by` (ADM) · [STD] |
| `commission_payments` | `payment_no` UQ · `project_commission_id` FK · `payment_date` IX · `amount` (signed MONEY) · `mode_id` lookup FK · `reference_no` · `tds_amount` MONEY NULL (**PENDING RCD-05**) · `proof_file_id` FK NULL (private, financial) · `notes` · `reverses_id` FK NULL UQ · `reversal_reason_id`, `reversal_note` · [STD] |
| `commission_status_history` | `project_commission_id` FK · `from_status` · `to_status` · `remark` · `changed_by` · `changed_at` |

**Derived amounts (stored or calculated, tested):**
- Payable = approved `commission_amount` + Σ adjustments.
- Paid = Σ commission payments (net of reversals).
- Outstanding = Payable − Paid.
- If `base_type` = amounts received: commission **earned to date** = base received to date × rate (shown separately; RCD-03).

**Integrity:**
- `is_applicable` = Y is allowed only when the project's `source_type` = contractor.
- Exactly one of `rate_pct` / `fixed_amount`, matching `commission_type`.
- Payments only when status = Approved.
- Negative amounts only on reversals.
- Every write happens in a transaction together with its number sequence.

### 10.4 Workflow (Part C to add to `WORKFLOWS.md`)
```
Enquiry (source = Contractor, partner selected)
   │ convert
   ▼
Project (source_type = contractor, partner copied) ──► Commission record created in DRAFT
   │                                                   (is_applicable not yet set — ADM decides)
   ▼
ADM sets: applicable? type? rate/amount? base? ── applicable = No → status Approved-as-not-applicable / closed
   │ applicable = Yes
   ▼
Pending approval ──► Approved (ADM, remark)  ──► Commission payments (partial allowed, any number)
   │               └► Rejected (reason)              │ wrong entry → reversal (ADM, reason)
   ▼                                                 ▼
Adjustments (fee variation, negotiated change) ─► Outstanding = Payable − Paid
Project cancelled → commission handling PENDING (RCD-08): cancel unpaid part / keep / recover
```
Direct project → no commission record can be created (the action is not offered; the server rejects it).

### 10.5 Pages (ADM only unless noted)

| URL | Purpose |
|---|---|
| `/erp/partners`, `/new`, `/{id}`, `/{id}/edit`, `/{id}/deactivate` | Contractor / referral master (STF select-only per RCD-06) |
| `/erp/projects/{id}/commission` | Project "Source & Commission" tab: terms, status history, adjustments, payments |
| `/erp/commissions` | Commission register: filters for partner, status, outstanding |
| `/erp/commissions/{id}/submit`, `/approve`, `/reject`, `/cancel` | Status actions (POST + CSRF, remark required) |
| `/erp/commissions/{id}/adjustments/new` | Signed adjustment with reason |
| `/erp/commissions/{id}/payments/new` | Record a commission payment (partial allowed) |
| `/erp/commission-payments/{id}`, `/{id}/reverse`, `/{id}/voucher` | View, reverse, print an internal payment voucher |

### 10.6 Reports and dashboard (ADM only)
- Commission payable / paid / outstanding by partner and by project.
- Commission payment register (date range, mode, reversals).
- Partner performance: enquiries, conversions and projects by partner. The non-financial version may be shown to STF if RCD-06 allows.
- Direct vs contractor projects: count and fee value (fee value is ADM only).
- Profitability: fees received − project expenses − commission paid (optional report).
- Dashboard tile: "Commission outstanding" and "Commission awaiting approval".
- All exports audited.

### 10.7 Audit
Create, every field change while in Draft, every status change, adjustment, payment, reversal,
export and partner bank-detail change → `audit_logs` with old and new values. Remarks are
mandatory on approval, rejection, cancellation, adjustment and reversal.

---

## 11. Remaining client decisions

These are genuine business ambiguities. They are **not** resolved in this report. "Impact" says
what is blocked or what the design does until answered.

| ID | Pri | Decision needed | Impact if open |
|---|---|---|---|
| RCD-01 | P1 | **Commission direction and parties:** does the studio pay commission **to** the contractor or referrer (assumed by the module), or can it also run the other way? Can one project have more than one partner or commission? | The data model direction and uniqueness. The module cannot be finalised |
| RCD-02 | P1 | Is a non-contractor referrer (friend, previous client, agent) recorded as source "Contractor", or as a third value "Referral"? | `source_type` values, reports |
| RCD-03 | P1 | **Commission base and timing:** a percentage of what — quoted total, agreed fee **excluding** GST, or amounts actually received? When is it payable — on agreement, pro-rata as the client pays, or on completion? Do fee variations, refunds or write-offs change it? | `base_type`, the earned-to-date calculation, the outstanding figure |
| RCD-04 | P1 | Contact details to publish: which number is primary, which is WhatsApp (8806956877 and/or **7796877369** from the visiting card)? | Contact page, WhatsApp button, letterhead |
| RCD-05 | P1 | **Tax on commission:** is tax deducted at source on commission payments, and is any GST involved? To be confirmed with the client's tax adviser. The design will not assume it | Whether `tds_amount` and PAN fields are used |
| RCD-06 | P2 | May staff (STF) see partner names and phone numbers, select a partner on enquiries, and see the "by source" counts? (Commission amounts stay ADM-only in all cases) | PM-12, PG-11 |
| RCD-07 | P2 | Are advances ever received **before** a project is opened (at enquiry stage)? | DB-10 |
| RCD-08 | P2 | What happens to commission when a project is cancelled or the client does not pay: cancel the unpaid part, pay in full, or recover what was paid? How long are partner records kept? | Commission cancellation rule, retention |
| RCD-09 | P1 | **Edge of "Admin-only finance":** may staff (a) draft quotation **scope** without prices, (b) send an Admin-approved quotation PDF, (c) submit expense claims for Admin approval? Will anyone other than Ar. Ajit Kumbhar use the ERP at all (Q-U1)? | PM-05, PM-06, WF-03, WF-15; possibly a single-user ERP |
| RCD-10 | P1 | **GST status:** is the studio GST-registered (GSTIN)? Applicable rate and SAC? Which projects or clients take GST? Treatment of advances? To be confirmed with the client's tax adviser | GST blocks stay dormant; quotations work without GST |
| RCD-11 | P2 | Keep "श्री" at the top of quotations? Signature wording ("Ar. Ajit Arjun Kumbhar" vs "Ar. Ajit Kumbhar")? Show the Instagram QR? | Letterhead layout, PDF library choice (D-18) |
| RCD-12 | P1 | Demo services: may demo services appear on the **live** public website before the client confirms them, or only in the ERP and on staging? Who may publish portfolio items? | MR-10, website go-live |
| RCD-13 | P1 | **Source of portfolio photos and content:** Instagram posts cannot be read without login and are lower resolution. Will the client supply original photos and project details, or grant access? Which projects are "major"? | Portfolio cannot be populated. Website content drafting is blocked |
| RCD-14 | P2 | Payment stages: as a % of the total **including** or **excluding** GST? | WF-11 |
| RCD-15 | P1 | Confirm the exact registered domain spelling: **ajdesignstudios.in** (plural "studios") while the brand is "AJ Design Studio". Is a business email on the domain planned? | DNS, SSL, email, SEO. A typo here is costly |
| RCD-16 | P2 | Refunds (Q-F9), write-offs (Q-F10), credit transfer between projects (Q-F11) | Optional tables stay switched off |
| RCD-17 | P1 | Still-open earlier P1 questions not settled by the latest decisions: Q-G1, Q-G2 (default path), Q-G9 (website first?), Q-S2 (meaning of Temple Work / कोकण शिल्प / Complete Project — design-only or execution?), Q-Q3 (area basis), Q-Q7 (standard terms), Q-F6 (receipt format), Q-U1 (actual users), Q-H2 (hosting plan), Q-B1 (vector logo) | See `CLIENT_QUESTIONS.md` |
| RCD-18 | P2 | Address spelling: "Sai **Arcade** Building" (quotation) vs "Sai **Arked** Building" (visiting card) | Contact page, letterhead, schema.org data |

Questions settled or narrowed by the latest decisions:
- **Answered:** Q-H1 (domain — subject to RCD-15), Q-Q2 (logo letterhead — "श्री" still open), Q-Q4/Q-Q5 (both area and item-wise supported), Q-W5 (no private info without approval — the process is still needed), Q-W9 (content drafted from Instagram, client reviews).
- **Narrowed:** Q-S1 (demo first), Q-W1 (all major projects), Q-W3/Q-W4 (Instagram + documents + card), Q-Q1 (developer proposes), Q-F1 (flexible), Q-F2 (staged supported), Q-F3 (optional; status open), Q-U1 (finance Admin-only; user list open).

---

## 12. Developer decisions requiring approval

Existing decisions D-01…D-23 (`STAGE1_ROADMAP_AND_DECISIONS.md` §4.2) remain open, except
where changed below. New or changed decisions:

| ID | Decision | Proposed default | Affects |
|---|---|---|---|
| DD-01 | Authoritative copy: local folder vs GitHub `codintdigitechdev/AJ_Design_Studio` | Initialise or clone Git **before** applying corrections; push the documents. Supersedes D-02 | INC-12 |
| DD-02 | Tag scheme | CONFIRMED-REF / CLIENT-DECISION / BRIEF / PROPOSED / ASSUMPTION / PENDING. Supersedes D-01 | INC-04 |
| DD-03 | Billing flexibility model | Per-project `billing_method` (agreement / bills) with a studio default; ad-hoc bills allowed; method changeable by ADM while no issued bills exist on that project | WF-01, DB-04 |
| DD-04 | GST structure | Studio GST profile + per-document `gst_applicable`; tax lines on quotation, agreement, variation, bill and credit note; one polymorphic `tax_lines` table vs per-document tables (prefer per-document tables for FK integrity) | WF-02, DB-05, DB-09, DB-11 |
| DD-05 | Numbering proposal (CD-14) | Quotation `AJDS/Q/{fy}/{seq3}` with revision suffix `-R{n}` on the PDF. Project `AJDS/P/{fy}/{seq3}`. Bills, receipts, credit notes, refunds and expenses as in `WORKFLOWS` B.11 with an `AJDS/` prefix. Commission payment `AJDS/CP/{fy}/{seq4}`. Financial year April–March (still ASSUMPTION, Q-G8). Supersedes D-09 timing: number taken on **first send** so that discarded drafts do not consume numbers | Numbering |
| DD-06 | Allocation target rule | Exactly one target per allocation (DB-06) | Payments |
| DD-07 | ACC role | Remove from the default roles; ADM, STF, SITE remain (STF/SITE without any financial rights) | PM-14 |
| DD-08 | Portfolio storage | Private originals, public derivatives created on publish and withdrawn on unpublish | MR-09, DB-16 |
| DD-09 | Commission model | As §10.3. Adjustments instead of edits; reversals instead of deletes; commission payments are not expenses | §10 |
| DD-10 | Financial response filtering | One central "financial field" registry used by every view, API, export and PDF renderer for non-ADM users | PM-15 |
| DD-11 | Private file access | `files.owner_type/owner_id` + one route; financial downloads always audited | MR-11, DB-13 |
| DD-12 | Supersede stale packages | Add a banner to `STAGE1_REVIEW_PACKAGE.md` and `STAGE1_REVIEW_PACKAGENew.md`; no deletion | INC-02, INC-03 |
| DD-13 | Off-site backup encryption | Encrypted archives; key kept off-server by ADM | MR-12 |
| DD-14 | Content drafting from Instagram | CodInt drafts, tagged "pending client review", no publication before review; images only from client-supplied originals | MR-07, RCD-13 |

---

## 13. Prioritized correction checklist

Do these in order. Do not mark an item done until the document change is made **and** the
approval (where needed) is recorded in the decision log.

### Critical — must be completed before Stage 1 approval
- [ ] 1. Record the client decisions with date and source (INC-08) and log them (INC-07).
- [ ] 2. Settle DD-01: put the documents under Git and agree the authoritative copy.
- [ ] 3. Write the financial-data definition and the Admin-only rule (MR-02) and apply PM-01…PM-07, PM-12, PM-13, PM-15 to `PERMISSION_MATRIX.md`, `MODULES.md`, `WORKFLOWS.md`, `ERP_PAGES_AND_FIELDS.md` and `WIREFRAMES.md` (PG-13).
- [ ] 4. Re-scope contractor commission into scope (INC-10). Add the commission module to `BUSINESS_REQUIREMENTS`, `MODULES`, `DATABASE_DESIGN` (DB-01…DB-03), `WORKFLOWS` (WF-12, WF-13), pages (PG-01, PG-02).
- [ ] 5. Replace the studio-wide billing mode with a flexible per-project method (WF-01, DB-04, MR-04, PG-03).
- [ ] 6. Make GST per-document and optional (WF-02, MR-05, PG-04).
- [ ] 7. Fix the allocation target rule (DB-06).
- [ ] 8. Move quotation pricing, sending and acceptance to ADM (WF-03, PM-05).
- [ ] 9. Apply the approved errata C-01…C-18 / R-01…R-08 to the original documents (INC-01).
- [ ] 10. Obtain answers to RCD-01, RCD-02, RCD-03, RCD-09, RCD-10 (or record agreed interim defaults).

### High — before the affected module's detailed design
- [ ] 11. Fix the calculation definitions WF-05, WF-06, WF-07, WF-08, WF-09 and the conversion order WF-04.
- [ ] 12. Fix the data model: DB-05, DB-07 (if Q-F11), DB-08, DB-09, DB-11, DB-13, DB-16, DB-22.
- [ ] 13. Portfolio workflow and storage: WF-14, MR-08, MR-09, PG-09.
- [ ] 14. Services demo handling and soft delete: MR-10, PG-08.
- [ ] 15. Website content drafting and review gate: INC-11, MR-07, RCD-12, RCD-13.
- [ ] 16. Private file route by owner: MR-11, PG-10.
- [ ] 17. Remaining permissions: PM-08…PM-11, PM-14, PM-16; AJAX endpoints PG-15.
- [ ] 18. Reports: MR-14, PG-11. Test cases: WF-16.
- [ ] 19. Housekeeping: INC-02, INC-03 (superseded banners), INC-04 (tags), INC-05 (`CLAUDE.md` map), INC-06 (domain), INC-09 (visiting card), INC-12, INC-14, INC-17.
- [ ] 20. Answers to RCD-04, RCD-05, RCD-13, RCD-15, RCD-17.

### Medium
- [ ] 21. INC-15/WF-11 schedule rule; INC-16/DB-15 lookup FK; INC-18 letterhead; DB-10, DB-12, DB-17, DB-19; MR-12 backup encryption; MR-13 partner privacy; PG-12, PG-14.
- [ ] 22. RCD-06, RCD-07, RCD-08, RCD-11, RCD-14, RCD-16, RCD-18.

### Low
- [ ] 23. DB-14, DB-18, DB-20, DB-21, DB-23; PM-17, PM-18.

---

## 14. Stage 1 approval readiness assessment

**Verdict: NOT READY.** Stage 1 must not be marked approved. This audit being complete does not
change that.

| Gate criterion (`STAGE1_ROADMAP_AND_DECISIONS.md` §2) | State | Blocking issues |
|---|---|---|
| 1. All P1 client questions answered or deferred with an agreed default | **Not met.** Several P1 items are answered by the latest decisions, but new P1 decisions exist (commission, GST status, Admin-only boundary, contacts, domain spelling, photo source) | RCD-01…05, 09, 10, 12, 13, 15, 17 |
| 2. Developer decisions D-01…D-23 decided | **Not met.** None recorded; DD-01…DD-14 added | §12 |
| 3. Original documents updated with the approved errata; tags re-qualified | **Not met.** No erratum applied | INC-01, INC-04 |
| 4. Decision log records the Stage 1 approval | **Not met** | INC-07 |
| Additional: the design reflects the latest client decisions | **Not met.** 4 contradicted, 6 not reflected, 10 partly reflected | §5 |
| Additional: no known calculation or integrity defects | **Not met** | DB-06, DB-08, WF-04…WF-08 |

**What is in good shape and should be preserved:**
- the hosting and folder model (public `/`, ERP `/erp/`, code and private storage outside the web root)
- immutability-by-reversal for financial records
- frozen quotation revisions with a calculation order
- the number-sequence locking
- the audit log design
- upload validation
- the consent-gated portfolio
- the lookup and status approach

The corrections are additive or local; no redesign of the architecture is needed.

**Estimated path to readiness:**
1. Record the decisions (checklist 1–2).
2. Apply the Critical corrections in one documentation revision (3–9).
3. Obtain the five Critical client answers (10).
4. Run a short re-audit limited to the changed sections.
5. Record the Stage 1 approval in the decision log, with date and approver.

---

*End of report. No existing project document was modified, renamed or deleted. No application
code, SQL or UI was created. No client approval has been assumed beyond the decisions listed in
§5, which are recorded here as reported by the developer and still need a dated written record
(INC-08).*
