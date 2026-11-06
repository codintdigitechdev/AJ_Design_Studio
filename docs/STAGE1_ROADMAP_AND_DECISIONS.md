# Stage 1 Roadmap and Decision Register

**Status: PROPOSED — Stage 1 not approved.** Corrected 2026-11-06. The stage table and the decision
log live in `project-context/DEVELOPMENT_ROADMAP.md`; this file is the **register of every decision
still requiring approval**. Tags: `CLAUDE.md` §3.

---

## 1. Where the project stands (2026-11-06)

| Stage | Status |
|---|---|
| 0 Discovery & documentation | Complete. **Acceptance not recorded** (D-03) |
| 1 Architecture & database design | Design documents produced and **corrected for the client decisions** (`docs/STAGE1_CORRECTION_TRACKING_MATRIX.md`). **Not approved** |
| 2–12 | Not started. Implementation blocked by the gate in `CLAUDE.md` |

## 2. Stage 1 deliverables

| Deliverable | File | State |
|---|---|---|
| Final module list | `project-context/MODULES.md` (incl. module 18 Commission) | Corrected — PROPOSED |
| ER diagram + table design (58 tables) | `docs/DATABASE_DESIGN.md` | Corrected — PROPOSED |
| Role / permission matrix (ADM, STF, SITE; finance ADM-only) | `docs/PERMISSION_MATRIX.md` | Corrected — PROPOSED; Q-U1, Q-U4, Q-C5 answered (CD-74, CD-80, CD-83) |
| Folder structure | `docs/TECHNICAL_REQUIREMENTS.md` §2 | Corrected — PROPOSED |
| URL map | `docs/ERP_PAGES_AND_FIELDS.md` §1 + `docs/PORTFOLIO_WEBSITE_PLAN.md` §2 | Corrected — PROPOSED |
| Quotation calculation spec | `docs/WORKFLOWS.md` A.4–A.6 | Corrected — PROPOSED; Q-Q3, Q-F2 answered (CD-54, CD-59) |
| Financial workflow | `docs/WORKFLOWS.md` Part B | Corrected — PROPOSED; Q-F3, Q-F9…F12 answered (CD-60, CD-66…CD-69) |
| Commission workflow | `docs/WORKFLOWS.md` Part C | New — PROPOSED; rules answered (CD-70…CD-75); TDS open (Q-C4) |
| Portfolio publishing workflow | `docs/WORKFLOWS.md` Part D | New — PROPOSED |
| Field specifications | `docs/ERP_PAGES_AND_FIELDS.md` §2 | Corrected — PROPOSED |
| Wireframes | `docs/WIREFRAMES.md` | Corrected — PROPOSED |
| PDF library choice | `docs/TECHNICAL_REQUIREMENTS.md` §1 | mPDF required by CD-50/CD-53 — D-18 approval PENDING |
| Host capability check | — | Not possible until Q-H2 |

### Stage 1 gate — exit criteria (PROPOSED)
1. All P1 client questions answered, or deferred with an agreed default (`docs/CLIENT_QUESTIONS.md` §10).
2. Developer decisions in §4.2 decided.
3. Client decisions CD-01…CD-90 confirmed in writing (date and channel filed).
4. Decision log records "Stage 1 architecture and database design approved — date — approved by".

## 3. Stage plan
See `project-context/DEVELOPMENT_ROADMAP.md` §1 (stages 0–12, updated for commission, per-project
billing, optional GST and Admin-only finance). Website and ERP delivered together (CD-37).

---

## 4. Decision register — everything still requiring approval

### 4.1 Client decisions still open
Master list with status: `docs/CLIENT_QUESTIONS.md`. P1 items: §10 of that file. New questions added
in this correction: Q-G11, Q-S5, Q-W11, Q-F9, Q-F10, Q-F11, Q-F12, Q-C1…Q-C6, Q-P4, Q-U4.
Answers received 2026-11-06: CD-31…CD-90. Still open: **Q-H2** hosting provider (P1); Q-S1, Q-S4,
Q-W1 (which projects are major), Q-W3 (map pin, office hours), Q-W7 (CoA number), Q-C4 (TDS), Q-Q8.

### 4.2 Developer decisions (PROPOSED defaults — none approved)

