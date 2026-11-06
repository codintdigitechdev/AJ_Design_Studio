# Development Roadmap

Each stage ends with an **approval gate**. Do not start a stage before the previous gate is
approved and recorded in §5. The detailed Stage 1 plan and the register of every open decision
are in `docs/STAGE1_ROADMAP_AND_DECISIONS.md`; this file holds the stage table and the
**decision log**. Status tags: `CLAUDE.md` §3.

## 1. Stages (naming fixed by C-18)

| Stage | Name | Deliverables | Gate |
|---|---|---|---|
| **0** | Discovery & documentation | `CLAUDE.md`, `project-context/*`, first `docs/*` | Developer acceptance — **accepted 2026-11-06** |
| **1** | Architecture & database design | `DATABASE_DESIGN`, `WORKFLOWS`, `PERMISSION_MATRIX`, `ERP_PAGES_AND_FIELDS`, `WIREFRAMES`, decision register; corrected 2026-11-06 | Written approval of architecture + DB design — **approved 2026-11-06** |
| 2 | Foundation | Folder skeleton, config, bootstrap, DB helper, number-sequence service, money/calculation helper, financial-field registry, auth, roles/permissions from the approved matrix, CSRF, layouts, audit log, `database.sql` v1 (full approved schema), installer | Login + security checklist executed |
| 3 | Masters & settings | Settings (studio, letterhead, numbering, finance incl. GST profile, website content), lookups, services (demo flag, soft delete), users & roles, partner master | Module tests executed |
| 4 | Public website | Public pages in English and Marathi, enquiry form (built-in CAPTCHA) → Website Enquiries inbox, WhatsApp counter, SEO | Client design and content review on the staging copy (CD-87) |
| 5 | Portfolio CMS | Portfolio items, private originals + publish copies, highlight/priority, consent and review checks, unpublish/remove | Client uploads a real project |
| 6 | CRM | Enquiries (unreviewed queue, activities, partner, conversion), clients, follow-ups, dashboard v1 | Module tests executed |
| 7 | Projects & documents | Projects (source, billing method), team, documents via `/erp/files/{id}/download`, site visits ◇ | Module tests executed |
| 8 | Quotations | Builder, revisions (Superseded), per-revision GST, approval ◇, PDF, acceptance → conversion → fee agreement | Client approves PDF with a real example |
| 9 | Fees, payments, commission, expenses | Fee agreements/variations, stages, bills (per project method), credit notes, payments, allocation, credit, receipts, reversals, refunds (with % deduction), write-offs, **commission**, expenses, lock date | Financial and commission test cases (`WORKFLOWS.md` B.12, C.6) executed |
| 10 | Reports & dashboard v2 | Agreed report list incl. source and commission reports, audited exports | Client sign-off |
| 11 | Hardening & QA | Security review incl. financial-data leak tests, device tests, backup/restore drill, `sample_data.sql` | Test report |
| 12 | Deployment & handover | Hostinger hPanel, SSL for `ajdesignstudios.in` (CD-85), cron, training, guides, final ZIP | Client acceptance |

Website and ERP are delivered **together** (CD-37); there is no website-first phase.

## 2. Testing approach
- Manual test checklist per module in `docs/testing/` (created in Stage 2).
- Security: auth bypass, CSRF, SQLi, XSS, upload abuse, direct file URL access, **financial data
  leakage to non-ADM roles** (pages, APIs, exports, PDFs, timelines, digests).
- Financial and commission calculation cases (`WORKFLOWS.md` B.12, C.6).
- Results recorded with date and environment. **No test is reported as passed unless executed.**

## 3. Environment
- Dev: XAMPP on Windows (PHP and MySQL not on shell PATH; XAMPP path to confirm).
- Staging: password-protected copy for client review (CD-87).
- Production: Hostinger (hPanel), HTTPS, domain `ajdesignstudios.in` [CLIENT-DECISION CD-01, CD-85]; hosting plan 10 GB+ (CD-86, CD-91).

## 4. Version control
- GitHub `codintdigitechdev/AJ_Design_Studio`, branch `main`, is authoritative. The local folder
  was made a working copy of `main` on 2026-11-06 (commit `12d7634`) with the developer's
  permission (C-12).
