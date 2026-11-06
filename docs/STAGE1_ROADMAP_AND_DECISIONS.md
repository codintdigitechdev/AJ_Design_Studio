# Updated Implementation Roadmap and Decision Register

**Status: PROPOSED — PENDING APPROVAL.**

This updates `project-context/DEVELOPMENT_ROADMAP.md`, which **has not been edited**. Once
this file is approved, the roadmap and its decision log will be brought in line with it.

---

## 1. Where the project stands (2026-11-06)

| Stage | Status |
|---|---|
| 0 Discovery & documentation | Documents complete. **Gate not yet recorded** in the decision log (D-03) |
| 1 Architecture & database design | **Draft deliverables produced** (§2). Waiting for developer review and client answers to the P1 questions |
| 2–12 | Not started. Implementation is **blocked** by the gate in `CLAUDE.md` |

## 2. Stage 1 deliverables — checklist

| Roadmap deliverable (ROADMAP §1) | File | State |
|---|---|---|
| Final module list after the necessity review | `STAGE1_GAP_RESOLUTION.md` §4–5 | Draft — PENDING APPROVAL |
| ER diagram | `DATABASE_DESIGN.md` §1 | Draft — PENDING APPROVAL |
| Table-by-table design | `DATABASE_DESIGN.md` §3 | Draft — PENDING APPROVAL |
| Role / permission matrix | `PERMISSION_MATRIX.md` | Draft — PENDING Q-U1 |
| Folder structure | `TECHNICAL_REQUIREMENTS.md` §2 (existing) | Unchanged — PENDING APPROVAL |
| URL map | `ERP_PAGES_AND_FIELDS.md` §1 + `PORTFOLIO_WEBSITE_PLAN.md` §2 | Draft — PENDING APPROVAL |
| Quotation calculation spec | `WORKFLOWS.md` A.4–A.6 | Draft — PENDING D-10, Q-Q3..Q-Q5 |
| Financial workflow (added) | `WORKFLOWS.md` Part B | Draft — PENDING Q-F1..Q-F9 |
| Field specifications (added) | `ERP_PAGES_AND_FIELDS.md` §2 | Draft |
| PDF library choice | — | **Not decided** (D-18 / Q-T1) |
| Wireframes for key pages | `WIREFRAMES.md` | Draft — PENDING APPROVAL |
| Host capability check | — | **Not possible yet**; needs Q-H2 |

### Stage 1 gate — proposed exit criteria
1. All **P1** client questions answered, or explicitly deferred with an agreed default
   (§4.1).
2. Developer decisions D-01 … D-23 decided (§4.2).
3. The original documents updated with the approved errata (C-01 … C-18), and the tags
   re-qualified (BRIEF-UNVERIFIED).
4. The decision log records: "Stage 1 architecture and database design approved — date —
   approved by".

## 3. Updated stage plan — PROPOSED

The changes from the original roadmap are shown in **bold**.

| Stage | Name | Deliverables | Gate | Depends on |
|---|---|---|---|---|
| 0 | Discovery & documentation | Done | **Record acceptance (D-03)** | — |
| 1 | Architecture & DB design | The files in §2. **Git initialised now, so the design documents are versioned (D-02)** | Written approval | P1 answers |
| 2 | Foundation | Folder structure, config, entry point, database helper, **number sequence service, money and calculation helper (with its own unit-level test checklist)**, login/logout/reset, roles and permissions **taken from the approved matrix**, CSRF, layouts, audit log, `database.sql` v1 **for the entire approved schema**, installer / first-admin setup | Login + security checklist executed | Stage 1 |
| 3 | Masters & settings | Settings (studio, letterhead, numbering, **finance switches**, website), lookups, services, users and roles | Module tests executed | 2 |
| 4 | Public website | All public pages, enquiry form → **single enquiry module**, WhatsApp **click counter**, SEO | Client design review on staging (Q-H3) | 3; real content (Q-W1) |
| 5 | Portfolio CMS | Portfolio items, image processing, gallery switch, **consent check before publishing** | Client uploads a real project | 3, 4 |
| 6 | CRM | Enquiries (**unreviewed queue, activities, conversion wizard**), clients, follow-ups, dashboard v1 | Module tests executed | 3 |
| 7 | Projects & documents | Projects (statuses **without "Enquiry stage"**), team members, documents, site visits ◇ | Module tests executed | 6 |
| 8 | Quotations | Builder, revisions (**no "Revised" status; Superseded**), approval ◇, print/PDF, compare, **acceptance → fee agreement** | Client approves the PDF using a real example | 7; D-10, D-18, Q-Q* |
| 9 | Fees, payments, expenses | **Fee agreement + variations**, milestones ◇, bills ◇ **(per billing mode)**, credit notes ◇, payments, **allocation and credit**, receipts, reversals, **refunds ◇**, **write-offs ◇**, expenses ◇, lock date | **Financial test cases (WORKFLOWS B.12) executed** | 8; Q-F1..F9 |
| 10 | Reports & dashboard v2 | The agreed reports, CSV export | Client sign-off | 9; Q-R1 |
| 11 | Hardening & QA | Security review, browser and device tests, performance, backup/restore drill, `sample_data.sql` (invented data only) | Test report | 10 |
| 12 | Deployment & handover | cPanel, SSL, cron, training, guides, final ZIP | Client acceptance | 11; Q-H1, Q-H2 |

