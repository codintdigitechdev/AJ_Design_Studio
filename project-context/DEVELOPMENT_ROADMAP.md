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
