# Business Workflows — Enquiry → Project → Quotation, Finance, Commission, Portfolio

**Status: PROPOSED — Stage 1 not approved.** Corrected 2026-11-06 (items WF-01…WF-16,
C-01…C-17 in `docs/STAGE1_CORRECTION_TRACKING_MATRIX.md`). Tags: `CLAUDE.md` §3.

All amounts in examples are **invented, for illustration only** — not defaults and not the sample
quotation's values. **Every financial step in this document is performed and seen by ADM only**
[CLIENT-DECISION]; non-ADM users see no amounts (`SECURITY_RULES.md` §8.1).

---

# PART A — Enquiry → Project → Quotation

## A.1 Overview

```
        ┌──────────── Website form (status: New – unreviewed)
        │  ┌───────── Manual: phone / WhatsApp / walk-in / Instagram / contractor / referral / other
        ▼  ▼
   ┌──────────┐  spam / duplicate / not relevant   ┌──────────┐
   │ ENQUIRY  │ ──────────────────────────────────►│  Closed  │
   └────┬─────┘                                    └──────────┘
        │ activities (calls, meetings, pre-project site visits — C-03), follow-ups
        │ source + contractor/referral partner recorded
   ┌────┴──────────────────────────────┐
   │ Path 1: quote the prospect (ADM)  │ Path 2: convert first
   ▼                                   ▼
 QUOTATION (enquiry)            CONVERT → CLIENT + PROJECT (status Proposal)
   │ Sent → Accepted (ADM)             │
   ▼                                   ▼
 CONVERT (forced in the same step) ◄── QUOTATION (project) — Sent → Accepted (ADM)
   └──────────────┬────────────────────┘
                  ▼
   FEE AGREEMENT for the project (A.4, B.2)  ─►  if source = Contractor: commission record in Draft (Part C)
                  ▼
   PROJECT status: Design → … → Completed
                  ▼
   (optional, consent + review) PORTFOLIO item (Part D)
```
Both paths are supported (C-01); the default path is PENDING Q-G2.

## A.2 Enquiry lifecycle

| Status | Entered when | Allowed next | Required data |
|---|---|---|---|
| New – unreviewed | Website form submitted | New, Closed | Name, mobile, consent |
| New | Created by hand, or reviewed | Contacted, Closed | Name, mobile, source; partner if source is contractor/referral |
| Contacted | First contact made | Meeting / site visit, Quotation sent, Lost, Closed | Activity |
| Meeting / site visit | Meeting or visit held/scheduled | Quotation sent, Lost | Activity with date |
| Quotation sent | Its quotation reaches Sent | Converted, Lost | Linked quotation |
| Converted | Turned into client + project | — | Client ID, project ID |
| Lost | Prospect declined | New (re-open) | Lost reason |
| Closed | Spam, duplicate, not relevant | — | Close reason |

Rules:
- Duplicate check on mobile/email against open enquiries and clients.
- **Conversion** copies name, contacts, location, project type, area, services, **source type and
  referral partner** into a new or existing client and a new project; links the enquiry's
  quotations to the project; nothing is deleted. If the source is contractor/referral, a
  commission record is created in **Draft** with *applicable* not set (C.2).
- Every status change → activity (no amounts) + audit log.
- Retention of Lost/Closed enquiries PENDING Q-G7.

## A.3 Project lifecycle (C-02)

Statuses: **Proposal** (opened before acceptance, Path 2), Design, Working drawings,
Approval/Municipal, Under construction (supervision), Interiors, Completed, On hold, Cancelled.
List PENDING Q-P1; labels editable; any change allowed except back to Proposal; history kept.
Cancelling or financially closing a project runs B.8 and C.5 first.

## A.4 Quotation lifecycle (C-04) — ADM for pricing and decisions [CLIENT-DECISION E-21]

