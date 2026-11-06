# Stage 1 Documentation Consistency Report

| | |
|---|---|
| Date | 2026-11-06 |
| Repository / branch | GitHub `codintdigitechdev/AJ_Design_Studio`, `main`; base commit `12d7634`. Local working copy `R:\CID\Clients\AJ_Design_Studio` |
| Change state | 23 files modified + 2 files added, **not committed, not pushed** |
| Scope | Step 1 — full documentation correction. No application code, SQL or production data touched |
| Verdict | Documents are **mutually consistent** for the checks in §3. **Stage 1 is NOT approved**: open client and developer decisions remain (§4, §5) |

---

## 1. What was done

1. Synchronised the local folder with GitHub `main` (developer-approved). The GitHub copy matched the
   local documents except for line endings and one extra file, `reference/portfolio/Senior office profile.pdf`.
2. Audited every item C-01…C-18, R-01…R-08, DB-01…DB-23, WF-01…WF-16, PM-01…PM-18, PG-01…PG-15
   (plus INC/MR items) against the documents — results in `docs/STAGE1_CORRECTION_TRACKING_MATRIX.md`.
3. Corrected the documents in place, preserving valid existing content and IDs.
4. Recorded the 26 client decisions with date and source (`docs/CLIENT_QUESTIONS.md` §0), as reported
   — not as written client confirmations.
5. Marked the two old review packages **SUPERSEDED** and the gap-resolution and audit reports with
   status banners. Nothing was deleted or renamed.
6. Restored Windows (CRLF) line endings so the Git diff shows only real changes.

## 2. Files

| File | Change |
|---|---|
| `CLAUDE.md` | Rewritten: repository, stage, full document map (24 documents), new tag scheme, references incl. visiting card and non-AJ profile PDF, client decisions, Admin-only finance |
| `project-context/PROJECT_OVERVIEW.md` | Facts from the visiting card, domain, commission stakeholders, assumption A7 |
| `project-context/BUSINESS_REQUIREMENTS.md` | E-21 financial-data definition; E-22…E-25; W-14…W-20; Q-R10…Q-R12; scope §7 |
| `project-context/MODULES.md` | Errata applied; ACC removed; module 18 Commission; billing method, GST, demo services, portfolio rules |
| `project-context/DATABASE_RULES.md` | Lookup FKs, allocation XOR, one active agreement, GST §8, commission integrity, files owner, retention, encryption |
| `project-context/SECURITY_RULES.md` | §8.1 Admin-only enforcement; file route; private portfolio originals; partner privacy |
| `project-context/UI_UX_GUIDELINES.md` | Visiting-card letterhead, tone of voice, ADM-only finance UI, no commission on PDFs |
| `project-context/DEVELOPMENT_ROADMAP.md` | Stage table updated; version control; **decision log** entries |
| `docs/DATABASE_DESIGN.md` | 58 tables: commission group I, credit transfers, tax-line tables, billing method, source fields, file owner, portfolio fields, integrity rules |
| `docs/WORKFLOWS.md` | Parts A–D: Admin decisions, conversion order, per-project billing, GST per document, formulas, partial payments, commission lifecycle, portfolio publishing, tests |
| `docs/PERMISSION_MATRIX.md` | ADM/STF/SITE; every financial row ADM-only; partner and commission rows; response rules |
| `docs/ERP_PAGES_AND_FIELDS.md` | Partner/commission pages and fields; file route; GST and billing fields; ADM-only markers on routes and AJAX |
| `docs/WIREFRAMES.md` | ADM-only finance panels; letterhead; allocation by method; portfolio editor; W-E11/W-E12 commission |
| `docs/CLIENT_QUESTIONS.md` | §0 client decisions; status per question; 15 new questions; P1 summary |
| `docs/PROJECT_SCOPE.md`, `docs/QUOTATION_ANALYSIS.md`, `docs/PORTFOLIO_WEBSITE_PLAN.md`, `docs/TECHNICAL_REQUIREMENTS.md` | Aligned with the client decisions and the corrected design |
| `docs/STAGE1_ROADMAP_AND_DECISIONS.md` | Decision register D-01…D-37 with status; assumptions A1…A14 |
| `docs/STAGE1_GAP_RESOLUTION.md`, `docs/STAGE1_CONSOLIDATED_CORRECTION_REPORT.md` | Status banner only |
| `docs/STAGE1_REVIEW_PACKAGE.md`, `docs/STAGE1_REVIEW_PACKAGENew.md` | SUPERSEDED banner only |
| **New:** `docs/STAGE1_CORRECTION_TRACKING_MATRIX.md`, this report | Tracking and consistency records |

## 3. Consistency checks performed