| ID | Decision | Proposed default | Status | Reference |
|---|---|---|---|---|
| D-01 | Re-qualify brief items | **Superseded by D-25** | — | GAP §2 |
| D-02 | Initialise Git at Stage 1 | Folder synced as a working copy of GitHub `main` on 2026-11-06 (developer instruction). Commit/push policy: only with explicit permission | Partly done | C-12, D-24 |
| D-03 | Record Stage 0 acceptance | Yes | PENDING | C-18 |
| D-04 | Separate DB logins public/ERP | Yes if the host allows | PENDING | SECURITY §1 |
| D-05 | Single download route | **Superseded by D-34** (`/erp/files/{id}/download`) | — | C-11 |
| D-06 | One generic `lookups` table | Yes, with real FKs | PENDING | R-07 |
| D-07 | Statuses fixed in code, labels editable | Yes | PENDING | R-08 |
| D-08 | Lock date feature | Yes, empty by default | PENDING | WORKFLOWS B.10 |
| D-09 | When the quotation number is taken | **Superseded by D-28** (on first send) | — | — |
| D-10 | Calculation order lines → discount → GST → rounding | As proposed | PENDING | WORKFLOWS A.5 |
| D-11 | Credit transfer between projects | **Withdrawn** — client said no (CD-68); table removed | Closed | DB-07 |
| D-12 | Payment reversals: same sequence or separate `RV` | Proposal changed to **separate `AJDS/RV/…`** (D-28) | PENDING | WORKFLOWS B.11 |
| D-13 | Write-off feature | Included, ADM only (CD-67) | Closed by client decision | WORKFLOWS B.8 |
| D-14 | Expenses posted on save | Yes | PENDING | WORKFLOWS B.9 |
| D-15 | DB triggers for posted rows | No (PHP); reconsider in Stage 11 | PENDING | DATABASE_DESIGN §4 |
| D-16 | Password policy ≥ 10, ≠ username | Yes | PENDING | SECURITY §3 |
| D-17 | SameSite Lax | Lax | PENDING | SECURITY §4 |
| D-18 | PDF library | **mPDF** — required for "श्री" and Marathi documents (CD-50, CD-53) | PENDING developer approval | Q-T1 |
| D-19 | WorkLedger as style reference | Style only | PENDING | Q-G3 |
| D-20 | Approve errata C-01…C-18 | Applied to the documents as PROPOSED on 2026-11-06; approval still required | PENDING | GAP §3 |
| D-21 | Approve R-01…R-08 and feature switches | Applied as PROPOSED; R-01 (merged enquiries) superseded by CD-31 and R-02 (gallery switch) by CD-44 | PENDING | GAP §4–5 |
| D-22 | Approve the database design | 58 tables (`DATABASE_DESIGN.md`) | PENDING | DB-23 |
| D-23 | Approve the permission matrix | ADM / STF / SITE, finance ADM-only | PENDING | PERMISSION_MATRIX |
| D-24 | Authoritative copy | GitHub `main`; local folder is a working copy (done 2026-11-06) | Done (sync); commit policy PENDING | INC-12 |
| D-25 | Status tag scheme | CONFIRMED-REF / CLIENT-DECISION / BRIEF / PROPOSED / ASSUMPTION / PENDING — applied in `CLAUDE.md` §3 and corrected documents | PENDING approval | INC-04 |
| D-26 | Billing flexibility | Per-project billing method (agreement / bills) with a studio default; ad-hoc bills; change while no issued bill | PENDING | WF-01, DB-04 |
| D-27 | GST structure | Studio GST profile + per-document "Apply GST" (off by default) + per-document tax-line tables | PENDING (studio not registered — CD-60) | WF-02 |
| D-28 | Numbering formats | Quotation `AJDS/Q/{fy}/{seq3}` **approved by the client (CD-52)**; others follow `AJDS/{type}/{fy}/{seq}`; number on first send; reversals `AJDS/RV/…` | Partly decided — non-quotation formats PENDING | WORKFLOWS B.11 |
| D-29 | Allocation target rule | Exactly one of bill / stage / agreement | PENDING | DB-06 |
| D-30 | Default roles | ADM, STF, SITE; ACC removed; only ADM in use now (CD-80) | PENDING | PM-14 |
| D-31 | Portfolio storage | Private originals; public copies on publish; withdrawn on unpublish/remove | PENDING | MR-09 |
| D-32 | Commission model | `DATABASE_DESIGN.md` group I + `WORKFLOWS.md` Part C | PENDING (rules from CD-70…CD-75; TDS Q-C4) | CM |
| D-33 | Financial response filtering | Central financial-field registry used by every renderer | PENDING | PM-15 |
| D-34 | Private file access | `files.owner_type/owner_id` + `/erp/files/{id}/download`; financial downloads audited | PENDING | MR-11 |
| D-35 | Superseded review packages | Banner, no deletion (done) | Done (banner); approval PENDING | INC-02/03 |
| D-36 | Off-site backup encryption | Encrypted archives, key held by ADM | PENDING | MR-12 |
| D-37 | Website content drafting | CodInt drafts from Instagram/references; review status; nothing unreviewed at launch | PENDING | MR-07 |
| D-38 | Website enquiries inbox | Separate `website_enquiries` table and inbox with conversion (implements CD-31; replaces the R-01 merge) | PENDING | CD-31 |
| D-39 | Marathi implementation | `*_mr` fields on public content; Marathi document templates; `/mr/` URLs with hreflang; ERP stays English | PENDING | CD-50 |
| D-40 | Commission payable on completion | Approved commission becomes payable when the project reaches Completed or HandOver; fee variations create automatic commission adjustments | PENDING | CD-72 |
| D-41 | Built-in CAPTCHA | Self-hosted arithmetic or image challenge; no third-party service | PENDING | CD-48 |

