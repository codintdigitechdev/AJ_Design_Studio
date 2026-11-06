# Security Rules

Mandatory for all code. A feature is not "done" until these are satisfied.
Status tags: `CLAUDE.md` §3. Rules here are BRIEF/PROPOSED unless marked.

## 1. Separation of public site and ERP
- One codebase, one database, **two entry areas**: public (`/`) and ERP (`/erp/`).
- Public code may read **only published portfolio/content data** and may **insert** website
  enquiries. It never includes ERP controllers or queries financial or commission tables.
- Every ERP request passes through one bootstrap: session valid → user active → permission for
  this module/action → record-level rule. No ERP page is reachable without it.
- ERP pages send `X-Robots-Tag: noindex, nofollow`; `/erp/` is disallowed in `robots.txt`
  (defence in depth only).
- Optional (D-04): two DB users — `ajds_public` (SELECT on published content, INSERT on enquiries
  and rate-limit log) and `ajds_erp` (full DML).

## 2. Files outside the web root
- `config/`, `app/`, `storage/` (private documents, portfolio originals, logs, backups, temp) live
  **above** `public_html`. Fallback inside the web root with `Require all denied` is weaker and
  used only if the host forbids the above.
- Never commit real credentials; `config/config.sample.php` in Git, real `config.php` ignored.
- `display_errors=Off` in production; errors logged to `storage/logs/`.
- Block web access to `*.sql, *.md, *.log, *.ini, *.bak, *.zip, .env, .git` and directory listing.

## 3. Authentication
- `password_hash()` (PASSWORD_DEFAULT) / `password_verify()`; rehash when needed.
- Password policy: 10+ chars, not equal to username (D-16, PROPOSED).
- Lockout: 5 failures → 15-minute lock per account, plus per-IP throttling.
- Generic error message. `session_regenerate_id(true)` on login and privilege change.
- Password reset: random 32-byte token, stored as a hash, 30–60 min expiry, single use.
- No default credentials in production; no `fix_login.php`-style scripts deployed.
- Optional 2FA (TOTP) for Admin — PENDING Q-U3.

## 4. Sessions and cookies
- ERP cookie `AJDS_ERP`, path `/erp`, `HttpOnly`, `Secure`, `SameSite=Lax` (D-17),
  `session.use_strict_mode=1`. Idle timeout 30 min, absolute 10 h (configurable).
- Public site has no login session; any CSRF session for the enquiry form uses a different
  cookie name.
- Logout via POST with CSRF.

## 5. Uploads and private files
| | Portfolio images | Private files (documents, site-visit photos, expense and commission proofs) |
|---|---|---|
| Upload storage | Originals and drafts: `storage/portfolio/` (private) | `storage/documents/` (private) |
| Public copies | Resized web versions copied to `public_html/uploads/portfolio/` **only when the item is published**; removed on unpublish/remove (D-31) | Never |
| Delivery | Direct URL of published web versions | **One route: `/erp/files/{id}/download`** (C-11, D-34) — resolves the owning record, applies its permission (incl. SITE assignment and Admin-only for financial owners/categories), sends `Content-Disposition: attachment`; financial downloads are always audited |
| Allowed | JPG, PNG, WebP | PDF, JPG, PNG, WebP; DWG/DOCX/XLSX etc. PENDING Q-D1 |
- Validate extension whitelist **and** MIME via `finfo`; images also via `getimagesize()`.
- Re-encode images (removes payloads and EXIF/GPS). Random stored names. Size limits configurable.
- Upload dirs: no PHP/script execution, no directory listing.
- Never build file paths from user input; resolve and verify paths stay inside the storage root.

## 6. Requests and output
- **CSRF** token on every POST incl. AJAX and the public enquiry form. State changes only via POST.
- **Server-side validation** of every field.
- **PDO prepared statements** only; `ATTR_EMULATE_PREPARES=false`; whitelisted sort columns.
- **Output escaping** by default; rich text sanitized with an allow-list.
- AJAX endpoints return JSON, check auth + permission + CSRF, never leak stack traces.

## 7. HTTP headers (both areas)
HSTS (after HTTPS confirmed), `X-Content-Type-Options: nosniff`, `frame-ancestors 'self'`,
`Referrer-Policy: strict-origin-when-cross-origin`, a CSP per area, `Permissions-Policy`.
Force HTTPS.

## 8. Authorization
- Permission checks server-side on every action (not just hiding menus).
- Record-level: SITE sees only projects where they are a team member — in lists, search,
  dashboards, documents, site visits and downloads.
- No user can change their own role, deactivate themselves, or remove the last ADM.

### 8.1 Financial data is Admin-only [CLIENT-DECISION]
Definition: `BUSINESS_REQUIREMENTS.md` §4.1. Enforcement [PROPOSED, D-33]:
- One central **financial-field registry** lists every financial column, document type, report,
  widget and file category. Every view, list, search, API/AJAX response, CSV export, PDF renderer,
  email/notification and timeline builder consults it and **omits** financial data for non-ADM
  users — the data is never sent, not merely hidden.
- Financial routes (fees, bills, credit notes, payments, receipts, allocations, refunds,
  write-offs, credit transfers, expenses, commission, partner bank/tax data, financial reports,
  finance settings, financial AJAX endpoints) return **403** for non-ADM users.
- System-generated activity-timeline entries never contain amounts; financial events are written
  to the audit log (ADM only).
- Follow-ups linked to bills, payments or commission are ADM-only.
- Non-ADM email digests and notifications contain no amounts.
- Error messages never reveal financial values.

## 9. Public form abuse
- Honeypot, minimum fill time, per-IP rate limit, length and link-count limits.
- No CAPTCHA by default (Q-W6). Visitor input never goes into email headers.

## 10. Privacy
- Website enquiries: minimal data, ERP access only, retention PENDING Q-G7, privacy notice by the form.
- Portfolio: publish only with consent recorded; city-level location; no client names unless
  approved [CLIENT-DECISION: no private client information without approval].
- Contractor/referral partner data: minimal contact data; bank and tax details optional,
  Admin-only, encrypted at rest where stored, masked in lists; retention PENDING Q-C6.
- Content from `reference/portfolio/Senior office profile.pdf` (another architect) is never published.
- India's DPDP Act 2023 to be reviewed with the client — not legal advice.

## 11. Audit, logging, backup
- Audit log per `DATABASE_RULES.md` §9 (append-only, ADM-only).
- Error logs in `storage/logs/`, rotated, never displayed.
- Backups outside the web root; off-site copies encrypted (D-36); DB backup downloads ADM-only and audited.

## 12. Dependencies
- Minimal: Bootstrap 5 and a PDF library (Dompdf or mPDF — D-18), versions pinned and bundled.
- ERP assets served locally, not from a CDN [PROPOSED].