```
 R0 Draft ──edit──► R0 Draft                (scope drafting by STF only if Q-U4 allows; no prices)
   │ Send (ADM; or Approve → Send if the approval step is on — Q-Q8)
   ▼
 R0 Sent ──changes requested──► "Create revision" → R1 Draft (copy); R0 → Superseded
   ├─► Accepted (ADM) ─► conversion if needed ─► fee agreement (B.2) ─► commission prompt (C.2)
   ├─► Rejected (reason)
   ├─► Expired (validity ended, if used)
   └─► Cancelled (reason)
```
Rules:
- Sent, Accepted, Rejected, Expired and Superseded revisions are never edited. One Accepted revision
  per quotation; acceptance is final — later scope changes are fee **variations** (B.2).
- **Order on acceptance from an enquiry (WF-04):** accept → convert (client + project) in the same
  transaction → create the fee agreement for the new project. A fee agreement never exists without a project.
- Quotation number taken on **first send** (D-28, PROPOSED; was D-09 "on creation").
- Rates: no default is pre-filled unless ADM set one; ADM can change any rate [CLIENT-DECISION].
- GST: per revision via **Apply GST** (only when the studio is GST-registered); never compulsory
  [CLIENT-DECISION]; default **off** (D-27).
- The PDF is generated from the frozen revision on the logo + visiting-card letterhead; it never
  shows commission or partner data.
- "Send" is a status change; emailing from the ERP is optional (Q-Q9).

## A.5 Calculation order (D-10, PROPOSED) — quotation revision, fee agreement, variation, bill

1. Line amounts: area × rate; quantity × rate; fixed/custom = entered. Rounded half-up to the paisa.
2. Subtotal = Σ lines.
3. Discount (if enabled): amount or % of subtotal (to the paisa); ≤ subtotal.
4. Taxable value = subtotal − discount.
5. **GST only if the document's Apply GST = Yes:** one line per tax (CGST+SGST or IGST by place of
   supply — rule PENDING Q-F3); each = taxable × rate, to the paisa.
6. Total before rounding = taxable + taxes.
7. Rounding (none / ₹1 / ₹10) as a separate stored line.
8. Grand total and all intermediate amounts stored.
9. Amount in words (Indian system) — optional (Q-Q6).

Example (invented): 1,250 sq.ft × ₹90 = ₹1,12,500.00; 4 views × ₹2,500 = ₹10,000.00;
subtotal ₹1,22,500.00; no discount; GST off; no rounding; total ₹1,22,500.00.

## A.6 Payment schedule (stages) [CLIENT-DECISION: staged payments supported]

- Lines: stage name, % of total **or** fixed amount, trigger text, optional due date.
- **One validation rule for quotation schedules and fee-agreement stages (WF-11):** drafts may be
  incomplete with a warning; the schedule must equal exactly 100% / the total before the quotation
  is sent or the agreement's stages are saved as final. Rounding difference goes to the last stage.
- Whether stages are computed on the total including or excluding GST: **PENDING Q-F2**.

---

# PART B — Financial workflow (ADM only)

## B.1 Building blocks

| Document | Purpose | Edit? | Corrected by |
|---|---|---|---|
| Fee agreement | Agreed fee for a project (from accepted revision or manual) | Never | Variation; cancel + new agreement |
| Fee variation | +/− change with reason, own GST switch | Never | Opposite variation |
| Payment stage | Expected amount per stage | Until billed or paid | Variation / re-plan |
| Bill (demand note / tax invoice) | Request for payment (bills method) | While Draft | Cancel + re-issue, or credit note |
| Credit note | Reduces an issued bill | Never | Its own cancellation |
| Payment / receipt | Money received | Never | Reversal |
| Allocation | Applies money to one target | Never | Allocation reversal |
| Credit transfer ◇ | Moves credit between projects of a client | Never | Reversal |
| Refund ◇ | Money paid back from credit | Never | Reversal |
| Write-off ◇ | Writes off an unpaid amount | Never | Reversal |
| Expense | Money spent by the studio | Never | Reversal |

Every record: unique number, never deleted, reversal points to the original with a reason, lock
date applies (B.10), audit log entry.

## B.2 Fee agreement and variations

- Created automatically on acceptance (after conversion — A.4): agreed total = revision grand total;
  GST switch, taxable amount and tax lines copied; schedule lines copied as stages.
