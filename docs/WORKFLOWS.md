# Business Workflows — Enquiry → Project → Quotation, and Financial Workflow

**Status: PROPOSED — PENDING APPROVAL (Q-G2, Q-Q*, Q-F*).**

This document fixes inconsistencies C-01 to C-08 and C-14 to C-17 from
`docs/STAGE1_GAP_RESOLUTION.md`.

All amounts in the examples are **invented, for illustration only**. They are not defaults,
and they are not the sample quotation's values (`CLAUDE.md` §7).

---

# PART A — Enquiry → Project → Quotation

## A.1 Overview

```
               ┌───────────────── Website form (status: New – unreviewed)
               │  ┌────────────── Manual: phone / WhatsApp / walk-in / referral / Instagram / other
               ▼  ▼
          ┌──────────┐  spam/duplicate  ┌──────────┐
          │ ENQUIRY  │ ───────────────► │  Closed  │
          └────┬─────┘                  └──────────┘
   activities: │ calls, meetings, pre-project site visit (C-03); follow-ups
               │
       ┌───────┴───────────────────────────────┐
       │ Path 1: quote the prospect            │ Path 2: convert first
       ▼                                       ▼
 QUOTATION (linked to enquiry)          CONVERT → CLIENT + PROJECT (status Proposal)
       │ Sent → Accepted                       │
       ▼                                       ▼
 CONVERT → CLIENT + PROJECT  ◄─────── QUOTATION (linked to project)
       │ (quotation re-linked to project)      │ Sent → Accepted
       └───────────────┬───────────────────────┘
                       ▼
          FEE AGREEMENT created from accepted revision  → Part B
                       ▼
          PROJECT status: Design → … → Completed
                       ▼
          (optional, with consent) PORTFOLIO item
```

- **Which path is the default:** PENDING APPROVAL (Q-G2).
- **Both paths are supported.** Path 1 matches the sample, which was quoted at enquiry stage
  and dated before any project existed. Path 2 suits repeat clients.

## A.2 Enquiry lifecycle

| Status | Entered when | Allowed next | Required data |
|---|---|---|---|
| New – unreviewed | Website form submitted | New, Closed (spam/duplicate) | Name, mobile, consent |
| New | Created by hand, or reviewed from the website | Contacted, Closed | Name, mobile, source |
| Contacted | First contact made | Meeting / site visit, Quotation sent, Lost, Closed | Activity note |
| Meeting / site visit | Meeting or visit held or scheduled | Quotation sent, Lost | Activity with a date |
| Quotation sent | Its quotation reaches status Sent | Converted, Lost | Linked quotation |
| Converted | Turned into a client + project | — (final) | Client ID, project ID |
| Lost | Prospect declined | New (re-open, ADM/STF) | Lost reason (from a list + free text) |
| Closed | Spam, duplicate, not relevant | — | Close reason |

**Rules:**
- **Duplicate check:** the same mobile number or email as an open enquiry or an existing
  client shows a warning and offers to link them (`MODULES.md` §2).
- **Converting:**
  - copies name, contact, location, project type, area and services into a new or existing
    client and a new project;
  - stores the enquiry's link to the project (`enquiry.project_id`);
  - moves the enquiry's quotations to the project, keeping their link to the enquiry;
  - copies all of this; nothing is moved or deleted.
- **Status changes:** each one is logged as an activity and in the audit log.
- **Keeping old enquiries:** Lost or Closed enquiries are kept for a period that is PENDING
  APPROVAL (Q-G7). Spam is deleted permanently after that period (`DATABASE_RULES.md` §5).

## A.3 Project lifecycle (C-02 applied)

| Status | Meaning |
|---|---|
| Proposal | Project opened before any quotation was accepted (Path 2) |
| Design | Quotation accepted / work started |
| Working drawings | |
| Approval / Municipal | |
| Under construction (supervision) | |
| Interiors | |
| Completed | |
| On hold | Can return to its previous status |
| Cancelled | Final. Needs a reason. Open bills or credit must be settled first (B.8) |

- **The status list itself** is PENDING APPROVAL (Q-P1). Statuses can be re-labelled in
  Settings; the ones in this order are **not** a strict sequence — any forward or backward
  change is allowed, except back to Proposal.
- **Status history** is kept: date, user, remark.

