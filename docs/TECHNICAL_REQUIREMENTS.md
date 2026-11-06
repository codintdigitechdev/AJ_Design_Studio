# Technical Requirements

Status: **[PROPOSED]** for approval in Stage 1. No code is written in Stage 0.

## 1. Stack
| Layer | Choice |
|---|---|
| Language | Core PHP 8.1+ (8.2/8.3 preferred), no framework |
| Database | MySQL 5.7+/8.0 or MariaDB 10.4+, InnoDB, utf8mb4 |
| DB access | PDO, prepared statements, `ERRMODE_EXCEPTION`, no emulated prepares |
| Front end | Bootstrap 5 (bundled locally), HTML5, CSS3 (custom properties), vanilla JS, `fetch()` AJAX |
| PDF | Dompdf or mPDF bundled in `vendor/` (decision Q-T1; mPDF if Devanagari text like "श्री" is needed) |
| Images | GD (or Imagick if available) for resize/re-encode/WebP |
| Math | `bcmath` for money (fallback: integer paise) |
| PHP extensions required | pdo_mysql, mbstring, fileinfo, gd, bcmath, openssl, json, intl (optional) |
| Dev | XAMPP (Windows) |
| Prod | cPanel shared hosting, Apache, HTTPS (AutoSSL/Let's Encrypt), cron |

Composer is used only to fetch the PDF library during development; the release ZIP ships
`vendor/` so cPanel needs no Composer.

## 2. Same hosting account: how the website and ERP coexist

### 2.1 Principle
One hosting account, one domain, **one codebase and one database**, with two front
doors. Only small entry scripts and public assets sit inside the web root; everything
sensitive sits beside it, unreachable by URL.

### 2.2 Production layout on cPanel (recommended)
```
/home/<cpaneluser>/
├── ajds_app/                      ← NOT web-accessible
│   ├── config/
│   │   └── config.php             DB credentials, secrets, paths, env = production
│   ├── app/
│   │   ├── core/                  bootstrap, DB, Router, Auth, Csrf, Validator, Audit, Upload, Money
│   │   ├── public/                public-site controllers + views
│   │   ├── erp/                   ERP module controllers + views (one folder per module)
│   │   └── shared/                helpers, layouts, PDF templates
│   ├── storage/
│   │   ├── documents/             private project documents
│   │   ├── logs/
│   │   ├── backups/               cron mysqldump output
│   │   ├── cache/  tmp/
│   ├── vendor/                    PDF library
│   └── database/                  database.sql, migrations/ (reference copy)
│
└── public_html/                   ← web root (https://<domain>/)
    ├── index.php                  public front controller → requires ../ajds_app/app/core/bootstrap.php
    ├── .htaccess                  HTTPS, pretty URLs, security headers, deny sensitive extensions
    ├── assets/                    css, js, fonts, images, logo variants, favicon
    ├── uploads/portfolio/         PUBLIC processed images only (.htaccess: no script execution)
    ├── robots.txt   (sitemap.xml generated dynamically)
    └── erp/
        ├── index.php              ERP front controller → same bootstrap, ERP mode
        └── .htaccess              rewrite /erp/login, /erp/dashboard … to index.php; noindex header
```
- `/erp/login` and `/erp/dashboard` are clean URLs rewritten to `erp/index.php`.
- Both front controllers locate the app via a single path constant (`APP_ROOT`) — the only
  line to change if the host layout differs.
- Private documents are streamed by `erp/index.php?route=documents/download&id=…` after
  authentication and permission checks — never by direct URL.
- If the domain is an **addon domain** with its own document root (e.g. `/home/user/domain.com/`),
  `ajds_app/` still sits in `/home/user/`, outside that root.

### 2.3 Fallback if the host forbids files above the web root
`public_html/ajds_app/` with `Require all denied` in its `.htaccess`, plus a startup check that
refuses to run if `config/` is web-reachable. Documented as weaker; avoid if possible.

### 2.4 XAMPP development layout
```
C:\xampp\htdocs\ajds\              (= public_html)  → http://localhost/ajds/ and /ajds/erp/login
C:\xampp\ajds_app\                 (= ajds_app, outside htdocs)
```
A `BASE_URL` setting supports running in a sub-folder locally and at domain root in production.

### 2.5 Shared vs separate
| Concern | Shared | Separate |
|---|---|---|
| Database | One DB | Optional separate DB users for public (limited) vs ERP (full) |
| Config | One `config.php` | Area-specific settings (session name, CSP) in bootstrap |
| Code | Core libs, models, settings, layouts partials | Public controllers/views vs ERP controllers/views |
| Sessions | — | ERP cookie `AJDS_ERP`, path `/erp`; public has no login session |
| Assets | Bootstrap, fonts, logo | `assets/public/*` vs `assets/erp/*` |
| Uploads | — | Public portfolio in web root; private docs in `storage/` |
| Errors/logs | One log dir | Tagged by area |

## 3. Request flow
```
Browser → Apache (.htaccess: HTTPS, rewrite, headers)
        → public_html/index.php or public_html/erp/index.php
        → ajds_app/app/core/bootstrap.php (config, error handling, session per area, DB)
        → Router → [ERP: Auth + Permission + CSRF middleware] → Controller → Model (PDO) → View
        → Response (HTML / JSON for AJAX / PDF / file stream)
```

## 4. Coding conventions
- PSR-12 style, `declare(strict_types=1)`, simple PSR-4-like autoloader (no framework).
- One folder per ERP module: controller, model/repository, views, validation rules.
- All SQL in model/repository classes; no SQL in views.
- Escape output by default (`e()` helper); CSRF field helper in forms.
- Money via a `Money` helper (bcmath, Indian formatting, amount in words).
- Constants for statuses; settings read from DB `settings` table with cache.
- No secrets, real client data or generated uploads in Git.

## 5. Email
- PHP `mail()` via host or SMTP (domain mailbox, Q-H5) through a small mailer class;
  used for password reset, enquiry notification, optional reminder digest.

## 6. Cron jobs (cPanel)
| Job | Frequency |
|---|---|
| DB backup (`mysqldump` → `storage/backups/`, gzip, rotate) | Daily |
| Files backup of `storage/documents` + `uploads/` (tar.gz, rotate) | Weekly |
| Reminder digest email (if approved) | Daily morning |
| Cleanup temp files, expired reset tokens, old spam enquiries | Daily |

## 7. Backup and restore strategy
- **What:** database; `storage/documents/`; `public_html/uploads/`; `config/config.php` (kept securely, not in normal backups shared by email).
- **Where:** `storage/backups/` (outside web root) + weekly off-site copy (Q-H4) + cPanel's own backups if the plan has them.
- **Retention (proposed):** 7 daily, 4 weekly, 3 monthly.
- **Restore:** documented steps for (a) full restore to new hosting, (b) DB-only restore via phpMyAdmin/`mysql`, (c) single-file document recovery. Restore drill performed before go-live.
- ERP Settings → "Download backup" for ADM (audited).

## 8. Deployment (outline; full guide in Stage 12)
1. Create MySQL DB + user(s) in cPanel; import `database.sql`.
2. Upload `ajds_app/` to home directory and `public_html/` contents to web root.
3. Copy `config.sample.php` → `config.php`; set DB, base URL, mail, environment.
4. Set folder permissions (755 dirs / 644 files; `storage` and `uploads` writable by PHP).
5. Run first-admin setup; force password change; remove/lock installer.
6. Enable AutoSSL, force HTTPS; set cron jobs; verify security headers and that
   `/ajds_app/…`, `.sql`, `config` are not reachable.
7. Smoke test public site, enquiry form, ERP login, upload, PDF.

## 9. Host capability checklist (to verify in Stage 1 — Q-H2)
PHP ≥ 8.1 selectable · required extensions · MySQL/MariaDB version · ability to place
folders outside `public_html` · `upload_max_filesize`/`post_max_size` · `memory_limit` (PDF) ·
cron · AutoSSL · disk quota for documents and backups · outgoing mail limits.
