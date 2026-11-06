# Security Rules

Mandatory for all code. A feature is not "done" until these are satisfied.

## 1. Separation of public site and ERP
- One codebase, one database, **two entry areas**: public (`/`) and ERP (`/erp/`).
- Public code may read **only published portfolio/content data** and may **insert** website
  enquiries. It never includes ERP controllers or queries ERP tables.
- Every ERP request passes through a single bootstrap that enforces: session valid →
  user active → permission for this module/action. No ERP page is reachable without it.
- ERP pages send `X-Robots-Tag: noindex, nofollow`; `/erp/` is disallowed in `robots.txt`
  (defence in depth only — not a security control).
- Optional (PROPOSED): two DB users — `ajds_public` (SELECT on published content, INSERT on
  enquiries) and `ajds_erp` (full DML). Decide in Stage 1 based on host limits.

## 2. Files outside the web root
- `config/` (DB credentials, secrets), `app/` (PHP classes/includes), `storage/`
  (private documents, logs, backups, temp) live **above** `public_html`.
- If a host forbids this, fallback: same folders inside the web root with `Require all denied`
  `.htaccess` + an index guard — documented as the weaker option.
- Never commit real credentials; `config/config.sample.php` in repo, real `config.php` excluded.
- `display_errors=Off` in production; errors logged to `storage/logs/`.
- Block web access to `*.sql, *.md, *.log, *.ini, *.bak, *.zip, .env, .git` and directory listing.

## 3. Authentication
- `password_hash()` (PASSWORD_DEFAULT) / `password_verify()`; rehash when needed.
- Minimum password policy: 10+ chars (PROPOSED), not equal to username.
- Lockout / throttling: e.g. 5 failures → 15-minute lock per account + per-IP throttling.
- Generic error message ("Invalid username or password").
- `session_regenerate_id(true)` on login and privilege change.
- Password reset: random 32-byte token, store **hash** of token, 30–60 min expiry, single use.
- No default credentials in production; no `fix_login.php`-style reset scripts deployed.
- Optional 2FA (TOTP) for Admin — PENDING Q-U3.

## 4. Sessions and cookies
- ERP session name e.g. `AJDS_ERP`, cookie path `/erp`, `HttpOnly`, `Secure` (HTTPS),
  `SameSite=Lax` (Strict if no cross-site links needed), `session.use_strict_mode=1`.
- Idle timeout (e.g. 30 min, configurable) and absolute timeout (e.g. 10 h).
- Public site uses no login session; if a session is needed (CSRF on enquiry form) it uses
  a different cookie name scoped to `/`.
- Logout via POST with CSRF; destroy session and cookie.

## 5. Uploads
| | Public portfolio images | Private project documents |
|---|---|---|
| Storage | `public_html/uploads/portfolio/` (web-served) | `storage/documents/` (outside web root) |
| Delivery | Direct URL | `erp/download.php?id=` after permission check, `Content-Disposition: attachment` |
| Allowed | JPG, PNG, WebP | PDF, JPG, PNG, WebP, DWG? DOCX? XLSX? (Q-D1) |
- Validate extension whitelist **and** MIME via `finfo`, and for images `getimagesize()`.
- Re-encode images with GD/Imagick (removes payloads and EXIF/GPS).
- Random stored file names (`bin2hex(random_bytes(16))`); original name kept only in DB.
- Size limits configurable; check `upload_max_filesize`/`post_max_size` on host.
- Upload dirs: `.htaccess` disabling PHP/script execution (`RemoveHandler`, `php_flag engine off`
  where supported, `Require all denied` for `*.php*`), no directory listing.
- Never use user input in file paths; resolve and verify paths stay inside the storage root.

## 6. Requests and output
- **CSRF** token (per session, `hash_equals`) on every POST/PUT/DELETE incl. AJAX and the public enquiry form.
- State changes only via POST.
- **Server-side validation** of every field (type, length, range, allowed values); client-side is convenience only.
- **PDO prepared statements** only; `ATTR_EMULATE_PREPARES=false`; whitelist column names for sorting.
- **Output escaping**: `htmlspecialchars(…, ENT_QUOTES, 'UTF-8')` by default; rich text from
  ERP (About page etc.) sanitized with an allow-list.
- AJAX endpoints return JSON, check auth + permission + CSRF, never leak stack traces.

## 7. HTTP headers (both areas)
`Strict-Transport-Security` (after HTTPS confirmed), `X-Content-Type-Options: nosniff`,
`X-Frame-Options: SAMEORIGIN` / CSP `frame-ancestors 'self'`, `Referrer-Policy: strict-origin-when-cross-origin`,
a Content-Security-Policy appropriate to each area, `Permissions-Policy`. Force HTTPS redirect.

## 8. Authorization
- Permission checks server-side on every action (not just hiding menu items).
- Record-level checks where needed (e.g. SITE role sees only assigned projects — PENDING).
- Financial reversals, user/role changes, settings, backups: ADM only (default).

## 9. Public form abuse
- Honeypot field, minimum fill time, per-IP rate limit, length limits, strip links count.
- No CAPTCHA by default (PROPOSED); add only if spam becomes a problem (Q-W6).
- Notification emails: never use visitor input in headers.

## 10. Privacy
- Website enquiries contain personal data: store only what is needed, ERP access only,
  retention period PENDING (Q-G7). Privacy notice link near the form.
- Portfolio publishes only with client consent; location shown at city/area level, not
  full address; no client names unless approved.
- India's DPDP Act 2023 considerations to be reviewed with the client — not legal advice.

## 11. Audit, logging, backup
- Audit log per `DATABASE_RULES.md` §8.
- Application error log in `storage/logs/`, rotated; never displayed to users.
- Backups stored outside web root; DB backup downloads ADM-only and audited.

## 12. Dependencies
- Minimal: Bootstrap 5, (optional) a PDF library such as Dompdf or mPDF bundled with the
  release (decision in Stage 1 — Q-T1). Pin versions; record them in the docs.
- No CDN for ERP assets (PROPOSED) — bundle locally; public site may use local copies too.