All checks ran on the current (non-superseded) documents. "Pass" means the search or read-through found no conflicting statement.

| # | Check | Method | Result |
|---|---|---|---|
| 1 | No finance rights for any non-ADM role (no ACC, no STF/SITE finance) | Search for `ACC`; read PERMISSION_MATRIX, MODULES, WORKFLOWS, ERP_PAGES, WIREFRAMES | Pass — ACC appears only as "removed" |
| 2 | Admin-only finance covers pages, APIs/AJAX, reports, exports, PDFs, notifications/digests, timelines, follow-ups, documents, settings | Read SECURITY §8.1, PERMISSION §3, ERP_PAGES §1 markers | Pass |
| 3 | Commission present in database, workflows, permissions, pages, wireframes, reports, scope, roadmap | Search per file (commission mentioned in 18 of 19 current docs; the website plan correctly has none) | Pass |
| 4 | Commission never automatic, never on Direct projects, Admin-only, never on client documents | Read BR E-23/E-24, DBD I2/§4, WF C.1/C.2, UI §7, WFR W-E7/W-E11 | Pass |
| 5 | Per-project billing method replaces the studio-wide mode everywhere | Search "billing mode / Mode A / Mode B" | Pass — appears only as "superseded" |
| 6 | GST optional per document, off by default, dormant until registration known | Read DBR §8, DBD A8/E2/F1–F10, WF A.5, PG §2.9–2.11, QA §5 | Pass |
| 7 | Partial payments always allowed; advances; XOR allocation | Read WF B.4, DBD F11/F12/§4, PG §2.12, WFR W-E8 | Pass |
| 8 | One file-download route | Search `download.php` and the route | Pass — only `/erp/files/{id}/download` (old name mentioned as removed) |
| 9 | Quotation statuses (no "Revised"); "Proposal" replaces "Enquiry stage" | Search | Pass |
| 10 | Table names consistent (`quotation_revision_items` gone) | Search | Pass — mentioned only as replaced |
| 11 | Backup retention identical | Search "4 weekly" | Pass — 7/4/3 in both |
| 12 | Every question ID used is defined in CLIENT_QUESTIONS | Automated comparison | Pass (Q-R* are business-rule IDs, defined in BR §5) |
| 13 | Every D-ID used is in the decision register | Automated comparison | Pass |
| 14 | CD-01…CD-26 consistent with the client decisions supplied | Read CQ §0 against the developer's brief | Pass |
| 15 | Old tags removed from current docs | Search `[CONFIRMED]`, "CONFIRMED (brief)", "PENDING APPROVAL", "BRIEF-UNVERIFIED" | Pass — only the legacy note in `CLAUDE.md` §3 |
| 16 | Domain recorded consistently; spelling confirmation flagged | Search | Pass |
| 17 | Non-AJ profile PDF never used as AJ content | Read CLAUDE §4, OV §3.5, SC §3, PWP, UI §5, DBR §11, SEC §10 | Pass |
| 18 | `CLAUDE.md` document map lists every document in `project-context/` and `docs/` | Compared with the folder listing (7 + 17 files incl. the 2 new ones) | Pass |
| 19 | No pending item presented as approved | Read decision log and register: only the sync is "Done"; everything else PENDING | Pass |

**Not checked / limitations:**
- Superseded files (`STAGE1_REVIEW_PACKAGE*.md`) and the historical audit report still contain the old
  content by design; they are bannered.
- No calculations or tests were executed — test cases are documented for Stage 9/11 only.
- Wording consistency was checked by targeted searches and reading, not by a full line-by-line proof of
  every sentence in the 1,779-line superseded package.

## 4. Unresolved client decisions (impact)

P1 — block Stage 1 approval:

