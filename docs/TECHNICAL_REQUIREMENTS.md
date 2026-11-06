# Technical Requirements

Status: **PROPOSED** — Stage 1 not approved. Corrected 2026-11-06 (C-11, C-13, MR-09, MR-11, MR-12).
Tags: `CLAUDE.md` §3. No code is written before approval.

## 1. Stack
| Layer | Choice |
|---|---|
| Language | Core PHP 8.1+ (8.2/8.3 preferred), no framework [BRIEF] |
| Database | MySQL 5.7+/8.0 or MariaDB 10.4+, InnoDB, utf8mb4 |
| DB access | PDO, prepared statements, `ERRMODE_EXCEPTION`, no emulated prepares |
| Front end | Bootstrap 5 (bundled locally), HTML5, CSS3, vanilla JS, `fetch()` AJAX |
| PDF | Dompdf or mPDF bundled in `vendor/` (D-18; mPDF if "श्री"/Devanagari is kept — Q-Q2) |
| Images | GD (or Imagick) for resize/re-encode/WebP |
| Math | `bcmath` for money and commission (fallback: integer paise) |
| PHP extensions | pdo_mysql, mbstring, fileinfo, gd, bcmath, openssl, json, intl (optional) |
| Dev / Prod | XAMPP (Windows) / cPanel shared hosting, Apache, HTTPS, cron [BRIEF] |

Composer only in development; the release ZIP ships `vendor/`.

## 2. Same hosting account: how the website and ERP coexist

### 2.1 Principle
One hosting account, domain `ajdesignstudios.in` [CLIENT-DECISION CD-01/CD-02; spelling Q-H1],
**one codebase and one database**, two front doors. Only small entry scripts, public assets and
**published** portfolio images sit in the web root.

### 2.2 Production layout on cPanel (recommended)
```
/home/<cpaneluser>/
├── ajds_app/                      ← NOT web-accessible
│   ├── config/config.php          DB credentials, secrets, paths, env
│   ├── app/
│   │   ├── core/                  bootstrap, DB, Router, Auth, Csrf, Validator, Audit, Upload,
│   │   │                          Money, NumberSequence, FinancialFieldRegistry (D-33)
│   │   ├── public/                public-site controllers + views
│   │   ├── erp/                   one folder per ERP module (incl. partners, commission)
│   │   └── shared/                helpers, layouts, PDF templates
│   ├── storage/
│   │   ├── documents/             private files (documents, site-visit photos, expense and commission proofs)
│   │   ├── portfolio/             portfolio ORIGINALS and drafts (private — D-31)
│   │   ├── logs/  backups/  cache/  tmp/
│   ├── vendor/
│   └── database/                  database.sql, migrations/
│
└── public_html/                   ← web root (https://ajdesignstudios.in/)
    ├── index.php                  public front controller
    ├── .htaccess                  HTTPS, pretty URLs, headers, deny sensitive extensions
    ├── assets/                    css, js, fonts, logo variants, favicon
    ├── uploads/portfolio/         web versions of PUBLISHED items only (created on publish,
    │                              deleted on unpublish/remove; no script execution)
    ├── robots.txt
    └── erp/
        ├── index.php              ERP front controller
        └── .htaccess              rewrites /erp/login, /erp/dashboard …; noindex header
```
- Private files are streamed only by **`/erp/files/{id}/download`** (C-11, D-34), which resolves the
  file's owner record and applies its permission (incl. Admin-only for financial files). There is no
  separate `download.php`.
- If the domain is an addon domain with its own document root, `ajds_app/` still sits outside it.

### 2.3 Fallback if the host forbids files above the web root
`public_html/ajds_app/` with `Require all denied` + a startup check that refuses to run if `config/`
is web-reachable. Weaker; avoid if possible.