## A.4 Quotation lifecycle (C-04 applied)

**Header:** quotation number (from the number sequence, e.g. `{seq}/{yyyy}` — format PENDING
APPROVAL, Q-Q1), linked enquiry or project, current revision number, current status.

**Revisions:** R0, R1, R2 … Each revision holds:
- the date and validity
- area, area basis and unit
- the text: subject, intro, scope sections and items
- the fee lines and the calculation method
- optional blocks: discount, tax, schedule, terms
- all totals

```
 R0 Draft ──edit freely──► R0 Draft
     │ Send (S; or Approve A → Send, if the approval step is on — Q-Q8)
     ▼
 R0 Sent ──client asks for changes──► "Create revision" → R1 Draft (copy of R0); R0 becomes Superseded
     │                                                       │ Send
     ├─► Accepted  ─► fee agreement created (Part B)          ▼
     ├─► Rejected (reason)                                   R1 Sent → …
     ├─► Expired (automatic when validity ends, if validity is used; or by hand)
     └─► Cancelled (reason)
```

**Rules:**
- A Sent, Accepted, Rejected, Expired or Superseded revision can never be edited.
- Only one revision can be Accepted. Accepting one locks the whole quotation.
- Re-opening an Accepted quotation is **not allowed**. A change in scope after acceptance is
  handled by a **fee agreement variation** (B.2).
- "Send" is a status change only. Emailing from the ERP is optional (Q-Q9); by default the
  user downloads the PDF and shares it.
- The PDF of each sent revision is generated from that revision's frozen data, so it can be
  re-printed exactly.
- Quotation number: the number is taken when R0 is created (proposed), so a draft has a
  number too. Alternative: take the number on first send. PENDING APPROVAL (D-09).
- Area-based fees use the area basis written on the revision (built-up, carpet, plot or total
  of all floors; Q-Q3). There are no hardcoded defaults.

## A.5 Calculation order for a quotation revision or bill — PROPOSED, PENDING APPROVAL (D-10)

The project files do not specify the order in which discount, tax and rounding are applied.
Proposed order:

1. **Line amounts:**
   - area line = area × rate
   - item line = quantity × rate
   - fixed line or custom line = the amount entered

   Each result is exact to the paisa (2 decimal places, rounded half-up).
2. **Subtotal** = sum of all line amounts.
3. **Discount** (if enabled): an amount, or a percentage of the subtotal rounded to the paisa.
   It cannot exceed the subtotal.
4. **Taxable value** = subtotal − discount.
5. **Tax** (if enabled): one line per tax (e.g. CGST and SGST, or IGST — PENDING Q-F3).
   Each tax = taxable value × rate, rounded to the paisa.
6. **Total before rounding** = taxable value + taxes.
7. **Rounding** (if enabled: none / nearest ₹1 / nearest ₹10): shown as a separate
   "Rounding" line, so the result can be checked.
8. **Grand total** is stored, together with every intermediate amount.
9. **Amount in words** uses the Indian system (lakh/crore) — on/off is PENDING (Q-Q6).

**Example** (invented numbers): area 1,250 sq.ft × ₹90 = ₹1,12,500.00. Item line:
4 views × ₹2,500 = ₹10,000.00. Subtotal ₹1,22,500.00. Discount off. Tax off.
Rounding none. Grand total ₹1,22,500.00.

## A.6 Payment schedule on the quotation (optional, Q-F2)

- **Lines:** stage name, then either a % of the grand total or a fixed amount, then the
  trigger ("on acceptance", "on plans", or free text).
- **Rule:** the lines must add up to exactly 100% or to the grand total. Any difference left
  by rounding is put on the last line.

---

# PART B — Financial workflow

## B.1 Building blocks

| Document | Purpose | Can be edited? | Corrected by |
|---|---|---|---|
| **Fee agreement** | The agreed fee for a project, taken from the accepted revision | Never directly | Variation (B.2) |
| **Fee milestone** | The expected amount per stage (if a schedule is used) | Until it is billed or due | Variation |
| **Bill** (demand note / tax invoice — name PENDING Q-F3) | A request for payment | While Draft | Cancel + re-issue, or credit note (B.7) |
| **Credit note** | Reduces an issued bill | Never once issued | Its own cancellation (ADM) |
| **Payment (receipt)** | Money received from a client | Never once posted | Reversal (B.5) |
| **Allocation** | Applies part of a payment, or client credit, to a bill or milestone | Never once posted | Allocation reversal (de-allocate) |
| **Refund** | Money paid back to a client from their credit | Never once posted | Reversal |
| **Expense** | Money spent by the studio | Never once posted | Reversal (B.9) |

