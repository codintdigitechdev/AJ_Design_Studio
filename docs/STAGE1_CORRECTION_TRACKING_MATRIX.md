# Stage 1 Correction Tracking Matrix

| | |
|---|---|
| Date | 2026-11-06 |
| Repository | GitHub `codintdigitechdev/AJ_Design_Studio`, branch `main`, base commit `12d7634`; changes **uncommitted** in the local working copy |
| Inputs | `docs/STAGE1_CONSOLIDATED_CORRECTION_REPORT.md`, `docs/STAGE1_GAP_RESOLUTION.md`, all current documents |
| Status | Documentation corrected. **Nothing here is an approval** — every design change is PROPOSED; open client items stay PENDING |

**"Found" column** — state of the item in the documents at the start of this correction:
**Implemented** (already correct) · **Partial** (correct in some documents only) · **Missing** · **Contradictory**.

**"Result" column:**
- **Corrected** — the change is now in every affected document (verified by reading and by
  cross-document search). The design is still PROPOSED.
- **Corrected – PENDING Q-x** — the design is in place, but the business rule waits for a client
  answer. The document says so and states the impact.
- **Superseded** — replaced by a later item, as stated.
- **Done** — an operational action, not a design change.

Abbreviations: BR = BUSINESS_REQUIREMENTS · MOD = MODULES · DBR = DATABASE_RULES · SEC = SECURITY_RULES ·
UI = UI_UX_GUIDELINES · RM = DEVELOPMENT_ROADMAP · OV = PROJECT_OVERVIEW · DBD = DATABASE_DESIGN ·
WF = WORKFLOWS · PM = PERMISSION_MATRIX · PG = ERP_PAGES_AND_FIELDS · WFR = WIREFRAMES ·
CQ = CLIENT_QUESTIONS · SC = PROJECT_SCOPE · QA = QUOTATION_ANALYSIS · PWP = PORTFOLIO_WEBSITE_PLAN ·
TR = TECHNICAL_REQUIREMENTS · S1R = STAGE1_ROADMAP_AND_DECISIONS.

---

## 1. Gap-resolution errata C-01…C-18 (`STAGE1_GAP_RESOLUTION.md` §3)

| ID | Found | Result | Affected files | Resolution |
|---|---|---|---|---|
| C-01 | Partial (WF only) | Corrected – PENDING Q-G2 | BR §2, MOD §2/§6, WF A.1 | Quotation from an enquiry or a project; both paths documented; default path open |
| C-02 | Partial | Corrected – PENDING Q-P1 | MOD §4, WF A.3, RM | "Enquiry stage" replaced by "Proposal" |
| C-03 | Partial | Corrected | MOD §2/§4, WF A.1/A.2 | Pre-project meetings and visits are enquiry activities |
| C-04 | Contradictory (MOD, BR, QA, CQ still had "Revised") | Corrected – PENDING Q-Q8 | BR Q-R07, MOD §6, QA §5, CQ Q-Q8, WF A.4, DBD E2 | Revision statuses incl. Superseded; no "Revised" |
| C-05 | Contradictory (MOD §12) | Corrected | MOD P5/§2, PWP §3, DBD H1 | WhatsApp click = counter only |
| C-06 | Partial | Corrected – PENDING Q-G4 | MOD §2/§12, PWP | Website enquiries merged into the enquiry module |
| C-07 | Partial (studio-wide mode) | **Superseded** by WF-01 / D-26 | MOD §7, WF B.3, DBD D1/A8 | Per-project billing method replaces the studio-wide mode |
| C-08 | Missing in MOD | Corrected | MOD §1/§14, WFR W-E2/W-E5 | Agreed / Billed / Received / Outstanding (ADM only) |
| C-09 | Partial | Corrected | MOD §2, DBD C2/C3, PG §2.2 | Preferred contact, consent, services on enquiries |
| C-10 | Partial | Corrected | MOD §1, PM §3, WFR W-E2 | Dashboard filtered by permission and record rules |
| C-11 | Contradictory (SEC `download.php` vs TR route) | Corrected (extended by D-34) | SEC §5, TR §2.2, PG §1.7, DBD A11 | Single route `/erp/files/{id}/download`, owner-resolved |
| C-12 | Contradictory (Stage 1 vs 2) | **Done** (sync) – commit policy PENDING D-02 | RM §4, CLAUDE header/§10, S1R D-02/D-24 | Folder synced as working copy of `main`; commits only with permission |
| C-13 | Contradictory | Corrected – PENDING Q-H2/Q-H4 | DBR §12, TR §7 | 7 daily / 4 weekly / 3 monthly |
| C-14 | Partial | Corrected – PENDING Q-F9 | MOD §8, WF B.6, DBD F14, PG §1.11 | Refunds as a separate optional document |
| C-15 | Partial | Corrected | MOD §8, WF B.4, PG §2.12 | Credit/advance and apply-credit; formula covers both methods |
| C-16 | Partial | Corrected – PENDING Q-F5/Q-F8 | MOD §9, WF B.7, DBD F7 | Reimbursable expense → bill line, off by default |
| C-17 | Partial | Corrected – PENDING Q-F5/Q-P3 | MOD §4, WF B.7, DBD D5/F7 | Chargeable visit → bill line; link stored once |
| C-18 | Contradictory | Corrected – PENDING D-03 | RM §1/§5, CLAUDE header, S1R §1 | Stage 0 / Stage 1 naming fixed; Stage 0 acceptance still to record |

