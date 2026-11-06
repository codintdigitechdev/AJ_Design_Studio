# Role × Module Permission Matrix

**Status: PROPOSED — PENDING APPROVAL (Q-U1, Q-U2, Q-Q8, Q-F4).**

This matrix is a starting default. The client has not said who will use the ERP or what each
person may see. It is built so that the Admin can change each role's permissions in
**Users & Roles → Role permissions** without any code change.

## 1. Roles (proposed)

| Code | Role | Intended user (to confirm with Q-U1) |
|---|---|---|
| ADM | Admin / Principal | Ar. Ajit Kumbhar; at least one active ADM at all times; the ADM role cannot be deleted |
| STF | Office staff | Front office / junior architect handling enquiries, clients, projects and quotations |
| ACC | Accounts | Fee billing, payments, receipts, expenses |
| SITE | Site engineer / designer | Assigned projects only: site visits, documents |

## 2. Matrix

**Permission codes:**

| Code | Meaning |
|---|---|
| **V** | view |
| **C** | create |
| **E** | edit |
| **D** | delete — soft delete or deactivate only (`DATABASE_RULES.md` §5) |
| **S** | change status (send, convert, close, publish, etc.) |
| **A** | approve |
| **R** | reverse or cancel a posted financial record |
| **X** | export (CSV/PDF) |
| **—** | no access |

| # | Module / function | ADM | STF | ACC | SITE |
|---|---|---|---|---|---|
| 1 | Dashboard – operational widgets | V | V | V | V (own projects/follow-ups only) |
| 1a | Dashboard – financial widgets | V | — | V | — |
| 2 | Enquiries (including website submissions) | V C E D S X | V C E S X | V | — |
| 2a | Enquiry: mark spam / delete spam | V D | V D | — | — |
| 2b | Enquiry: convert to client + project | S | S | — | — |
| 3 | Clients – profile | V C E D X | V C E | V | V (clients of own projects; contact details only) |
| 3a | Client – financial summary (balance, credit) | V | — | V | — |
| 4 | Projects – details, status, team | V C E D S X | V C E S X | V | V (assigned only) |
| 4a | Project – site-visit log | V C E D | V C E | V | V C E (assigned only; edit own entries within 48 h — PENDING APPROVAL) |
| 4b | Project – fee & payment tabs | V | — (PENDING Q-U1) | V | — |
| 5 | Services & work categories | V C E D | V | V | V |
| 6 | Quotations – create, edit draft | V C E D X | V C E X | V | — |
| 6a | Quotation – send / mark accepted, rejected, expired | S | S (if approval is off) | — | — |
| 6b | Quotation – approve before sending (optional workflow) | A | — | — | — |
| 6c | Quotation – discount above the threshold | A | — | — | — |
| 7 | Fee agreement & milestones | V C E | V | V C E | — |
| 7a | Bills – draft | V C E D | — | V C E D | — |
| 7b | Bills – issue | S | — | S | — |
| 7c | Bills – cancel / credit note | R | — | R (PENDING: maybe ADM only) | — |
| 8 | Payments & receipts – record | V C X | — (PENDING Q-U1) | V C X | — |
| 8a | Payment – allocate / apply credit | E | — | E | — |
| 8b | Payment – reversal (bounced, wrong entry) | R | — | — (requests it; ADM performs it) | — |
| 8c | Refund | C R | — | C (PENDING) | — |
| 8d | Receipt – print / re-print | V | — | V | — |
| 9 | Expenses – own entry | V C E D X | V C (own) | V C E X | V C (own, assigned projects) |
| 9a | Expense – edit or reverse after posting | R | — | R | — |
| 10 | Project documents – view / download | V | V | V (agreement / financial categories) | V (assigned projects) |
| 10a | Project documents – upload / new version | C E | C E | C | C (assigned) |
| 10b | Project documents – delete | D | — | — | — |
| 11 | Portfolio & gallery – edit | V C E D | V C E | — | — |
| 11a | Portfolio – publish / unpublish | S | — (PENDING) | — | — |
| 13 | Follow-ups | V C E D (all) | V C E (own + unassigned) | V C E (payment follow-ups) | V C E (own) |
| 14 | Reports – operational (enquiry, quotation, project status) | V X | V X | V X | — |
| 14a | Reports – financial (billed/received, outstanding, collections, expenses, profitability) | V X | — | V X | — |
| 15 | Users & roles | V C E D | — | — | — |
| 16 | Organization settings, masters, numbering, tax | V E | — | V (tax/numbering read-only) | — |
| 16a | Website content settings | V E | V E | — | — |
| 16b | Backup download | S | — | — | — |
| 16c | Lock date | E | — | — | — |
| 17 | Audit log | V X | — | — | — |
| — | Own profile, change own password | V E | V E | V E | V E |

## 3. Record-level rules (proposed)

| Rule | Applies to |
|---|---|
| SITE sees a project only if they are on that project's team (`project_members`). This filter applies to dashboards, lists, search, document downloads and site visits | SITE |
| "Own" means `created_by` = the current user, or `assigned_to` = the current user | STF, SITE follow-ups and expenses |
| Financial fields (fees, rates, totals, balances) are **removed from the server response** for roles without financial view, not just hidden on screen. This includes quotation totals in lists | STF (pending), SITE |
| A posted financial record can never be edited; it can only be reversed or cancelled | All roles, including ADM |
| No user can change their own role, deactivate themselves, or remove the last ADM | All |
| Every S, A, R and D action, and every export of financial data, is recorded in the audit log | All |

## 4. Open questions that change this matrix — PENDING APPROVAL

1. **Q-U1** – Who actually uses the ERP? Can STF see fees and payments (rows 4b, 8)?
   Should there be a separate junior-architect role?
2. **Q-Q8** – Is there an approval step before a quotation is sent (row 6b)? Who can send?
3. **Q-F4** – Do discounts need approval, and what is the threshold (row 6c)?
4. Can ACC perform reversals, cancellations and refunds, or only ADM (rows 7c, 8b, 8c)?
5. Can STF publish portfolio items (row 11a)?
6. **Q-U2** – Will SITE use the ERP on a phone? This affects the mobile screens for rows 4a and 10a.