**Common rules for every financial record** (`DATABASE_RULES.md` §6):
- Each record has a unique number taken from a number sequence.
- Nothing is ever deleted permanently.
- Every reversal points back to the original record and needs a reason.
- The lock date applies (D-08).
- Every change is recorded in the audit log.

## B.2 Fee agreement

- **Created automatically** when a quotation revision is Accepted:
  - agreed amount = that revision's grand total
  - the tax portion is stored separately, if tax is used
  - the milestones are copied from the revision's payment schedule, if one exists
- **Without a quotation:** a fee agreement can also be created by hand (ADM / ACC), with a
  mandatory reason.
- **Variation** (a change in scope or a negotiated change):
  - recorded as a separate +/− amount with a reason and date, and optionally a link to a new
    quotation;
  - the original agreement row is never overwritten;
  - the **current agreed fee** = original + all variations.
- **One project** can have exactly one active fee agreement (PROPOSED).

## B.3 Billing modes (C-07) — PENDING APPROVAL (Q-F1)

| | Mode A — Bills | Mode B — Agreement only |
|---|---|---|
| Payment request | A bill is issued (from a milestone, or by hand) | No bill. A follow-up or reminder is used if needed |
| A payment is applied to | Bills (and optionally milestones) | The fee agreement |
| Outstanding = | Issued bills − allocated payments − credit notes | Current agreed fee − net payments received |
| Receipt | Always | Always |
| Tax | Possible on bills (Q-F3) | Not supported. Mode B assumes no tax invoicing |

The mode is a studio-wide setting, chosen once before go-live. Changing it later needs ADM and
is allowed only when no bills exist (PROPOSED).

## B.4 Payments, advances and allocation

```
 Payment received (date, client, project, amount, mode, reference)
        │ posted → receipt number
        ▼
 ┌─────────────────────────────────────────────┐
 │ Allocation screen (Mode A)                  │
 │  open bills of this project/client listed   │
 │  user allocates ≤ payment amount            │
 │  unallocated remainder → CLIENT CREDIT      │
 └─────────────────────────────────────────────┘
```

**Advances**
- An advance is a payment received **before** any bill, or a payment larger than the open
  bills.
- In Mode A it stays **unallocated** and appears as **credit** on the project (and so on the
  client).
- In Mode B every payment simply reduces the agreement's outstanding amount. An advance is
  just an early payment.
- The receipt says "Advance against <project>" when nothing was allocated.

**Applying credit later (C-15)**
- When a bill is issued and the project has credit, the bill screen offers "Apply available
  credit".
- Doing so creates allocation rows from the earlier payment to the new bill. The payment
  itself is not changed.

**Allocation rules**
- Total allocated from one payment ≤ that payment's amount.
- Total allocated to one bill ≤ that bill's amount still open (after credit notes).
- **Allocation is per project.** Moving credit from one project to another of the same client
  is a transfer of credit: ADM only, with a reason, as two linked allocation rows. PENDING
  APPROVAL (D-11).
- **Bill status is calculated:** Issued → Partly paid → Paid. It is never set by hand.
- **Overpayment:** whatever is left after allocation stays as credit.

**Formulas**

| Term | Calculation |
|---|---|
| Net received (project) | Payments − payment reversals |
| Credit (project) | Net received − active allocations − net refunds |
| Outstanding, Mode A (project) | Issued bills − cancelled bills − credit notes − active allocations |
| Outstanding, Mode B (project) | Current agreed fee − net received + net refunds |
| Client figure | Sum of the client's projects |

## B.5 Payment reversal (bounced cheque, wrong entry)

1. ADM (or another role, if approved) chooses **Reverse** on a posted payment and gives a
   reason (from a list + free text) and the reversal date.
2. The system creates a reversal payment record:
   - amount = −original amount
   - linked to the original (`reverses_id`)
   - its own number taken from the payment sequence (PENDING: or a separate "RV"
     sequence, D-12)
