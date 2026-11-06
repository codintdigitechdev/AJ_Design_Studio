# Business Requirements

Status tags: **CONFIRMED-REF · CLIENT-DECISION · BRIEF · PROPOSED · ASSUMPTION · PENDING**
(`CLAUDE.md` §3). PENDING items carry a question ID from `docs/CLIENT_QUESTIONS.md`.
Client decisions are listed with date and source in `docs/CLIENT_QUESTIONS.md` §0.

---

## 1. Current situation (as understood)

- No website; online presence is the Instagram profile @ar.ajkumbhar. [CONFIRMED-REF]
- Quotations appear to be typed documents with a manually numbered reference ("Ref: 1/2025"). [ASSUMPTION]
- Some projects come directly, some through contractors/referral sources who may earn
  commission. [CLIENT-DECISION]
- Records are kept today in a mix of notebooks, files and WhatsApp [CLIENT-DECISION CD-90]; nothing is imported (CD-38).

## 2. Core business flow [PROPOSED; both paths used — CLIENT-DECISION CD-89]

```
Website form / WhatsApp / phone / walk-in / Instagram / contractor or referral source
          │
          ▼
     ENQUIRY (source; contractor/referral partner if any) ──► follow-ups ──► Lost / Closed
          │
          ├── Path 1: QUOTATION to the prospect ──► Accepted (Admin) ──► convert
          └── Path 2: convert first ──► CLIENT + PROJECT ──► QUOTATION ──► Accepted (Admin)
                                   │
                                   ▼
             CLIENT + PROJECT (source Direct / Contractor; billing method)
                                   │
                                   ├── FEE AGREEMENT (from accepted revision, or manual)
                                   ├── optional payment schedule (stages)
                                   ├── BILLS (bills method) / collections against agreement (agreement method)
                                   ├── PAYMENTS & RECEIPTS (partial, advances, allocation)
                                   ├── COMMISSION (contractor projects only, when applicable and approved)
                                   ├── project stages, site visits, documents, expenses
                                   └── (optional, with consent) PORTFOLIO item
```
A quotation can be created from an enquiry (prospect) or from a project; both paths are
supported (`docs/WORKFLOWS.md` A.1). [PROPOSED]

## 3. Public website requirements

| ID | Requirement | Status |
|---|---|---|
| W-01 | Public pages without login: Home, About Studio, Services, Portfolio, Project Details (with gallery), Contact, Enquiry | BRIEF + CLIENT-DECISION CD-44 (Gallery merged into Portfolio) |
| W-02 | Premium, professional look aligned with logo and visiting-card colours | BRIEF |
| W-03 | Responsive: mobile, tablet, desktop | BRIEF |
| W-04 | High-quality project galleries | BRIEF |
| W-05 | Contact details + WhatsApp enquiry button, details taken from Instagram and reference documents | CLIENT-DECISION (Sai Arcade Building; only 8806956877 published, also WhatsApp — CD-45, CD-46) |
| W-06 | Enquiry form saved into the ERP **Website Enquiries** inbox, separate from manual enquiries | BRIEF + CLIENT-DECISION CD-31 |
| W-07 | SEO-friendly URLs, meta tags, sitemap | BRIEF |
| W-08 | Portfolio and page content editable from the ERP | BRIEF |
| W-09 | Email notification to ar.ajitkumbhar16@gmail.com on each new enquiry, sent from a domain mailbox | CLIENT-DECISION CD-48 |
| W-10 | Google Map of office | CLIENT-DECISION — map from the address, pin checked on staging; visits by appointment (CD-95, CD-96) |
| W-11 | Testimonials only with client permission; Council of Architecture registration number shown | CLIENT-DECISION CD-49 (number to be supplied — Q-W7) |
| W-12 | Public website in **English and Marathi**; printed documents (quotation, bill, receipt) in English or Marathi; ERP screens in English | CLIENT-DECISION CD-50 |
| W-13 | Spam protection: simple built-in CAPTCHA + honeypot + rate limit | CLIENT-DECISION CD-48 / PROPOSED |
| W-14 | Detailed website content **drafted by CodInt** from the Instagram presence and reference documents | CLIENT-DECISION (client sends original photos — CD-43) |
| W-15 | Tone: professional, formal and ethical; no unverifiable claims, invented numbers, awards or testimonials | CLIENT-DECISION |
| W-16 | Client reviews website content later; each content block carries a review status and nothing unreviewed goes live at launch | CLIENT-DECISION (review) / PROPOSED (status mechanism) |
| W-17 | Portfolio includes all major projects and available photographs; major projects are prioritised and can be highlighted; sensible display sequence | CLIENT-DECISION (client sends original photos — CD-43; the client marks "major" projects — CD-97) |
| W-18 | Projects can be unpublished or removed later; removal also withdraws their public images | CLIENT-DECISION (removal) / PROPOSED (mechanism) |
| W-19 | No invented project details; no private client information without approval; client names shown only with that client's permission | CLIENT-DECISION (CD-11, CD-47) |
| W-20 | Demo services may be used initially; whether they may appear on the live public site before confirmation | CLIENT-DECISION — demo services stay in the ERP, never on the public site (CD-06, CD-42) |