## 2. Duplicate resolutions R-01…R-08 (`STAGE1_GAP_RESOLUTION.md` §4)

| ID | Found | Result | Affected files | Resolution |
|---|---|---|---|---|
| R-01 | Partial | Corrected – PENDING Q-G4 | MOD §2/§12, PG §1.3 | One enquiry module with "New – unreviewed" queue |
| R-02 | Partial | Corrected – PENDING Q-W2 | MOD P3, DBD G3, PWP | Gallery = portfolio images with gallery switch |
| R-03 | Partial | Corrected | MOD §2/§4, WF A.2 | Enquiry activities vs project site visits |
| R-04 | Partial | Corrected | MOD P1/§16, DBD A8, PG §2.18 | Website content edited only in Settings, with review status |
| R-05 | Implemented (DBD) | Corrected (no change needed beyond PM-16) | DBD C4/C5 | One activity log + follow-ups |
| R-06 | Implemented | Corrected | DBR §9, DBD A7/C4 | Audit log vs activity log kept separate |
| R-07 | Implemented (DBD) | Corrected – PENDING D-06 | DBR §2, DBD A10 | Generic lookups with real FKs |
| R-08 | Implemented (DBD) | Corrected – PENDING D-07 | DBR §2 | Fixed statuses, editable labels |

## 3. Database design DB-01…DB-23