3. All active allocations of the original payment are reversed automatically. The bills they
   paid go back to Partly paid or Issued.
4. The original receipt is marked **REVERSED**. When re-printed it shows a watermark.
5. **Wrong amount:** reverse the payment, then post a new correct payment. There is no
   in-place edit.
6. **Bounced cheque charges** are not assumed. If the client wants them, they would be a
   custom bill line (Q-F5).

## B.6 Refunds (C-14) — PENDING APPROVAL (Q-F9)

- **When:** only from available project credit (overpayment, advance on a cancelled project,
  or after a credit note).
- **Fields:** date, project, client, amount ≤ available credit, mode, reference, reason,
  approved by (ADM).
- **Number:** its own refund number sequence.
- **Effect:** credit goes down. Shown in the collections report as money paid out.
- **Correcting a refund:** a refund reversal (amount −, `reverses_id`).

## B.7 Bills: issuing, cancelling, credit notes (Mode A)

- **Draft bill:** the lines come from milestones, fixed or custom lines, and (if enabled)
  chargeable visits or reimbursable expenses (C-16, C-17). The calculation order follows A.5.
- **Issue:** the number is taken, the bill is frozen, and the PDF is available.
- **Cancel:** allowed only if nothing is allocated to the bill. The bill keeps its number and
  shows as CANCELLED. A corrected bill is issued with a new number.
- **Credit note:** used when a bill already has payments allocated, or to reduce part of it.
  It references the bill, has its own number, and reduces what is open on the bill. If the
  bill had been fully paid, the excess becomes credit.
- **Tax on credit notes** follows the original bill's tax lines (Q-F3).

## B.8 Project cancellation, and closing financially

- Before a project can be set to Cancelled or Completed (financially closed), the system
  shows outstanding and credit.
- **Credit left:** choose a refund, a transfer to another project (ADM), or "retain" with a
  reason. The legal and commercial rules are the client's decision (Q-Q7 cancellation terms).
- **Outstanding left:** choose write-off (ADM, reason; recorded as a write-off adjustment row
  linked to the bill or agreement) or keep it open. Write-off is PENDING APPROVAL (D-13).

## B.9 Expenses

- **Fields:** date, category, project (optional — left blank means office overhead), paid to,
  amount, mode, attachment, reimbursable flag (optional).
- **Posted on save** (PROPOSED). Correcting one means a reversal + a new entry.
  Alternative: allow editing until the lock date — PENDING APPROVAL (D-14).
- **Reimbursable** to the client: becomes a bill line only in Mode A, and only with Q-F5 and
  Q-F8 confirmed.

## B.10 Lock date (D-08)

- Set by ADM in Settings.
- Nothing financial dated on or before the lock date can be created or reversed by non-ADM
  users. ADM can do it with a mandatory reason, recorded in the audit log.

## B.11 Numbering sequences (Q-Q1, Q-P2, Q-F6) — formats PENDING APPROVAL

| Sequence | Proposed default token format | Reset |
|---|---|---|
| Enquiry | `ENQ-{yyyy}-{seq4}` | yearly |
| Project | `AJ-{yyyy}-{seq3}` (example in Q-P2) | yearly |
| Quotation | `{seq}/{yyyy}` (matches the sample) | yearly — calendar year or financial year PENDING |
| Bill | `B/{fy}/{seq4}` | financial year |
| Credit note | `CN/{fy}/{seq4}` | financial year |
| Receipt | `R/{fy}/{seq4}` | financial year |
| Refund | `RF/{fy}/{seq4}` | financial year |
| Expense | `EX/{fy}/{seq4}` | financial year |

`{fy}` = financial year, e.g. 2026-27. The April–March financial year is an ASSUMPTION (Q-G8).

## B.12 Financial test cases to prepare (Stage 9)

1. Area + item lines; discount on/off; tax on/off; each rounding mode.
2. An advance, then a bill, then applying the credit.
3. A partial payment across two bills.
4. Reversing a payment that was allocated to two bills.
5. Credit note on a paid bill, then a refund.
6. Cancelling a bill that has payments allocated → blocked.
7. A fee agreement variation, then the outstanding amount in Mode B.
8. A lock-date breach by a non-ADM user → blocked.
9. Two users posting at the same moment → numbers stay unique, with no gaps caused by
   rollbacks (or gaps documented).
