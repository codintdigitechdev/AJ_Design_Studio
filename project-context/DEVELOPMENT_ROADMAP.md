# Development Roadmap

Each stage ends with an **approval gate**. Do not start a stage before the previous gate is
approved and recorded in §5. The detailed Stage 1 plan and the register of every open decision
are in `docs/STAGE1_ROADMAP_AND_DECISIONS.md`; this file holds the stage table and the
**decision log**. Status tags: `CLAUDE.md` §3.

## 1. Stages (naming fixed by C-18)

| Stage | Name | Deliverables | Gate |
|---|---|---|---|
| **0** | Discovery & documentation | `CLAUDE.md`, `project-context/*`, first `docs/*` | Developer acceptance — **not yet recorded (D-03)** |
| **1** | Architecture & database design | `DATABASE_DESIGN`, `WORKFLOWS`, `PERMISSION_MATRIX`, `ERP_PAGES_AND_FIELDS`, `WIREFRAMES`, decision register; corrected 2026-11-06 | Written approval of architecture + DB design — **not approved** |
| 2 | Foundation | Folder skeleton, config, bootstrap, DB helper, number-sequence service, money/calculation helper, financial-field registry, auth, roles/permissions from the approved matrix, CSRF, layouts, audit log, `database.sql` v1 (full approved schema), installer | Login + security checklist executed |
| 3 | Masters & settings | Settings (studio, letterhead, numbering, finance incl. GST profile, website content), lookups, services (demo flag, soft delete), users & roles, partner master | Module tests executed |
| 4 | Public website | Public pages, enquiry form → enquiry module, WhatsApp counter, SEO | Client design and content review on staging (Q-H3) |
| 5 | Portfolio CMS | Portfolio items, private originals + publish copies, highlight/priority, consent and review checks, unpublish/remove | Client uploads a real project |
| 6 | CRM | Enquiries (unreviewed queue, activities, partner, conversion), clients, follow-ups, dashboard v1 | Module tests executed |
| 7 | Projects & documents | Projects (source, billing method), team, documents via `/erp/files/{id}/download`, site visits ◇ | Module tests executed |
| 8 | Quotations | Builder, revisions (Superseded), per-revision GST, approval ◇, PDF, acceptance → conversion → fee agreement | Client approves PDF with a real example |
| 9 | Fees, payments, commission, expenses | Fee agreements/variations, stages, bills (per project method), credit notes, payments, allocation, credit, receipts, reversals, refunds ◇, write-offs ◇, **commission**, expenses, lock date | Financial and commission test cases (`WORKFLOWS.md` B.12, C.6) executed |
| 10 | Reports & dashboard v2 | Agreed report list incl. source and commission reports, audited exports | Client sign-off |
| 11 | Hardening & QA | Security review incl. financial-data leak tests, device tests, backup/restore drill, `sample_data.sql` | Test report |
| 12 | Deployment & handover | cPanel, SSL for `ajdesignstudios.in` (spelling confirmed — Q-H1), cron, training, guides, final ZIP | Client acceptance |

Website-first phasing (Stages 2→3→4→5 + enquiry part of 6) is PENDING Q-G9.

## 2. Testing approach
- Manual test checklist per module in `docs/testing/` (created in Stage 2).
- Security: auth bypass, CSRF, SQLi, XSS, upload abuse, direct file URL access, **financial data
  leakage to non-ADM roles** (pages, APIs, exports, PDFs, timelines, digests).
- Financial and commission calculation cases (`WORKFLOWS.md` B.12, C.6).
- Results recorded with date and environment. **No test is reported as passed unless executed.**

## 3. Environment
- Dev: XAMPP on Windows (PHP and MySQL not on shell PATH; XAMPP path to confirm).
- Staging: optional password-protected copy (Q-H3).
- Production: cPanel, HTTPS, domain `ajdesignstudios.in` [CLIENT-DECISION; spelling PENDING Q-H1].

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
| — | Stage 0 accepted | *not yet decided* | — | D-03 |
| — | Stage 1 architecture and database design approved | *not yet decided* | — | Stage 1 gate |

## 6. Risks
| Risk | Mitigation |
|---|---|
| No AJ portfolio photos yet; Instagram posts not readable without login | Q-W1; launch with fewer, verified projects |
| Non-AJ material in `reference/portfolio/` could be mistaken for AJ work | Marked "not AJ content" everywhere; Q-G11 |
| Logo only as JPEG | Q-B1; careful crops meanwhile |
| Commission rules undecided (direction, base, timing, tax) | Module designed with those fields PENDING (Q-C1…Q-C6); no assumptions coded |
| GST status unknown | GST dormant until Q-F3; never compulsory |
| Financial data leaking to non-ADM users | Central financial-field registry (D-33); leak tests in Stage 11 |
| Shared hosting limits | Verify in Stage 1/2 (Q-H2) |
| Domain spelling (`ajdesignstudios` vs brand "Studio") | Confirm before DNS/SSL (Q-H1) |