| ID | Found | Result | Affected files | Resolution |
|---|---|---|---|---|
| DB-01 | Missing | Corrected – PENDING Q-C1…Q-C4 | DBD §2/§3 group I, DBR §6, A9 | 5 commission tables; commission-payment sequence |
| DB-02 | Missing | Corrected – PENDING Q-C2 | DBD D1, PG §2.5, MOD §4 | `source_type`, `referral_partner_id` with rules |
| DB-03 | Missing | Corrected | DBD C2, PG §2.2, MOD §2 | Partner on enquiry; contractor/referral sources |
| DB-04 | Contradictory | Corrected – PENDING D-26 | DBD A8/D1, PG §2.5/§2.18 | `default_billing_method` + `projects.billing_method` |
| DB-05 | Missing | Corrected – PENDING Q-F3 | DBD F1–F4 | GST switch, taxable amount and tax lines on agreements and variations |
| DB-06 | Contradictory (double-count risk) | Corrected – PENDING D-29 | DBD F12/§4, DBR §6, WF B.4 | XOR allocation target |
| DB-07 | Missing | Corrected – PENDING Q-F11 | DBD F13, WF B.4, PG §1.11 | `credit_transfers` table (optional) |
| DB-08 | Contradictory | Corrected | DBD F1/§4, DBR §6, WF B.2 | One **active** agreement per project |
| DB-09 | Missing | Corrected – PENDING Q-F3 | DBD F9/F10 | Credit-note tax lines and taxable amount |
| DB-10 | Missing | Corrected – PENDING Q-F12 | DBD F11/§4, PG §2.12 | Client consistency rule; pre-project advance only if allowed |
| DB-11 | Missing | Corrected – PENDING Q-F3 | DBD A8/C1/E2/F6, PG §2.4/§2.18 | GST profile, client state code, place of supply |
| DB-12 | Contradictory | Corrected | DBD D5/F7 | Link stored only on `bill_lines` |
| DB-13 | Missing | Corrected – PENDING D-34 | DBD A11, DBR §10 | `owner_type`, `owner_id`, `is_financial` on files |
| DB-14 | Contradictory | Corrected | DBD E1/E2, DBR §7 | Revision status is the source; header derived |
| DB-15 | Partial | Corrected | DBD A10, DBR §2 | Real lookup FKs; new list types |
| DB-16 | Contradictory (public drafts) | Corrected – PENDING D-31 | DBD G1/G3, SEC §5, TR §2.2, DBR §10 | Private originals, public copies on publish, unpublish fields |
| DB-17 | Partial | Corrected | DBD G1, PG §2.15, WF Part D | Highlighted, display priority, content review status |
| DB-18 | Contradictory (FK cycle undocumented) | Corrected | DBD G1 | Cover set after images exist; documented |
| DB-19 | Partial | Corrected – PENDING Q-S5 | DBD B1/B2, PG §2.8, MOD §5 | `content_origin` incl. demo |
| DB-20 | Missing | Corrected | DBD §0, DBR §2/§3 | Audit columns are FKs to users |
| DB-21 | Contradictory | Corrected | DBD C2/D1/E2 | `area_unit_id` lookup FK everywhere |
| DB-22 | Missing | Corrected | DBD §4 | 12 integrity/calculation rules incl. XOR, write-offs, commission |
| DB-23 | Contradictory (49) | Corrected – PENDING D-22 | DBD §0/§2, S1R | 58 tables |

## 4. Workflows WF-01…WF-16

| ID | Found | Result | Affected files | Resolution |
|---|---|---|---|---|
| WF-01 | Contradictory | Corrected – PENDING D-26 | WF B.3, MOD §7, BR E-08, QA §5 | Per-project billing method; ad-hoc bills |
| WF-02 | Contradictory | Corrected – PENDING Q-F3/D-27 | WF A.4/A.5/B.2/B.7, DBR §8, DBD, PG §2.9–2.11, QA §5 | GST per document, off by default |
| WF-03 | Contradictory | Corrected – PENDING Q-U4 | WF A.4, PM 6/6a, MOD §6, BR Q-R12 | Send/accept/reject ADM only |
| WF-04 | Contradictory | Corrected | WF A.4/B.2 | Accept → convert → agreement, in one step |
| WF-05 | Contradictory | Corrected | WF B.4 | Precise bills-method outstanding |
| WF-06 | Missing | Corrected – PENDING Q-F10 | WF B.4 | Write-offs in all balances |
| WF-07 | Missing | Corrected | WF B.4/B.6 | One credit formula for both methods |
| WF-08 | Contradictory | Corrected | WF B.7, PG §2.11, DBD F9 | Credit-note limit fixed; excess → credit |
| WF-09 | Missing | Corrected | WF B.4, PG §2.12, MOD §8, BR E-09 | Partial payments always accepted |
| WF-10 | Partial | Corrected – PENDING Q-C3 | WF B.5/C.4, PM 8b | ADM-only reversal; commission never edited |
| WF-11 | Contradictory | Corrected – PENDING Q-F2 | WF A.6, PG §2.9/§2.10 | One schedule rule |
| WF-12 | Missing | Corrected – PENDING Q-C2 | WF A.2/C.2 | Conversion copies source/partner; Draft commission |
| WF-13 | Missing | Corrected – PENDING Q-C1…Q-C6 | WF Part C | Full commission lifecycle and tests |
| WF-14 | Missing | Corrected – PENDING Q-W1/Q-W11 | WF Part D, PWP §5, MOD §11 | Portfolio publish/unpublish/remove |
| WF-15 | Contradictory | Corrected – PENDING Q-U4 | WF B.9, PM 9, MOD §9, PG §1.12 | Expenses ADM only; claims optional |
| WF-16 | Missing | Corrected (tests not executed) | WF B.12/C.6, RM §2 | New financial, commission and leak test cases |