| ID | Decision needed | Impact while open |
|---|---|---|
| Q-C1 | Commission direction; one or several partners per project | Model assumes studio pays one partner (A7) |
| Q-C2 | "Referral" as a separate source value? | `source_type` limited to Direct/Contractor |
| Q-C3 | Commission base, timing, effect of variations/refunds/write-offs | `base_type` and earned-to-date calculation not final |
| Q-C4 | Tax on commission (TDS/GST), PAN | Tax fields dormant |
| Q-F3 | GST registration, GSTIN, rate, SAC, advances | GST dormant; quotations and bills work without GST |
| Q-F2 | Stage percentages incl./excl. GST | Stage calculation basis open |
| Q-U4 | Staff scope drafting, sending, expense claims | All treated as "not allowed" |
| Q-U1 | Actual ERP users | STF/SITE roles may be unused |
| Q-W1 | Photo source, "major" projects | Portfolio cannot be populated |
| Q-G11 | Purpose of the non-AJ profile PDF | Not used at all |
| Q-S2 | Meaning of Temple Work / कोकण शिल्प / Complete Project; design-only? | Services and scope boundary |
| Q-S5 | Demo services on the live website? | Demo services hidden publicly |
| Q-S1 | Final service list | Demo list used in the ERP |
| Q-W3 / Q-W4 | Address spelling; WhatsApp and published numbers | Contact page and letterhead not final |
| Q-W5 | Consent process detail | Publish requires a recorded consent |
| Q-Q2 | "श्री" and Instagram QR on letterhead | Optional settings; PDF library choice (D-18) |
| Q-Q3, Q-Q7 | Area basis; standard terms | Quotation text blocks blank |
| Q-F6 | Receipt format | Numbering proposal only |
| Q-H1 | Domain spelling `ajdesignstudios.in` | DNS/SSL waits |
| Q-H2 | Hosting plan and capabilities | Folder layout, PHP version unverified |
| Q-G1, Q-G2, Q-G9, Q-B1 | Current tracking; default path; phasing; vector logo | Workflow defaults and launch plan |

P2/P3 open items: `docs/CLIENT_QUESTIONS.md` (incl. Q-C5, Q-C6, Q-F9…Q-F12, Q-W11, Q-P4).
Also outstanding: **written confirmation** of CD-01…CD-26 (date and channel).

## 5. Assumptions and proposed decisions requiring approval

- **Developer decisions:** D-03…D-37 in `docs/STAGE1_ROADMAP_AND_DECISIONS.md` §4.2. Most significant:
  D-26 billing method · D-27 GST structure · D-28 numbering · D-29 allocation rule · D-30 roles ·
  D-31 portfolio storage · D-32 commission model · D-33 financial filtering · D-34 file access ·
  D-36 backup encryption · D-37 content drafting · D-20/D-21 errata · D-22 database design · D-23 matrix.
- **Assumptions:** A1…A14 in the same file §4.3 (notably A7 commission direction, A13 staff limits,
  A14 partner visibility).

## 6. Readiness

| Gate criterion | State |
|---|---|
| Documents reflect the client decisions and are mutually consistent | **Met** (this report; tracking matrix) |
| P1 client questions answered or deferred with agreed defaults | Not met (§4) |
| Developer decisions approved | Not met (§5) |
| Client decisions confirmed in writing | Not met |
| Stage 0 acceptance and Stage 1 approval recorded in the decision log | Not met |

**Stage 1 remains NOT APPROVED.** The final Stage 1 approval package has not been created, as instructed.

## 7. Addendum — client answers recorded 2026-11-06 (CD-27…CD-90)

Sections 4–6 above describe the state before these answers. After them:

- **Recorded:** CD-27…CD-30 (assumptions A2, A5, A8, A10) and CD-31…CD-90 (the question list, plus
  follow-up choices made in the development session) in `docs/CLIENT_QUESTIONS.md` §0 and the decision log.
- **Applied to:** `CLAUDE.md`, all 7 project-context files, `DATABASE_DESIGN`, `WORKFLOWS`,
  `PERMISSION_MATRIX`, `ERP_PAGES_AND_FIELDS`, `WIREFRAMES`, `PROJECT_SCOPE`, `QUOTATION_ANALYSIS`,
  `PORTFOLIO_WEBSITE_PLAN`, `TECHNICAL_REQUIREMENTS`, `STAGE1_ROADMAP_AND_DECISIONS`.
- **Main design changes:** separate Website Enquiries inbox (new `website_enquiries` table; still 58
  tables because `credit_transfers` was removed); Gallery merged into Portfolio; project statuses
  Planned/OnGoing/OnHold/Completed/HandOver/Cancelled; Direct/Contractor/Referral sources; commission
  on final fee excl. GST, payable on completion; refunds with % deduction; advances at enquiry stage;
  English + Marathi website and documents (mPDF); built-in CAPTCHA; quotation number
  `AJDS/Q/{fy}/{seq3}`; GST designed but off (not registered).
- **Checks re-run:** a search for every answered question ID without its decision reference, for
  credit transfers, the old Gallery page, the old statuses and "New – unreviewed" found only
  intentional references (superseded notes and the sample-quotation analysis).
- **Open:** Q-H2 hosting provider (the only P1 item), Q-C4 TDS, Q-S1/Q-S4, Q-W1, Q-W3, Q-W7, Q-Q8.
  New developer decisions D-38…D-41 added to the register.
- **Still not met:** written client confirmation of CD-01…CD-90, developer approval of D-03…D-41,
  Stage 0 acceptance and the Stage 1 approval entry.