## 4. ERP requirements

| ID | Requirement | Status |
|---|---|---|
| E-01 | Separate secure login at `/erp/login` | BRIEF |
| E-02 | Role-based access for authorized users only | BRIEF |
| E-03 | Enquiry management (manual) with status, activities (incl. pre-project meetings/visits — CD-78) and follow-ups; **separate Website Enquiries inbox** with conversion; Admin date-wise delete | BRIEF + CLIENT-DECISION CD-31, CD-34 |
| E-04 | Client master | BRIEF |
| E-05 | Project management (site; type Architectural/Civil/Interior/Landscape; area; status Planned/OnGoing/OnHold/Completed/HandOver/Cancelled; team; **source Direct/Contractor/Referral**; billing method) | BRIEF + CLIENT-DECISION CD-41, CD-71, CD-76 |
| E-06 | Service / work-category master; Admin can add, update and soft-delete categories and services; demo items flagged; final public list = the quotation categories (CD-94) | CLIENT-DECISION CD-06, CD-07, CD-94 |
| E-07 | Quotations: area-based and item-wise (plus fixed and custom lines), no mandatory fixed pricing, Admin-editable rates, revisions, approval status, PDF/print on logo + visiting-card letterhead ("श्री", no QR), acceptance block, all term sections, English/Marathi print, shared by download + WhatsApp, discount ≤ 5% | CLIENT-DECISION (CD-13…CD-17, CD-53…CD-57, CD-61) |
| E-08 | Design fees and billing — **flexible, not agreement-only**: per-project billing method (agreement or bills), ad-hoc bills allowed | CLIENT-DECISION (flexibility) / PROPOSED (per-project method, D-26) |
| E-09 | Payments and receipts: **partial payments always allowed**, advances (also before a project exists), allocation, staged payment schedules, numbered receipts, modes Online/Cash/UPI | CLIENT-DECISION (CD-22…CD-24, CD-63, CD-64, CD-69) |
| E-10 | Expenses: rent, travel and similar; Admin-only | CLIENT-DECISION CD-65 |
| E-11 | Project documents and attachments (private) | BRIEF |
| E-12 | Portfolio and gallery management with publish/unpublish/remove | BRIEF + CLIENT-DECISION |
| E-13 | Follow-ups and reminders on the dashboard, with emails for priority items | CLIENT-DECISION CD-32 |
| E-14 | Reports, including source and commission reports | CLIENT-DECISION (all proposed reports — CD-84) |
| E-15 | User and role management; only the Admin uses the ERP for now; no two-step login; mobile use allowed | CLIENT-DECISION CD-80…CD-82 |
| E-16 | Organization settings (letterhead, numbering, GST profile, terms, website content) | BRIEF |
| E-17 | Audit log of important operations, incl. every financial and commission action | BRIEF |
| E-18 | Financial corrections via reversal/adjustment, never silent overwrite (incl. commission) | BRIEF |
| E-19 | Site-visit log against a project (date, stage, notes, photos), no visit limits | CLIENT-DECISION CD-77 |
| E-20 | Client portal / client login | Not needed — CLIENT-DECISION CD-33 |
| **E-21** | **Financial information and financial decisions are Admin-only** — see §4.1 | **CLIENT-DECISION** |
| **E-22** | Project source **Direct / Contractor**; contractor/referral source details recorded | **CLIENT-DECISION** — Direct / Contractor / Referral (CD-71) |
| **E-23** | Commission: applicable Yes/No; type Percentage/Fixed; rate and amount; approval status; paid and outstanding amounts; commission payment records and dates; remarks; audit history | **CLIENT-DECISION** |
| **E-24** | Commission never applies automatically and never to direct projects; recorded only when applicable and approved; visible to Admin only | **CLIENT-DECISION** |
| E-25 | GST optional and configurable; not compulsory for any quotation or project; actual tax treatment confirmed with the client's adviser | CLIENT-DECISION — not GST-registered today, GST off (CD-60) |
| E-26 | Commission: studio pays one partner per project; % of final fee excl. GST incl. variations; payable on completion; GST may apply; Admin decides on cancellation/non-payment | CLIENT-DECISION CD-70, CD-72, CD-73, CD-75 (TDS field kept, off — CD-92) |
| E-27 | Refunds with an optional percentage deduction; write-offs Admin-only; no credit transfer between projects | CLIENT-DECISION CD-66…CD-68 |