## 5. Permission matrix PM-01…PM-18

| ID | Found | Result | Affected files | Resolution |
|---|---|---|---|---|
| PM-01 | Contradictory (ADM/ACC) | Corrected | PM 1a, MOD §1, WFR W-E2 | Financial widgets ADM only |
| PM-02 | Contradictory | Corrected | PM 3a/4b, PG §1.4/§1.5 | Client/project finance ADM only |
| PM-03 | Contradictory | Corrected | PM 7/7a/7b, PG §1.10 | Agreements, bills, credit notes ADM only |
| PM-04 | Contradictory | Corrected | PM 8–8c, PG §1.11 | Payments, allocation, reversal, refunds ADM only |
| PM-05 | Contradictory | Corrected – PENDING Q-U4 | PM 6/6a/6b, PG §1.9/§2.9, MOD §6 | Quotation pricing and decisions ADM only |
| PM-06 | Contradictory | Corrected – PENDING Q-U4 | PM 9, PG §1.12, WF B.9 | Expenses ADM only |
| PM-07 | Contradictory | Corrected | PM 14b, PG §1.15, MOD §14 | Financial reports ADM only |
| PM-08 | Contradictory | Corrected | PM 16a, PG §1.16/§2.18 | Finance/GST settings ADM only |
| PM-09 | Contradictory | Corrected | PM 5/5a, PG §1.8/§1.17/§2.8 | Service rates ADM only |
| PM-10 | Contradictory | Corrected | PM 10/10a, MOD §10, DBD A10/D7 | Financial document categories ADM only |
| PM-11 | Contradictory | Corrected | PM 13/13a, DBD C5, MOD §13 | Financial follow-ups ADM only |
| PM-12 | Missing | Corrected – PENDING Q-C5 | PM 2c/18/18a, PG §1.14/§2.19 | Partner master rights |
| PM-13 | Missing | Corrected | PM 4c/19, PG §1.14 | Commission ADM only |
| PM-14 | Contradictory | Corrected – PENDING D-30/Q-U1 | PM §1, MOD header, DBD A1 | ACC removed from defaults |
| PM-15 | Partial ("STF pending") | Corrected – PENDING D-33 | PM §3, SEC §8.1, TR §3 | All non-ADM roles; every response path named |
| PM-16 | Missing | Corrected | PM §3, DBD C4, SEC §8.1, WFR W-E4 | Timeline entries without amounts |
| PM-17 | Partial | Corrected – PENDING Q-W11 | PM 11a | Publish ADM only by default |
| PM-18 | Implemented | Corrected | PM 17, DBR §9 | Audit log ADM only; exports audited |

## 6. ERP pages and fields PG-01…PG-15

