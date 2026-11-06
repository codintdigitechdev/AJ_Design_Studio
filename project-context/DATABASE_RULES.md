# Database Rules

These rules govern the future `database.sql` and `sample_data.sql`.
**No schema is created in Stage 0.** The schema design is a Stage 1 deliverable
that must be approved before implementation.

## 1. Engine and encoding
- MySQL 5.7+ / MariaDB 10.4+ (to be checked against the chosen host — Q-H2).
- `ENGINE=InnoDB`, `CHARSET utf8mb4`, `COLLATE utf8mb4_unicode_ci` (Marathi/Devanagari safe).
- Connection time zone `+05:30`; PHP `date_default_timezone_set('Asia/Kolkata')`.
- Store `DATETIME` values in IST consistently (single-region business).

## 2. Naming
- Tables: lowercase snake_case, plural (`clients`, `projects`, `quotation_items`).
- Primary key: `id INT UNSIGNED AUTO_INCREMENT` (BIGINT for audit/log tables).
- Foreign keys: `<singular>_id` (`client_id`), real `FOREIGN KEY` constraints, `ON DELETE RESTRICT`
  for business data.
- Booleans: `TINYINT(1)` named `is_*` / `has_*`.
- Statuses: `VARCHAR(30)` validated in PHP against constants (or lookup table), not ENUM, so
  new statuses don't need ALTER TABLE. Final choice in Stage 1.
- Indexes on every FK, status columns, date columns used in reports, and unique business numbers.

## 3. Standard columns
Every master and transaction table:
```
created_at  DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
created_by  INT UNSIGNED NULL
updated_at  DATETIME NULL ON UPDATE CURRENT_TIMESTAMP
updated_by  INT UNSIGNED NULL
```
Soft-deletable tables additionally:
```
deleted_at  DATETIME NULL
deleted_by  INT UNSIGNED NULL
```

## 4. Money, area and rates
- **DECIMAL only. Never FLOAT/DOUBLE.**
  - Money: `DECIMAL(14,2)`.
  - Rates: `DECIMAL(12,2)` (rate per sq.ft/sq.m or per item).
  - Area: `DECIMAL(12,2)` + `area_unit` (`sqft` / `sqm`).
  - Percentages: `DECIMAL(5,2)`.
  - Quantities: `DECIMAL(10,2)`.
- PHP arithmetic on money uses `bcmath` (or integer paise) — never float. Check `bcmath` availability on host (Q-H2).
- Rounding rule configurable (none / nearest rupee / nearest 10). Applied once, at total level, and stored.
- Totals are **stored** on the document (snapshot), and recomputable for verification.

## 5. Soft deletion
- Ordinary master records (clients, projects, services, users, portfolio items, masters)
  use `deleted_at`. Default queries filter `deleted_at IS NULL`.
- A record referenced by financial transactions cannot be soft-deleted without ADM override
  and audit entry; normally it is made **inactive** instead.
- Hard delete is only for: spam website enquiries (after retention), temp upload files.

## 6. Financial integrity
- Financial records: bills/invoices, payments/receipts, payment allocations, expenses,
  credit notes, reversals.
- **Never silently overwrite or delete** a posted financial record.
- Correction = reversal record (negative amount, `reverses_id` → original) + new correct record,
  with mandatory reason.
- Drafts may be edited; once **issued/posted** the row is immutable except status fields
  (enforced in PHP; optional DB triggers decided in Stage 1).
- Optional "lock date": nothing dated on/before it can be added or reversed without ADM.
- Document numbers (quotation, bill, receipt) are generated inside a transaction from a
  `number_sequences` table with `SELECT … FOR UPDATE`; unique index on the number;
  numbers are never reused, cancelled documents keep their number.

## 7. Quotation revisions
- `quotations` (header, current status, current revision no.) + `quotation_revisions`
  (frozen snapshot: dates, scope text, lines, area, rate, method, totals, terms) +
  `quotation_revision_items`.
- A sent revision is read-only. Editing creates revision n+1.
- Accepted revision ID is stored on the project fee agreement.

## 8. Audit log
- `audit_logs`: `id, user_id, action, module, record_type, record_id, summary,
  old_values JSON NULL, new_values JSON NULL, ip_address, user_agent, created_at`.
- Written by a single helper; append-only (no UPDATE/DELETE from the app).
- Login success/failure, password changes, role changes, financial postings/reversals,
  quotation status changes, portfolio publish/unpublish, document downloads (optional), backups.

## 9. Files
- DB stores metadata only: original name, stored (random) name, relative path, MIME,
  size, SHA-256 hash, uploader, linked record. File bytes stay on disk.
- Public portfolio images and private documents use different storage roots
  (see `SECURITY_RULES.md` §5).

## 10. Scripts
- `database.sql`: full schema + required seed (roles, permissions, default settings,
  number sequences, masters marked as reference). **No real client data.**
- `sample_data.sql`: fictitious demo data only — no real names from the sample
  quotation (e.g. not "Uttekar"), no real phone numbers.
- First admin user created by an install step or documented one-time procedure, with a
  forced password change; no well-known default password in production.
- Schema changes after first release: numbered migration files
  (`migrations/2027_01_15_001_add_x.sql`) and `database.sql` kept in sync.
- XAMPP version includes `CREATE DATABASE`; cPanel instructions explain importing
  into the pre-created database.

## 11. Backups
- Daily automated `mysqldump` via cPanel cron to a non-public folder, rotated (e.g. 7 daily, 4 weekly).
- Weekly off-site copy (method PENDING Q-H4).
- Restore procedure documented and **tested** before go-live.