- Commits and pushes only with the developer's explicit permission.
- `.gitignore` (Stage 2): `config/config.php`, `storage/*` (except `.gitkeep`),
  `public_html/uploads/*`, backups, ZIPs.

## 5. Decision log

Only decisions actually made are recorded here. Proposals and open questions live in
`docs/STAGE1_ROADMAP_AND_DECISIONS.md` and `docs/CLIENT_QUESTIONS.md`.

| Date | Decision | Decided by | Source / evidence | Reference |
|---|---|---|---|---|
| 2026-11-06 | Stage 0 documentation produced | CodInt Digitech | Files in repository | — |
| 2026-11-06 | Client decisions CD-01…CD-26 received (domain, content, services, portfolio, contacts, quotations, billing, GST, payments, Admin-only finance, contractor commission) | Ar. Ajit Kumbhar (as reported by CodInt Digitech) | Developer's audit brief of 2026-11-06. **Written client confirmation (date, channel) still to be filed** | `docs/CLIENT_QUESTIONS.md` §0 |
| 2026-11-06 | Local folder synchronised as a working copy of GitHub `main` | Developer (CodInt Digitech) | Session instruction "Yes, sync here" | C-12, D-24 |
| 2026-11-06 | Client decisions CD-27…CD-30: INR only; single office for now; Ar. Ajit Kumbhar is owner and main Admin user; operations mainly within Maharashtra (IST) | Ar. Ajit Kumbhar (as entered by the developer) | Developer's edit of `docs/STAGE1_ROADMAP_AND_DECISIONS.md` §4.3, commit `899ce73`. Written client confirmation still to be filed | `docs/CLIENT_QUESTIONS.md` §0; assumptions A2, A5, A8, A10 |
| 2026-11-06 | Client decisions CD-31…CD-90 (answers to the question list: website inbox, statuses, Marathi, letterhead, numbering, GST not registered, refunds, commission rules, users, hosting, etc.) | Ar. Ajit Kumbhar (as provided by the developer) | Developer's answers in `docs/CLIENT_QUESTIONS.md` and follow-up choices in the development session. Written client confirmation still to be filed | `docs/CLIENT_QUESTIONS.md` §0 |
| 2026-11-06 | Client decisions CD-91…CD-97 (Hostinger hPanel; TDS field off; no separate quotation approval step; final services = quotation categories; visits by appointment; map from the address; client marks major projects) | Ar. Ajit Kumbhar (as provided by the developer) | Development-session answers; written confirmation via `docs/CLIENT_DECISION_SUMMARY.md` pending | `docs/CLIENT_QUESTIONS.md` §0 |
| 2026-11-06 | **Stage 0 accepted** | Developer (CodInt Digitech) | Development-session answer "Yes, accept Stage 0" | D-03 |
| 2026-11-06 | Developer decisions D-02…D-41 approved as proposed in `docs/STAGE1_ROADMAP_AND_DECISIONS.md` §4.2 (superseded and withdrawn items excepted) | Developer (CodInt Digitech) | Development-session answer "Approve all defaults" | D-02…D-41 |
| 2026-11-06 | **Stage 1 architecture and database design approved — Stage 2 may start** | Developer (CodInt Digitech) | Development-session answer "Approve now"; client signature to be filed | Stage 1 gate |
| — | Client's signed decision summary filed | *pending* | — | `docs/CLIENT_DECISION_SUMMARY.md` |

## 6. Risks
| Risk | Mitigation |
|---|---|
| No AJ portfolio photos yet | Client sends originals (CD-43); launch with verified projects only |
| Non-AJ material in `reference/portfolio/` could be mistaken for AJ work | Client confirmed: sample only, not used (CD-39) |
| Logo only as JPEG | Client chose to use it as given (CD-51); careful crops |
| Commission TDS not yet in use | TDS field kept off (CD-92); switch on if the tax adviser requires |
| Studio may register for GST later | GST designed but off (CD-60); switched on when registered |
| Financial data leaking to non-ADM users | Central financial-field registry (D-33); leak tests in Stage 11 |
| Hostinger hPanel differs from cPanel (paths, cron, SSH by plan) | Verify folders outside `public_html`, SSH and cron on the purchased plan at the start of Stage 2 (A12) |
| Coding starts before the client signs the summary | Corrections from the signed summary are applied before the affected module is built |
| Marathi content and documents add effort | Translate from approved English; client review (CD-50) |