**Phased launch option — PENDING APPROVAL (Q-G9)**
- **Phase 1 (website first):** Stages 2 → 3 → 4 → 5, plus the enquiry part of Stage 6.
  Goes live with the website, the portfolio CMS and the enquiry inbox.
- **Phase 2:** the rest of Stage 6, then Stages 7 → 12 for the ERP.
- **Database:** the full schema is still created in Stage 2, so Phase 2 needs no structural
  migration.
- **Risk:** Phase 1 cannot go live until real portfolio photos exist (Q-W1).

**Testing rule (unchanged):** a test is reported as passed only if it was actually executed.
PHP and MySQL are not on this machine's shell PATH, and the XAMPP location is still to be
confirmed.

---

## 4. Decision register — everything still requiring approval

### 4.1 Client decisions (`docs/CLIENT_QUESTIONS.md`, plus new questions)

**P1 — blocks the Stage 1 gate**

| ID | Decision | Affects |
|---|---|---|
| Q-G1 | How enquiries, quotations, payments and drawings are tracked today | Data import, workflow defaults |
| Q-G2 | The real sequence (quote at enquiry stage, or open a project first?) | `WORKFLOWS.md` A.1, C-01 |
| Q-G9 | Website first, or everything together | §3 phasing |
| Q-S1 | Final services and sub-items | Services master, website, quotation scope |
| Q-S2 | Meaning of Temple Work / कोकण शिल्प / Complete Project; design-only or also execution | Scope boundary |
| Q-W1 | Portfolio projects and photos available | Stage 4–5 go-live |
| Q-W3 | Address, map and office hours to publish | Contact page |
| Q-W4 | WhatsApp number and email to publish | Contact page, WhatsApp |
| Q-W5 | Client publishing consent; whether client names are shown | Portfolio publish rule |
| Q-B1 | Vector or transparent logo | Header, favicon, PDF |
| Q-Q1 | Quotation number format, and whether it resets by calendar or financial year | Number sequences |
| Q-Q2 | Letterhead: logo or red text heading; whether to keep "श्री" | PDF, PDF library choice |
| Q-Q3 | Area basis and unit | Quotation fields |
| Q-Q4 | One composite rate, or separate rates per service | Fee line types |
| Q-Q5 | Fixed and item-wise fees | Fee line types |
| Q-Q7 | Standard terms: validity, revisions, visits, exclusions, cancellation, ownership | Text blocks |
| Q-F1 | Bills issued, or payments against the agreement only (**billing mode**) | All of `WORKFLOWS.md` B |
| Q-F2 | Payment stages | Milestones |
| Q-F3 | GST registration, GSTIN, rate, SAC, invoice format | Tax tables, bill type |
| Q-F6 | Receipts: format and numbering | Payments |
| Q-U1 | Users, roles, who sees finances | `PERMISSION_MATRIX.md` |
| Q-H1 | Domain | Deployment |
| Q-H2 | Hosting plan and capabilities | Folder layout, PHP version, bcmath, GD, cron |

**P2 / P3**
- Q-G4 (single enquiry list — R-01) · Q-G5 (reminder channel) · Q-G6 (client portal)
- Q-G7 (how long to keep enquiry data) · Q-G8 (date format / financial year)
- Q-G10 (data import)
- Q-S3 (project types) · Q-S4 (services shown on the website)
- Q-W2 (Gallery page — R-02) · Q-W6 (enquiry email recipients, CAPTCHA)
- Q-W7 (testimonials, registration) · Q-W8 (Marathi) · Q-W9 (About text)
- Q-B2 (colours and fonts)
- Q-Q6 (amount in words, client block, acceptance block) · Q-Q8 (statuses, who approves)
- Q-Q9 (email quotations) · Q-Q10 (signature)
- Q-F4 (discounts and their approval) · Q-F5 (extra charges) · Q-F7 (payment modes)
- Q-F8 (expenses scope)
- Q-P1 (project statuses — C-02) · Q-P2 (project code format) · Q-P3 (site-visit log)
- Q-D1 (file types and sizes)
- Q-U2 (mobile use) · Q-U3 (two-factor login) · Q-R1 (reports)
- Q-H3 (staging site) · Q-H4 (off-site backup) · Q-H5 (domain email)