| ID | Found | Result | Affected files | Resolution |
|---|---|---|---|---|
| PG-01 | Missing | Corrected | PG §1.14/§2.19–2.22 | Partner and commission pages and fields |
| PG-02 | Missing | Corrected – PENDING Q-C2/Q-C5 | PG §2.2/§2.5 | Source and partner fields |
| PG-03 | Contradictory | Corrected – PENDING Q-F3 | PG §1.16/§2.18 | Finance, GST and feature settings split; ADM only |
| PG-04 | Contradictory | Corrected | PG §2.9, WFR W-E6 | Apply GST per revision; ADM rates |
| PG-05 | Missing | Corrected | PG §2.10/§2.11/§2.5 | GST on agreement/variation/bill; billing method field |
| PG-06 | Partial | Corrected | PG §2.12, WFR W-E8 | Allocation grid by method; any amount |
| PG-07 | Contradictory | Corrected – PENDING Q-Q2/Q-Q10 | WFR W-E7, UI §1/§7, PG §2.18 | Logo + visiting-card letterhead; no commission printed |
| PG-08 | Missing | Corrected – PENDING Q-S5 | PG §1.8/§2.8 | Service delete routes, demo badge, content origin |
| PG-09 | Missing | Corrected | PG §1.13/§2.15, WFR W-E9 | Reorder, highlight, unpublish/remove reasons, consent file |
| PG-10 | Partial | Corrected – PENDING D-34 | PG §1.7, SEC §5, TR §2.2 | Owner-resolved file route; financial downloads audited |
| PG-11 | Missing | Corrected – PENDING Q-R1/Q-C5 | PG §1.15, MOD §14 | Source and commission reports |
| PG-12 | Missing | Corrected | PG §2.18, DBD A8 | Review status; phone 1/2; WhatsApp |
| PG-13 | Contradictory | Corrected | WFR W-E2/W-E4/W-E5/W-E11/W-E12 | ADM-only finance panels; commission screens |
| PG-14 | Missing | Corrected | PG §2.4, DBD C1 | Client state code; GSTIN ADM only |
| PG-15 | Partial | Corrected | PG §1.17, PM §3 | Financial AJAX endpoints marked ADM only |

## 7. Other audit items (INC, MR) from the consolidated report

| ID | Result | Affected files | Resolution |
|---|---|---|---|
| INC-01 | Corrected | All originals | Errata applied (§1–2 above) |
| INC-02, INC-03 | Done | Both review packages | SUPERSEDED banners; files kept |
| INC-04 | Corrected – PENDING D-25 | CLAUDE §3; all corrected docs | New tag scheme |
| INC-05 | Corrected | CLAUDE §2 | Document map lists all 24 documents |
| INC-06 | Corrected – PENDING Q-H1 | CLAUDE, OV, SC, TR, RM, CQ | Domain recorded; spelling check open |
| INC-07 | Corrected | RM §5 | Decision log: client decisions as reported; sync; open items marked "not yet decided" |
| INC-08 | Partly corrected – written confirmation PENDING | CQ §0, RM §5 | Decisions listed with date and source; client's written confirmation still to be filed |
| INC-09 | Corrected – PENDING Q-W3/Q-W4 | CLAUDE §4/§6, OV §3, UI §1 | Visiting card referenced; discrepancies recorded |
| INC-10 | Corrected | BR §7, SC §3, MOD summary | Commission in scope; construction-contractor payments out |
| INC-11 | Corrected – PENDING Q-W1 | SC §2.1, PWP, BR W-14 | CodInt drafts content for client review |
| INC-12 | Done | RM §4 | Working copy of `main` |
| INC-13 | Corrected | MOD §1, PM, WFR | No ACC finance access |
| INC-14 | Corrected | WF B.7, PG §2.11 | = WF-08 |
| INC-15 | Corrected | WF A.6, PG §2.9/§2.10 | = WF-11 |
| INC-16 | Corrected | DBR §2, DBD §0 | Real lookup FKs |
| INC-17 | Corrected | CQ | New questions added; statuses filled |
| INC-18 | Corrected – PENDING Q-Q2 | UI §1, WFR W-E7 | Logo + card letterhead |
| MR-01 | Corrected | see DB-01, WF-13, PM-13, PG-01 | Commission module |
| MR-02 | Corrected – PENDING Q-U4 | BR §4.1, SEC §8.1 | Financial-data definition |
| MR-03 | Corrected | BR Q-R02, MOD §6, PG §2.9 | Admin-only rates |
| MR-04 | Corrected – PENDING D-26 | BR E-08, WF B.3 | Flexible billing |
| MR-05 | Corrected – PENDING Q-F3 | BR E-25, DBR §8 | Optional GST per document |
| MR-06 | Corrected – PENDING Q-F2 | BR E-09, WF A.6/B.4 | Stages core; partial always allowed |
| MR-07 | Corrected – PENDING D-37 | BR W-14…W-16, UI §4, PWP, DBD A8/G1 | Review status; tone |
| MR-08 | Corrected | MOD §11, WF Part D, PWP §3 | Display sequence |
| MR-09 | Corrected – PENDING D-31 | SEC §5, TR §2.2, DBD G3 | Private originals |
| MR-10 | Corrected – PENDING Q-S5 | MOD §5, DBD B1/B2 | Demo services |
| MR-11 | Corrected – PENDING D-34 | SEC §5, PG §1.7, DBD A11 | File route by owner |
| MR-12 | Corrected – PENDING D-36 | DBR §12, TR §7 | Encrypted off-site backups; restore check |
| MR-13 | Corrected – PENDING Q-C6 | SEC §10 | Partner privacy |
| MR-14 | Corrected – PENDING Q-R1 | MOD §14, PG §1.15 | Reports |