### 4.3 Assumptions requiring validation
Answers given by the client are kept in the developer's original words; validated rows now point to
the client decision recorded in `docs/CLIENT_QUESTIONS.md` §0.

| ID | Assumption | Validated by / client answer | Status |
|---|---|---|---|
| A1 | 1–5 ERP users | Only the Admin for now (CD-80) | **CLIENT-DECISION (CD-80)** |
| A2 | INR only, Indian format | Yes INR Only | **CLIENT-DECISION (CD-27)** — INR only. Indian number formatting stays PROPOSED |
| A3 | sq.ft default, sq.m possible | Area bases answered (CD-54); unit default still assumed | ASSUMPTION |
| A4 | English v1, Marathi optional | English + Marathi website and documents (CD-50) | **Replaced by CLIENT-DECISION (CD-50)** |
| A5 | Single office | Right now just single office only | **CLIENT-DECISION (CD-28)** — single office for now; multi-branch stays out of scope |
| A6 | Design and supervision only, no construction | Confirmed (CD-40) | **CLIENT-DECISION (CD-40)** |
| A7 | Studio pays commission to one partner per project | Confirmed (CD-70) | **CLIENT-DECISION (CD-70)** |
| A8 | Ar. Ajit Kumbhar has decision authority | Yes he is business owner / Main Admin USer as well | **CLIENT-DECISION (CD-29)** — owner, decision authority and main Admin (ADM) user |
| A9 | DD/MM/YYYY; FY April–March | Confirmed (CD-35, CD-36) | **CLIENT-DECISION (CD-35, CD-36)** |
| A10 | Asia/Kolkata | Maharashtra (Mumbai) Not Much Outside Mh now | **CLIENT-DECISION (CD-30)** — operations mainly within Maharashtra; time zone Asia/Kolkata (IST) |
| A11 | Client supplies photos, project facts, consent, final services; CodInt drafts terms | Photos CD-43; terms CD-56; services Q-S1 | Partly CLIENT-DECISION |
| A12 | Host supports PHP 8.1+, cron, GD, bcmath, `finfo`, HTTPS, folders outside web root | Q-H2 | ASSUMPTION |
| A13 | Staff may not draft quotation scope, send quotations or claim expenses | Confirmed (CD-83) | **CLIENT-DECISION (CD-83)** |
| A14 | Partner names/sources hidden from staff | Confirmed (CD-74) | **CLIENT-DECISION (CD-74)** |

## 5. Follow-up after approval
Once D-20…D-37 and the P1 questions are settled: record them in the decision log, change the affected
tags from PROPOSED to approved wording, and run a short re-check of the changed sections.