- Manual agreement (no quotation): ADM, mandatory reason.
- **Optional:** a project may have no agreement at all (e.g. a small item-wise job billed ad hoc).
- Variations: signed amount, own **Apply GST** switch and tax lines, reason, optional link to a new
  quotation revision. Current agreed total = original total + Σ variations.
- One **active** agreement per project; a cancelled agreement may be replaced (DB-08).

## B.3 Billing methods — per project (WF-01, D-26) [CLIENT-DECISION: flexible, not agreement-only]

| | **Agreement method** | **Bills method** |
|---|---|---|
| Payment request | Stage reminder / follow-up; no bill needed | Bill issued (from a stage, manual lines, chargeable visit or reimbursable expense, or **ad hoc without an agreement**) |
| Payments applied to | A stage, or the agreement | Bills |
| GST | Per agreement/variation (if registered) | Per bill (if registered) |
| Receipt | Always | Always |
| Outstanding | B.4 formula (agreement) | B.4 formula (bills) |

- Each project has a billing method; the default comes from Settings. ADM may change it while the
  project has **no issued bill** (D-26). Both methods run side by side across projects.
- Superseded: the earlier studio-wide "Mode A / Mode B" switch (C-07).

## B.4 Payments, partial payments, advances and allocation [CLIENT-DECISION]

```
 Payment received (date, client, project, any amount > 0, mode, reference)
        │ posted → receipt number
        ▼
 Allocation (ADM): each row targets exactly ONE of  bill | stage | agreement   (D-29)
   bills method → open bills of the project
   agreement method → open stages, else the agreement
        │
        ▼
 Unallocated remainder = project CREDIT (advance)
```

- **Partial payments are always accepted (WF-09):** no validation rejects a payment for being smaller
  than the amount due; a partly covered bill/stage shows Partly paid.
- **Advances:** a payment before any bill/stage is due, or larger than what is open, stays unallocated
  as credit; the receipt reads "Advance against <project>". Advances before a project exists: PENDING Q-F12.
- **Apply credit later:** allocation rows from the earlier payment to the new target; the payment is unchanged.
- Allocation limits: Σ net allocations of a payment ≤ payment amount; to a bill ≤ bill total −
  credit notes − write-offs; to a stage ≤ stage amount; to an agreement ≤ current agreed total.
- Allocations are per project. Moving credit to another project of the same client uses a **credit
  transfer** ◇ (DB-07, Q-F11) — never an allocation row.
- Bill and stage statuses (Partly paid / Paid) are calculated, never set by hand.

**Formulas (per project; "net" = after reversals) — WF-05, WF-06, WF-07**

| Term | Calculation |
|---|---|
| Net received | Σ payments + Σ payment reversals (negative) |
| Net allocated | Σ allocations + Σ allocation reversals |
| Credit (both methods) | Net received − net allocated − net refunds − credit transferred out + credit transferred in |
| Agreed total | Original agreement total + Σ variations (active agreement only) |
| Outstanding — agreement method | Agreed total − net allocated − net write-offs |
| Billed — bills method | Σ grand totals of bills with status Issued (cancelled bills excluded) |
| Outstanding — bills method | Billed − Σ issued credit notes (not cancelled) − net allocated to bills − net write-offs |
| Client figure | Sum over the client's projects |

## B.5 Payment reversal (ADM only — WF-10)
1. ADM reverses a posted payment with reason and date.
2. A reversal record (−amount, `reverses_id`, own receipt-sequence number; separate "RV" sequence D-12).
3. All active allocations of the payment are reversed automatically; targets return to Partly paid / open.
4. Original receipt marked REVERSED (watermark on reprint).
5. Wrong amount → reverse and post a new payment.
6. If a commission's base is "amounts received" (Q-C3), the earned-to-date figure is recalculated;
   **paid commission is never edited** — any excess shows as recoverable (C.4).
7. Bounced-cheque charges not assumed (Q-F5).

## B.6 Refunds ◇ (C-14, Q-F9)
From available credit only (B.4 formula, either method); ADM; own number; reduces credit; reversal to correct.