### 4.1 Financial data definition (E-21) [CLIENT-DECISION for the rule; PROPOSED for the list]

"Financial data" — visible to, entered by and decided by **ADM only** — includes:
- fees, rates (incl. service default rates), quotation amounts, discounts, tax amounts and totals;
- quotation send / accept / reject decisions on priced quotations;
- fee agreements, variations, payment schedules (milestones), bills, credit notes;
- payments, receipts, allocations, advances/credit, refunds, write-offs;
- expenses;
- **all commission data**, including whether commission applies to a project, and partner bank/tax details;
- balances, outstanding, profitability, financial dashboard widgets and reports;
- finance settings (billing method default, GST profile, rounding, lock date, financial numbering);
- document categories flagged financial (agreements, bills, receipts, payment proofs, commission documents);
- CSV/PDF exports, notifications, email digests, activity-timeline entries and API/AJAX responses
  that would reveal any of the above.

Edge cases — whether staff may draft quotation **scope** without prices, send an Admin-approved
PDF, or submit expense claims for Admin approval — are **not allowed** [CLIENT-DECISION CD-83].

## 5. Quotation business rules

| ID | Rule | Status |
|---|---|---|
| Q-R01 | Calculation methods: area-based, area per category, fixed fee, item-wise, custom charges (combinable) | CLIENT-DECISION (area + item-wise) / PROPOSED (others) |
| Q-R02 | Rate, area unit and rounding entered per quotation; defaults optional and set by Admin | CLIENT-DECISION (Admin rates) / PROPOSED |
| Q-R03 | No hardcoded ₹100/sq.ft or 1100 sq.ft; no mandatory fixed pricing | CONFIRMED-REF (dummy) + CLIENT-DECISION |
| Q-R04 | Discount (max 5%), payment schedule (% of total incl. GST), all standard term sections drafted by CodInt for client review | CLIENT-DECISION CD-56, CD-59, CD-61 |
| Q-R05 | Scope built from service categories with editable sub-items | PROPOSED |
| Q-R06 | Every change after "Sent" creates a new revision; old revisions read-only | PROPOSED |
| Q-R07 | Revision statuses: Draft, Sent, Accepted, Rejected, Expired, Cancelled, Superseded (no "Revised" status — C-04); no separate approval step | PROPOSED + CLIENT-DECISION CD-93 |
| Q-R08 | Quotation number `AJDS/Q/{fy}/{seq3}` (e.g. AJDS/Q/2026-27/001), -R{n} for revisions; number taken on first send | CLIENT-DECISION CD-52 (format) / PROPOSED (timing) |
| Q-R09 | Acceptance block on the PDF; amount in words and client block not requested (off) | CLIENT-DECISION CD-55 |
| Q-R10 | GST applied per quotation revision only when switched on; never compulsory; studio not registered today | CLIENT-DECISION CD-19, CD-20, CD-60 / PROPOSED (switch) |
| Q-R11 | Commission and partner data never appear on any client-facing document | PROPOSED |
| Q-R12 | Pricing, sending and accepting/rejecting priced quotations are Admin-only | CLIENT-DECISION (E-21) |

## 6. Non-functional requirements

| ID | Requirement | Status |
|---|---|---|
| N-01 | Runs on Hostinger shared hosting (hPanel), latest PHP/MySQL, 10 GB+; kept portable to cPanel | CLIENT-DECISION CD-86, CD-91 |
| N-02 | Pages load fast on mobile data; images optimized, lazy-loaded | PROPOSED |
| N-03 | Documented, tested backup and restore; weekly encrypted off-site copy taken by CodInt Digitech | BRIEF / CLIENT-DECISION CD-88 / PROPOSED (encryption) |
| N-04 | Installation, user, testing and deployment guides | BRIEF |
| N-05 | Time zone Asia/Kolkata (IST; operations mainly within Maharashtra); currency INR only; DD/MM/YYYY; FY April–March; Indian number format | CLIENT-DECISION CD-27, CD-30, CD-35, CD-36 / PROPOSED (number format) |
| N-06 | Accessibility: WCAG 2.1 AA contrast and keyboard navigation for public site | PROPOSED |
| N-07 | Password-protected staging copy for client review before launch | CLIENT-DECISION CD-87 |

## 7. Explicitly not assumed / out of scope

Not requirements (design and supervision only — CLIENT-DECISION CD-40): construction execution/contracting, material
procurement or resale, turnkey interiors, **payments to construction contractors or vendors**,
payroll, inventory, GST filing, online payment gateway, client portal, mobile app, multi-branch,
multi-currency.

**In scope by client decision:** recording contractor/referral sources and the **commission**
the studio pays them (E-22…E-24, E-26). The studio pays one partner per project [CLIENT-DECISION CD-70].
