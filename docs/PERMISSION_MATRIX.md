# Role × Module Permission Matrix

**Status: PROPOSED — Stage 1 not approved.** Corrected 2026-11-06 (PM-01…PM-18).
Rule implemented: **financial information and financial decisions are Admin-only**
[CLIENT-DECISION] — definition in `project-context/BUSINESS_REQUIREMENTS.md` §4.1,
enforcement in `project-context/SECURITY_RULES.md` §8.1. Tags: `CLAUDE.md` §3.

The ADM can edit non-financial permissions per role in **Users & Roles → Role permissions**.
Permissions flagged financial (`permissions.is_financial`) can be granted to another role only by a
recorded future client decision; by default they are ADM-only.

## 1. Roles (PROPOSED — D-30; only ADM in use now — CLIENT-DECISION CD-80)

| Code | Role | Intended user |
|---|---|---|
| ADM | Admin / Principal | Ar. Ajit Kumbhar. At least one active ADM; the role cannot be deleted. **Only role with financial access** |
| STF | Office staff | Enquiries, clients, projects, documents, portfolio editing, follow-ups — **no financial data** |
| SITE | Site engineer / designer | Assigned projects only: site visits, non-financial documents |
| ~~ACC~~ | ~~Accounts~~ | **Removed from the defaults** (PM-14): every finance right it had is ADM-only by client decision |

## 2. Matrix

Codes: **V** view · **C** create · **E** edit · **D** delete (soft/deactivate) · **S** change status ·
**A** approve · **R** reverse/cancel posted financial record · **X** export · **—** no access.
**[FIN]** = financial row: ADM only, always.

| # | Module / function | ADM | STF | SITE |
|---|---|---|---|---|
| 1 | Dashboard – operational widgets (counts, no amounts) | V | V | V (own projects/follow-ups) |
| 1a | [FIN] Dashboard – financial and commission widgets | V | — | — |
| 2 | Enquiries (manual) | V C E D S X | V C E S X | — |
| 2d | Website Enquiries inbox – review, spam, convert (CD-31) | V S | V S | — |
| 2a | Date-range delete of Lost/Closed enquiries and inbox items (CD-34) | D | — | — |
| 2b | Enquiry: convert to client + project | S | S | — |
| 2c | Enquiry/project: select contractor/referral partner | V E | — (CD-74) | — |
| 3 | Clients – profile (no GSTIN, no balances) | V C E D X | V C E | V (clients of own projects; contact only) |
| 3a | [FIN] Client – GSTIN, financial summary, balance, credit | V E | — | — |
| 4 | Projects – details, status, team | V C E D S X | V C E S X | V (assigned) |
| 4a | Project – site-visit log (CD-77) | V C E D | V C E | V C E (assigned; edit own within 48 h — PENDING) |
| 4b | [FIN] Project – billing method, fees, bills, payments, expenses tabs | V C E | — | — |
| 4c | [FIN] Project – source & commission tab (incl. "commission applicable") | V C E S A | — | — |
| 4d | Project – source type (Direct/Contractor/Referral) | V E | — (CD-74) | — |
| 5 | Services & categories – names, descriptions, website flags, order | V C E D | V | V |
| 5a | [FIN] Service default rates | V E | — | — |
| 6 | [FIN] Quotations – create, price, edit draft, PDF, export | V C E D X | — (CD-83) | — |
| 6a | [FIN] Quotation – send / accept / reject / expire / cancel | S | — | — |
| 6b | [FIN] Quotation – approval step ◇, discount approval | A | — | — |
| 7 | [FIN] Fee agreement, variations, payment stages | V C E | — | — |
| 7a | [FIN] Bills – draft, issue, PDF | V C E D S | — | — |
| 7b | [FIN] Bills – cancel; credit notes | R | — | — |
| 8 | [FIN] Payments & receipts – record, print | V C X | — | — |
| 8a | [FIN] Allocation / apply credit (no credit transfer — CD-68) | E | — | — |
| 8b | [FIN] Payment reversal | R | — | — |
| 8c | [FIN] Refund (with % deduction), write-off (CD-66, CD-67) | C R | — | — |
| 9 | [FIN] Expenses – entry, reversal | V C R X | — (CD-83) | — |
| 10 | Project documents – non-financial categories | V C E D | V C E | V C (assigned) |
| 10a | [FIN] Documents in financial categories; expense and commission proofs | V C E D | — | — |
| 11 | Portfolio & gallery – edit, images, review status | V C E D | V C E | — |
| 11a | Portfolio – publish / unpublish / remove | S D | — | — |
| 12 | Website content blocks – edit / mark reviewed | V E S | V E | — |
| 13 | Follow-ups – non-financial | V C E D (all) | V C E (own + unassigned) | V C E (own) |
| 13a | [FIN] Follow-ups linked to bills, payments or commission | V C E D | — | — |
| 14 | Reports – operational, counts only (enquiries, quotation counts, project status) | V X | V X | — |
| 14a | Reports – enquiries/projects by source (counts) | V X | — (CD-74) | — |
| 14b | [FIN] Reports – values, outstanding, collections, expenses, profitability, commission | V X | — | — |
| 15 | Users & roles | V C E D | — | — |
| 16 | Settings – studio, letterhead, numbering, security, lookups | V E | — | — |
| 16a | [FIN] Settings – finance, GST profile, lock date, feature switches | V E | — | — |
| 16b | Backup download | S | — | — |
| 17 | Audit log (contains financial values) | V X | — | — |
| 18 | Partner master – name, firm, contacts | V C E D X | — (CD-74) | — |
| 18a | [FIN] Partner bank/tax details, default commission suggestion | V E | — | — |
| 19 | [FIN] Commission – terms, approval, adjustments, payments, reversals, vouchers, register | V C E S A R X | — | — |
| — | Own profile, own password | V E | V E | V E |

## 3. Record-level and response rules

| Rule | Applies to |
|---|---|
| SITE sees a project only if listed in `project_members` — in dashboards, lists, search, documents, site visits and downloads | SITE |
| "Own" = `created_by` or `assigned_to` = current user | STF, SITE follow-ups |
| **Financial data is removed from every server response** for non-ADM roles — pages, list columns, search results, AJAX/API (`/erp/api/*`), CSV exports, PDFs, email digests and notifications, activity timelines, follow-up notes, error messages (PM-15; central registry D-33) | **All non-ADM roles, no exceptions** |
| System-generated activity entries contain no amounts; financial events are recorded in the audit log only (PM-16) | All |
| Financial routes return 403 for non-ADM | All non-ADM |
| A posted financial or approved commission record is never edited — reversal, cancellation or adjustment only | All, incl. ADM |
| No user can change their own role, deactivate themselves, or remove the last ADM | All |
| Every S, A, R, D action, every export and every financial document download is audited (PM-18) | All |

## 4. Client decisions applied to this matrix

Q-U1 → CD-80 (only ADM uses the ERP for now; STF/SITE prepared for later) · Q-U4 → CD-83 (no staff
scope drafting, sending or expense claims) · Q-C5 → CD-74 (staff see no partner or source data) ·
Q-W11 → ADM only publishes · Q-U2 → CD-81 (mobile use allowed — SITE screens responsive) ·
Q-U3 → CD-82 (no two-step login) · Q-G4 → CD-31 (separate website inbox, row 2d).

Still open: Q-Q8 separate approval step (not needed while only the ADM uses the ERP).