## B.7 Bills and credit notes (bills method)
- Draft lines from stages, manual/fixed/custom lines, chargeable visits (C-17), reimbursable expenses
  (C-16) — the last two only if enabled. Calculation A.5; GST per bill.
- Issue: number taken, frozen, PDF. Cancel: only if nothing is allocated; keeps its number.
- **Credit note (WF-08):** total ≤ bill grand total − earlier credit notes − write-offs on the bill. If it
  exceeds what is still open on the bill, the excess becomes project credit. Tax lines follow the bill's
  GST switch and rates.

## B.8 Project cancellation / financial close
Shows outstanding, credit and commission status. Credit: refund ◇, transfer ◇ or retain (reason).
Outstanding: write-off ◇ (ADM, reason) or keep open. Commission: C.5.

## B.9 Expenses (ADM only — WF-15)
Fields as in `ERP_PAGES_AND_FIELDS.md` §2.14. Posted on save (D-14); reversal to correct.
Staff expense **claims** (submitted → ADM approves → posted) only if Q-U4 allows; off by default.
Commission payments are not expenses.

## B.10 Lock date (D-08)
ADM sets it. Financial or commission records dated on/before it cannot be created or reversed
except by ADM with a reason (audited).

## B.11 Numbering (D-28, PROPOSED) [CLIENT-DECISION: developer proposes]

| Sequence | Proposed format | Reset |
|---|---|---|
| Enquiry | `AJDS/E/{fy}/{seq4}` | FY |
| Project | `AJDS/P/{fy}/{seq3}` | FY |
| Quotation | `AJDS/Q/{fy}/{seq3}` (+ `-R{n}` on the PDF) — number on first send | FY |
| Bill | `AJDS/B/{fy}/{seq4}` | FY |
| Credit note | `AJDS/CN/{fy}/{seq4}` | FY |
| Receipt | `AJDS/R/{fy}/{seq4}` (reversals `AJDS/RV/…` — D-12) | FY |
| Refund ◇ | `AJDS/RF/{fy}/{seq4}` | FY |
| Write-off ◇ | `AJDS/WO/{fy}/{seq4}` | FY |
| Credit transfer ◇ | `AJDS/CT/{fy}/{seq4}` | FY |
| Expense | `AJDS/EX/{fy}/{seq4}` | FY |
| Commission payment | `AJDS/CP/{fy}/{seq4}` | FY |
`{fy}` = e.g. 2026-27; April–March is an ASSUMPTION (Q-G8). If the studio is GST-registered, tax
invoice numbering must also satisfy GST rules (Q-F3).

## B.12 Financial test cases (Stage 9 — to be executed, not yet run)
1. Area + item lines; discount on/off; GST on/off; each rounding mode.
2. **Two quotations of one project, one with GST and one without.**
3. **An agreement-method project and a bills-method project side by side**; switching method blocked after a bill is issued.
4. **Ad-hoc bill without a fee agreement.**
5. Advance, then a bill, then applying the credit.
6. **Partial payment below the amount due** — accepted; target shows Partly paid.
7. Partial payment across two bills; across two stages (agreement method).
8. **Allocation with two targets — blocked (XOR).**
9. Reversing a payment allocated to two bills.
10. Credit note on a fully paid bill → excess becomes credit → refund ◇.
11. Cancelling a bill with allocations → blocked.
12. Variation (with and without GST), then outstanding in the agreement method.
13. **Write-off, then outstanding and bill status.**
14. Lock-date breach by a non-ADM user → blocked.
15. Concurrent postings → unique numbers.
16. **Every financial route, API, export and PDF requested as STF and SITE → 403 / no amounts.**

---

# PART C — Contractor / referral commission (ADM only) [CLIENT-DECISION; design PROPOSED, D-32]

## C.1 Principles
- Project source is **Direct** or **Contractor** (separate "Referral" value PENDING Q-C2).
- Commission is **never automatic** and **never allowed on Direct projects**; it is recorded only
  when applicable and approved; all commission data is ADM-only and never on client documents.
- Direction assumed: the studio pays the partner (ASSUMPTION A7, PENDING Q-C1).