### 2.4 XAMPP development layout
`C:\xampp\htdocs\ajds\` (= public_html) and `C:\xampp\ajds_app\` (outside htdocs); `BASE_URL`
supports a sub-folder locally and domain root in production.

### 2.5 Shared vs separate
| Concern | Shared | Separate |
|---|---|---|
| Database | One DB | Optional DB users: public (limited) vs ERP (full) — D-04 |
| Config | One `config.php` | Area-specific session name and CSP |
| Code | Core libs, models, settings | Public vs ERP controllers/views |
| Sessions | — | ERP cookie `AJDS_ERP`, path `/erp`; public has no login session |
| Uploads | — | Published portfolio copies in web root; everything else in `storage/` |
| Logs | One log dir | Tagged by area |

## 3. Request flow
```
Browser → Apache (.htaccess) → public_html/index.php | public_html/erp/index.php
  → bootstrap (config, errors, session per area, DB)
  → Router → [ERP: Auth → Permission → Record-level rule → CSRF] → Controller → Model (PDO)
  → FinancialFieldRegistry filter for non-ADM (pages, JSON, CSV, PDF, digests, timelines)
  → Response (HTML / JSON / PDF / file stream)
```

## 4. Coding conventions
PSR-12, `declare(strict_types=1)`, simple autoloader, one folder per ERP module, SQL only in
models, `e()` escaping, CSRF helper, Money helper (bcmath, Indian format, amount in words),
status constants, settings cache. No secrets, real client data or uploads in Git.

## 5. Email
`mail()` or SMTP via a domain mailbox (Q-H5) for password reset, enquiry notification and optional
digests. Non-ADM digests never contain amounts.

## 6. Cron jobs (cPanel)
| Job | Frequency |
|---|---|
| DB backup (`mysqldump` → `storage/backups/`, gzip, rotate) | Daily |
| Files backup (`storage/documents`, `storage/portfolio`, `public_html/uploads`) | Weekly |
| Encrypted off-site copy (D-36; destination Q-H4) | Weekly |
| Reminder digest (if approved, Q-G5) | Daily |
| Cleanup: temp files, expired reset tokens, rate-limit log, old spam enquiries, orphaned public portfolio copies | Daily |

## 7. Backup and restore strategy
- **What:** database; `storage/documents/`; `storage/portfolio/`; `public_html/uploads/`;
  `config/config.php` (kept separately and securely).
- **Where:** `storage/backups/` (outside web root) + weekly **encrypted** off-site copy (password-
  protected archive; key held by ADM off-server — D-36) + host backups if available.
- **Retention:** 7 daily / 4 weekly / 3 monthly, subject to disk quota (C-13; Q-H2, Q-H4).
- **Restore:** documented full restore, DB-only restore, single-file recovery; a consistency check that
  every `files` row has its file and vice versa; restore drill before go-live and per release.
- ERP Settings → "Download backup" for ADM (audited). Backups contain financial, commission and
  partner data — handle as confidential.

## 8. Deployment (outline; full guide in Stage 12)
1. Confirm the domain spelling (Q-H1); point DNS; enable AutoSSL.
2. Create the MySQL DB + user(s); import `database.sql`.
3. Upload `ajds_app/` to the home directory and `public_html/` contents to the web root.
4. `config.sample.php` → `config.php`; set DB, base URL, mail, environment.
5. Permissions: 755 dirs / 644 files; `storage` and `public_html/uploads` writable by PHP.
6. First-admin setup with forced password change; lock the installer.
7. Force HTTPS; cron jobs; verify headers and that `ajds_app`, `.sql`, `config` and `storage` are unreachable.
8. Smoke test: public site, enquiry form, ERP login, upload, publish/unpublish, PDF, a non-ADM login
   showing no financial data.

## 9. Host capability checklist (Q-H2)
PHP ≥ 8.1 · required extensions · MySQL/MariaDB version · folders outside `public_html` ·
`upload_max_filesize`/`post_max_size` · `memory_limit` (PDF) · cron · AutoSSL · disk quota for
documents, portfolio originals and backups · outgoing mail limits.