## 8. Totals

| Group | Items | Corrected | Corrected – PENDING | Superseded | Done |
|---|---|---|---|---|---|
| C-01…C-18 | 18 | 7 | 9 | 1 (C-07) | 1 (C-12, policy pending) |
| R-01…R-08 | 8 | 4 | 4 | — | — |
| DB-01…DB-23 | 23 | 10 | 13 | — | — |
| WF-01…WF-16 | 16 | 6 | 10 | — | — |
| PM-01…PM-18 | 18 | 12 | 6 | — | — |
| PG-01…PG-15 | 15 | 9 | 6 | — | — |
| **Total (report scope)** | **98** | **48** | **48** | **1** | **1** |

No item is left uncorrected in the documents. "Corrected – PENDING" items cannot be finalised until the
named client question or developer decision is answered; their impact is stated in the documents and in
`docs/STAGE1_DOCUMENTATION_CONSISTENCY_REPORT.md` §4.

## 9. Addendum — client answers CD-27…CD-90 (2026-11-06)

The client answers recorded after this matrix was written changed the status of these items. All
changes were applied to the affected documents in the same session.

| Item | New status | Reason |
|---|---|---|
| R-01, C-06 (one merged enquiry module) | **Superseded** | Website enquiries kept as a separate inbox (CD-31; D-38) |
| R-02 (gallery switch) | **Superseded** | Gallery merged into each portfolio project; no Gallery page (CD-44) |
| C-02 ("Proposal" status) | **Superseded** | Statuses Planned / OnGoing / OnHold / Completed / HandOver / Cancelled (CD-76) |
| DB-07 (`credit_transfers`) | **Withdrawn** | No credit transfer between projects (CD-68); table removed |
| C-01, C-14, C-16, C-17 | Corrected — client rule now known | CD-89, CD-66, CD-65 (no reimbursement), CD-62 / CD-77 |
| DB-02, DB-10, DB-19, WF-06, WF-11, WF-12, WF-13 | Corrected — client rule now known | CD-71, CD-69, CD-42, CD-67, CD-59, CD-70…CD-75 (TDS still Q-C4) |
| PM-05, PM-06, PM-12, PM-14, PM-17, PG-02, PG-08 | Corrected — client rule now known | CD-83, CD-74, CD-80, ADM-only publishing, CD-71, CD-42 |
| DB-01, WF-02, DB-05, DB-09, DB-11, PG-03 | Corrected — GST stays designed but off | Studio not GST-registered today (CD-60) |
| C-13, MR-12 | Corrected — client rule now known | Plan 10 GB+ (CD-86); CodInt takes weekly off-site backup (CD-88) |

Still pending a client answer: **Q-H2** hosting provider (P1), Q-C4 TDS on commission, Q-S1/Q-S4 final
services, Q-W1 major projects, Q-W3 map pin and hours, Q-W7 Council of Architecture number, Q-Q8.