## C.2 Lifecycle

```
Contractor-source project created (conversion or manual)
        │  system creates commission record: status Draft, applicable = (not set)
        ▼
ADM decides applicable?
   ├─ No  → status "Not applicable" (remark) — closed; can be re-opened by ADM with reason
   └─ Yes → ADM enters type (Percentage / Fixed), rate or amount, base (PENDING Q-C3), remarks
              │ amount calculated: base × rate (to the paisa) or fixed amount; base snapshot stored
              ▼
          Pending approval ──► Approved (ADM, remark)   ──► payments (C.3)
                           └─► Rejected (ADM, reason)    ──► may be re-drafted
Approved ──► Cancelled (ADM, reason; only if net paid = 0, otherwise C.5)
```
- Approved terms are frozen. Later changes (e.g. after a fee variation) are **adjustments** (signed,
  reason, ADM). Whether a fee variation should change commission is PENDING Q-C3.
- Every step → `commission_status_history` + audit log; no amounts in the shared timeline.

## C.3 Commission payments
- Only for Approved commissions. Any amount > 0 (partial allowed), any number of payments.
- Fields: date, amount, mode, reference, proof file (private, financial), notes; TDS amount only if
  Q-C4 requires it.
- Limit: Σ net commission payments ≤ commission amount + Σ adjustments.
- Wrong entry → **reversal** (ADM, reason); never edited or deleted. Internal payment voucher PDF (ADM).

## C.4 Amounts
| Term | Calculation |
|---|---|
| Payable | Approved commission amount + Σ adjustments |
| Paid | Σ commission payments + Σ reversals |
| Outstanding | Payable − Paid |
| Earned to date (only if base = amounts received) | Net allocated client receipts × rate — shown beside Payable; rule PENDING Q-C3 |
| Recoverable | Paid − Payable, when negative outstanding arises after an adjustment (no automatic clawback) |

## C.5 Project cancellation, non-payment
What happens to approved or partly paid commission when the project is cancelled or the client does
not pay is **PENDING Q-C6**. Until decided: the system shows the commission position during B.8 and
requires an ADM decision (cancel unpaid part via adjustment / keep / mark recoverable) with a reason.

## C.6 Commission test cases (Stage 9 — to be executed)
1. Commission on a Direct project → blocked (UI and server).
2. Contractor project, applicable = No → no payments possible.
3. Percentage commission → amount = base × rate (paisa rounding); fixed commission.
4. Payment before approval → blocked.
5. Two partial payments, then a reversal → outstanding correct.
6. Overpayment beyond payable → blocked.
7. Adjustment after a fee variation → payable and outstanding correct.
8. Commission figures requested as STF/SITE (pages, API, reports, exports, timeline) → none returned.
9. Quotation/bill/receipt PDFs never contain commission or partner data.

---

# PART D — Portfolio publishing (WF-14) [CLIENT-DECISION: major projects, removal, no private info]

```
Draft ──(consent recorded + cover image + alt text on all images + content review approved)──► Published
  ▲                                                                                              │
  └──────────── Re-publish ◄── Unpublished (reason) ◄────────────────────────────────────────────┤
                                                                                                 ▼
                                                                         Removed (soft delete, reason)
```
- **Upload:** originals stored privately; nothing public yet (D-31).
- **Publish (ADM):** web versions copied to the public folder; added to listings and `sitemap.xml`.
- **Unpublish / remove (ADM):** public copies deleted; removed from listings and sitemap; the URL
  returns 410 (removed) or 404; reason recorded; audit log.
- **Slug change:** old slug kept and redirected (301).
- **Display sequence:** highlighted (major) by display priority → others by display priority →
  completion year (newest first) → title. Featured flag controls the home page selection.
- **Content:** drafted from the Instagram presence and reference documents; status
  "pending client review" until the client reviews it (W-16). Never uses
  `reference/portfolio/Senior office profile.pdf` (another architect's work).
- Which projects are "major", and the source of photos: PENDING Q-W1. Who may publish besides ADM: PENDING Q-W11.
