# Database Rules

These rules govern the future `database.sql` and `sample_data.sql`. **No SQL is written
before the Stage 1 gate.** The table-by-table design is `docs/DATABASE_DESIGN.md` (PROPOSED).
Status tags: `CLAUDE.md` §3.

## 1. Engine and encoding
- MySQL 5.7+ / MariaDB 10.4+ (to be checked against the chosen host — Q-H2).
- `ENGINE=InnoDB`, `CHARSET utf8mb4`, `COLLATE utf8mb4_unicode_ci` (Marathi/Devanagari safe).
- Connection time zone `+05:30`; PHP `date_default_timezone_set('Asia/Kolkata')` [CLIENT-DECISION CD-30, N-05]. Currency INR only (CD-27) — no currency column is needed.

## 2. Naming and keys
- Tables: lowercase snake_case, plural. Primary key `id INT UNSIGNED AUTO_INCREMENT`
  (BIGINT for log tables).
- Foreign keys: `<singular>_id`, **real `FOREIGN KEY` constraints**, `ON DELETE RESTRICT` for
  business data. References to the generic `lookups` table are real FKs to `lookups.id`; the
  application also checks the lookup's `list_type` (INC-16).
- `created_by` / `updated_by` / `deleted_by` are FKs to `users.id` (NULL allowed for system and
  public rows).
- Booleans `TINYINT(1)` named `is_*` / `has_*`.
- Workflow statuses: `VARCHAR(30)` validated against fixed lists in the application; labels can be
  renamed in Settings, statuses cannot be added (D-07, R-08) [PROPOSED].
- Exactly-one-of rules (e.g. an allocation's target) are enforced in the application and covered
  by test cases; database CHECK constraints are added where the server version enforces them.
- Indexes on every FK, status column, report date column and unique business number.

## 3. Standard columns
Every master and transaction table:
```
created_at  DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
created_by  INT UNSIGNED NULL  (FK users)
updated_at  DATETIME NULL ON UPDATE CURRENT_TIMESTAMP
updated_by  INT UNSIGNED NULL  (FK users)
```
Soft-deletable tables additionally: `deleted_at DATETIME NULL`, `deleted_by INT UNSIGNED NULL`.

## 4. Money, area and rates
- **DECIMAL only. Never FLOAT/DOUBLE.** Money `DECIMAL(14,2)`; rates `DECIMAL(12,2)`;
  area `DECIMAL(12,2)` + area unit; percentages `DECIMAL(5,2)`; quantities `DECIMAL(10,2)`.
- PHP money arithmetic uses `bcmath` (or integer paise) — never float.
- Line amounts and each tax are rounded half-up to the paisa; the optional document rounding
  (none / ₹1 / ₹10) is applied once, at the end, as a separate stored line (D-10).
- Totals and every intermediate amount are **stored** on the document (snapshot) and can be
  recomputed for verification.
- Commission amounts follow the same rules (percentage × base, rounded to the paisa, stored).

## 5. Soft deletion
- Ordinary master records (clients, projects, services, users, partners, portfolio items, lookups)
  use `deleted_at`. Default queries filter `deleted_at IS NULL`.
- A record referenced by financial or commission rows is **deactivated**, not soft-deleted, unless
  ADM overrides with a reason (audited).
- Soft-deleted services stay visible on the quotations and portfolio items that already use them.
- Hard delete only for: spam website enquiries after the retention period (Q-G7), expired
  temporary files, rate-limit log rows.

## 6. Financial integrity (includes commission)
- Financial records: fee agreements and variations, payment stages once billed or paid, bills,
  credit notes, payments/receipts, allocations, credit transfers, refunds, write-offs, expenses,
  **project commissions after approval, commission adjustments, commission payments**.
- **Never silently overwrite or delete** a posted financial record.
- Correction = reversal record (negative amount, `reverses_id` → original, mandatory reason) and,
  where needed, a new correct record. Approved commission terms change only through adjustments.
- Drafts may be edited; once issued/posted/approved the row is immutable except status and
  cancellation fields (PHP enforcement; optional triggers D-15).
- Optional lock date: nothing dated on/before it can be added or reversed without ADM + reason.
- Document numbers (quotation, bill, credit note, receipt, refund, expense, commission payment,
  credit transfer) come from `number_sequences` inside the same transaction, using
  `SELECT … FOR UPDATE`; unique index; never reused; cancelled documents keep their number.
- **Allocation targets:** each allocation row targets exactly one of bill / payment stage / fee
  agreement (D-29). Allocated totals are always computed **net of allocation reversals**.
- **One active fee agreement per project** (not a plain unique index — a cancelled agreement must
  not block its replacement).

## 7. Quotation revisions
- `quotations` (header) + `quotation_revisions` (frozen snapshot) + per-revision child tables
  `quotation_scope_items`, `quotation_fee_lines`, `quotation_tax_lines`,
  `quotation_schedule_lines`. (The earlier name `quotation_revision_items` is replaced by the
  scope and fee-line tables.)
- A sent revision is read-only; editing creates revision n+1 and the previous one becomes
  Superseded. The revision status is the source of truth; any header status is derived.
- The accepted revision ID is stored on the fee agreement.

## 8. GST (optional, per document)
- Studio GST profile in settings (registered yes/no, GSTIN, state code, default SAC, default rates);
  **no GST fields are active until the studio is marked GST-registered** (Q-F3).
- Each taxable document (quotation revision, fee agreement, fee variation, bill, credit note)
  stores `gst_applicable`, `taxable_amount`, `tax_amount` and its own tax-line rows (name, rate,
  SAC, amount). GST is never compulsory [CLIENT-DECISION].
- Client `state_code` and the document's `place_of_supply` snapshot allow a CGST+SGST or IGST
  split; the actual rule is PENDING Q-F3.

## 9. Audit log
- `audit_logs`: `id, user_id, action, module, record_type, record_id, summary,
  old_values JSON NULL, new_values JSON NULL, ip_address, user_agent, created_at`.
- Append-only (no UPDATE/DELETE from the app). ADM-only viewing.
- Logged: login success/failure, password and role changes, every financial and commission
  action (post, approve, adjust, reverse, cancel), quotation status changes, portfolio
  publish/unpublish/remove, financial exports, financial document downloads, backups,
  partner bank-detail changes.

## 10. Files
- DB stores metadata only: storage area (public/private), relative path, random stored name,
  original name, MIME, size, SHA-256, **owner type + owner ID**, **is_financial**, uploader.
- Portfolio originals are private; public web versions are created on publish and withdrawn on
  unpublish/remove (D-31). Private documents never sit in the web root.

## 11. Scripts
- `database.sql`: full schema + required seed (roles ADM/STF/SITE, permissions, default settings,
  number sequences, lookups, reference/demo services flagged by `content_origin`). **No real
  client data.**
- `sample_data.sql`: fictitious demo data only — no names from the sample quotation, no real phone
  numbers, nothing from `reference/portfolio/Senior office profile.pdf`.
- First admin created by an install step with forced password change; no well-known default password.
- Schema changes after first release: numbered migrations; `database.sql` kept in sync.

## 12. Backups
- Daily `mysqldump` via cPanel cron to a non-public folder; weekly archive of private files and
  public uploads.
- Retention **7 daily / 4 weekly / 3 monthly**, subject to the host's disk quota (C-13; PENDING Q-H2, Q-H4).
- Off-site copies are **encrypted** (password-protected archive; key held by ADM off-server — D-36).
- Restore procedure documented and **tested** before go-live, including a check that every `files`
  row has its file and every stored file has a row.