**New client questions raised by this package** — to be added to `CLIENT_QUESTIONS.md` once
approved:

| ID | Pri | Question |
|---|---|---|
| Q-F9 | P2 | Do you ever refund money to clients (overpayment, cancelled project)? Who approves it? |
| Q-F10 | P2 | If a client never pays a balance, should the ERP allow a write-off (ADM only)? |
| Q-F11 | P2 | Should credit from one project be transferable to another project of the same client? |
| Q-P4 | P2 | Do you hold meetings or site visits before a project is confirmed, and should these be recorded on the enquiry? |

### 4.2 Developer decisions (for you)

| ID | Decision | Proposed default | Reference |
|---|---|---|---|
| D-01 | Re-qualify "CONFIRMED (brief)" items as BRIEF-UNVERIFIED; either add the brief to `reference/brief/` or re-affirm the items | Re-affirm in the decision log | GAP §2 |
| D-02 | Initialise Git at Stage 1 (now) | Yes | C-12 |
| D-03 | Record Stage 0 as accepted, and treat this package as Stage 1 | Yes | C-18 |
| D-04 | Separate database logins for public and ERP | Yes, if the host allows it; otherwise one | SECURITY §1 |
| D-05 | Single download route `/erp/documents/{id}/download` | Yes | C-11 |
| D-06 | One generic `lookups` table for simple lists | Yes | R-07 |
| D-07 | Workflow statuses fixed in code, labels editable | Yes | R-08 |
| D-08 | Enable the lock-date feature | Yes, empty by default | WORKFLOWS B.10 |
| D-09 | Take the quotation number when the draft is created, or on first send | On creation | WORKFLOWS A.4 |
| D-10 | Calculation order: lines → subtotal → discount → tax → rounding | As proposed | WORKFLOWS A.5 |
| D-11 | Credit transfer between projects | ADM only, linked entries | WORKFLOWS B.4 |
| D-12 | Payment reversals: same sequence as payments, or a separate one | Same sequence | WORKFLOWS B.5 |
| D-13 | Include the write-off feature | Build only if Q-F10 = yes | WORKFLOWS B.8 |
| D-14 | Expenses: posted when saved, or editable until the lock date | Posted when saved | WORKFLOWS B.9 |
| D-15 | Optional database triggers to block changes to posted financial rows | No (PHP enforcement); reconsider in Stage 11 | DATABASE §4 |
| D-16 | Password policy (minimum 10 characters, not the same as the username) | As proposed | SECURITY §3 |
| D-17 | ERP cookie SameSite setting: Lax or Strict | Lax | SECURITY §4 |
| D-18 | PDF library: Dompdf or mPDF | mPDF if Devanagari is needed (Q-Q2, Q-W8) | Q-T1 |
| D-19 | Use WorkLedger as a style reference | Style only; nothing reused for security | Q-G3, CLAUDE §4 |
| D-20 | Approve errata C-01 … C-18 and their changes to the original documents | — | GAP §3 |
| D-21 | Approve the duplicate resolutions R-01 … R-08 and the optional-feature switches | — | GAP §4–5 |
| D-22 | Approve the database design (49 tables) as the basis for `database.sql` v1 | — | DATABASE_DESIGN |
| D-23 | Approve the permission matrix as the starting role default | — | PERMISSION_MATRIX |

## 5. Changes to make to the original files after approval (not done yet)

| File | Change |
|---|---|
| `CLAUDE.md` | Stage line; document map (add the 7 new files); Git timing (D-02) |
| `project-context/BUSINESS_REQUIREMENTS.md` | Re-tag BRIEF-UNVERIFIED; add billing mode, refunds, credit; update E-19 / E-20 |
| `project-context/MODULES.md` | C-01 … C-10, C-14 … C-17; merge module 12 into 2 |
| `project-context/DATABASE_RULES.md` | Backup retention (C-13); lookups (D-06); refunds, write-offs |
| `project-context/SECURITY_RULES.md` | Download route (C-11) |
| `project-context/DEVELOPMENT_ROADMAP.md` | §3 plan above; decision-log entries |
| `docs/CLIENT_QUESTIONS.md` | Add Q-F9, Q-F10, Q-F11, Q-P4 |
| `docs/TECHNICAL_REQUIREMENTS.md` | Backup retention wording; download route |
