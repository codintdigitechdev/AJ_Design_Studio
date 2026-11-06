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
- How enquiries, payments, expenses and drawings are tracked today is unknown. [PENDING – Q-G1]

## 2. Core business flow [PROPOSED; default path PENDING – Q-G2]

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
| W-01 | Public pages without login: Home, About Studio, Services, Portfolio, Project Details, Gallery, Contact, Enquiry | BRIEF (Gallery page PENDING – Q-W2) |
| W-02 | Premium, professional look aligned with logo and visiting-card colours | BRIEF |
| W-03 | Responsive: mobile, tablet, desktop | BRIEF |
| W-04 | High-quality project galleries | BRIEF |
| W-05 | Contact details + WhatsApp enquiry button, details taken from Instagram and reference documents | CLIENT-DECISION (number and address spelling PENDING – Q-W3, Q-W4) |
| W-06 | Enquiry form saved into the ERP enquiry module | BRIEF |
| W-07 | SEO-friendly URLs, meta tags, sitemap | BRIEF |
| W-08 | Portfolio and page content editable from the ERP | BRIEF |
| W-09 | Email notification to studio on new enquiry | PROPOSED (PENDING – Q-W6) |
| W-10 | Google Map of office | PROPOSED (PENDING – Q-W3) |
| W-11 | Testimonials, only with real client consent | PROPOSED (PENDING – Q-W7) |
| W-12 | Marathi language version | PENDING – Q-W8 |
| W-13 | Spam protection (honeypot + rate limit; no CAPTCHA by default) | PROPOSED |
| W-14 | Detailed website content **drafted by CodInt** from the Instagram presence and reference documents | CLIENT-DECISION (source access PENDING – Q-W1) |
| W-15 | Tone: professional, formal and ethical; no unverifiable claims, invented numbers, awards or testimonials | CLIENT-DECISION |
| W-16 | Client reviews website content later; each content block carries a review status and nothing unreviewed goes live at launch | CLIENT-DECISION (review) / PROPOSED (status mechanism) |
| W-17 | Portfolio includes all major projects and available photographs; major projects are prioritised and can be highlighted; sensible display sequence | CLIENT-DECISION (which projects are "major": PENDING – Q-W1) |
| W-18 | Projects can be unpublished or removed later; removal also withdraws their public images | CLIENT-DECISION (removal) / PROPOSED (mechanism) |
| W-19 | No invented project details; no private client information published without approval | CLIENT-DECISION |
| W-20 | Demo services may be used initially; whether they may appear on the live public site before confirmation | CLIENT-DECISION (demo use) / PENDING – Q-S5 (public display) |

## 4. ERP requirements

| ID | Requirement | Status |
|---|---|---|
| E-01 | Separate secure login at `/erp/login` | BRIEF |
| E-02 | Role-based access for authorized users only | BRIEF |
| E-03 | Enquiry management (website + manual) with status, activities and follow-ups; one enquiry module | BRIEF (single module PROPOSED – Q-G4) |
| E-04 | Client master | BRIEF |
| E-05 | Project management (site, type, area, status, team, **source Direct/Contractor**, billing method) | BRIEF + CLIENT-DECISION (source) |
| E-06 | Service / work-category master; Admin can add, update and soft-delete categories and services; demo items flagged | CLIENT-DECISION |
| E-07 | Quotations: area-based and item-wise (plus fixed and custom lines), no mandatory fixed pricing, Admin-editable rates, revisions, approval status, PDF/print on logo + visiting-card letterhead | CLIENT-DECISION |
| E-08 | Design fees and billing — **flexible, not agreement-only**: per-project billing method (agreement or bills), ad-hoc bills allowed | CLIENT-DECISION (flexibility) / PROPOSED (per-project method, D-26) |
| E-09 | Payments and receipts: **partial payments always allowed**, advances, allocation, staged payment schedules | CLIENT-DECISION (receipt format PENDING – Q-F6) |
| E-10 | Expenses | PROPOSED (scope PENDING – Q-F8; Admin-only) |
| E-11 | Project documents and attachments (private) | BRIEF |
| E-12 | Portfolio and gallery management with publish/unpublish/remove | BRIEF + CLIENT-DECISION |
| E-13 | Follow-ups and reminders | BRIEF (channel PENDING – Q-G5) |
| E-14 | Reports, including source and commission reports | BRIEF + CLIENT-DECISION (list PENDING – Q-R1) |
| E-15 | User and role management | BRIEF (users PENDING – Q-U1) |
| E-16 | Organization settings (letterhead, numbering, GST profile, terms, website content) | BRIEF |
| E-17 | Audit log of important operations, incl. every financial and commission action | BRIEF |
| E-18 | Financial corrections via reversal/adjustment, never silent overwrite (incl. commission) | BRIEF |
| E-19 | Site-visit log against a project (date, stage, notes, photos) | PROPOSED – PENDING Q-P3 |
| E-20 | Client portal / client login | Out of scope unless requested – Q-G6 |
| **E-21** | **Financial information and financial decisions are Admin-only** — see §4.1 | **CLIENT-DECISION** |
| **E-22** | Project source **Direct / Contractor**; contractor/referral source details recorded | **CLIENT-DECISION** (separate "Referral" value PENDING – Q-C2) |
| **E-23** | Commission: applicable Yes/No; type Percentage/Fixed; rate and amount; approval status; paid and outstanding amounts; commission payment records and dates; remarks; audit history | **CLIENT-DECISION** |
| **E-24** | Commission never applies automatically and never to direct projects; recorded only when applicable and approved; visible to Admin only | **CLIENT-DECISION** |
| E-25 | GST optional and configurable; not compulsory for any quotation or project; actual tax treatment confirmed with the client's adviser | CLIENT-DECISION (treatment PENDING – Q-F3) |

### 4.1 Financial data definition (E-21) [CLIENT-DECISION for the rule; PROPOSED for the list]

"Financial data" — visible to, entered by and decided by **ADM only** — includes:
- fees, rates (incl. service default rates), quotation amounts, discounts, tax amounts and totals;
- quotation send / accept / reject decisions on priced quotations;
- fee agreements, variations, payment schedules (milestones), bills, credit notes;
- payments, receipts, allocations, advances/credit, refunds, write-offs, credit transfers;
- expenses;
- **all commission data**, including whether commission applies to a project, and partner bank/tax details;
- balances, outstanding, profitability, financial dashboard widgets and reports;
- finance settings (billing method default, GST profile, rounding, lock date, financial numbering);
- document categories flagged financial (agreements, bills, receipts, payment proofs, commission documents);
- CSV/PDF exports, notifications, email digests, activity-timeline entries and API/AJAX responses
  that would reveal any of the above.

Edge cases — whether staff may draft quotation **scope** without prices, send an Admin-approved
PDF, or submit expense claims for Admin approval — are **PENDING – Q-U4**. Until answered, the
documents treat them as **not allowed** (safest reading of the client decision).

## 5. Quotation business rules

| ID | Rule | Status |
|---|---|---|
| Q-R01 | Calculation methods: area-based, area per category, fixed fee, item-wise, custom charges (combinable) | CLIENT-DECISION (area + item-wise) / PROPOSED (others) |
| Q-R02 | Rate, area unit and rounding entered per quotation; defaults optional and set by Admin | CLIENT-DECISION (Admin rates) / PROPOSED |
| Q-R03 | No hardcoded ₹100/sq.ft or 1100 sq.ft; no mandatory fixed pricing | CONFIRMED-REF (dummy) + CLIENT-DECISION |
| Q-R04 | Discounts, payment schedule, validity, terms: configurable, off/blank by default until approved | BRIEF |
| Q-R05 | Scope built from service categories with editable sub-items | PROPOSED |
| Q-R06 | Every change after "Sent" creates a new revision; old revisions read-only | PROPOSED |
| Q-R07 | Revision statuses: Draft, Sent, Accepted, Rejected, Expired, Cancelled, Superseded (no "Revised" status — C-04) | PROPOSED – Q-Q8 |
| Q-R08 | Numbering proposed by the developer (proposal D-28: `AJDS/Q/{fy}/{seq3}`, number taken on first send) | CLIENT-DECISION (developer proposes) / PROPOSED (format) |
| Q-R09 | Amount in words on PDF (Indian system) | PROPOSED – Q-Q6 |
| Q-R10 | GST applied per quotation revision only when switched on; never compulsory | CLIENT-DECISION / PROPOSED (switch) |
| Q-R11 | Commission and partner data never appear on any client-facing document | PROPOSED |
| Q-R12 | Pricing, sending and accepting/rejecting priced quotations are Admin-only | CLIENT-DECISION (E-21) |

## 6. Non-functional requirements

| ID | Requirement | Status |
|---|---|---|
| N-01 | Works on cPanel shared hosting (PHP 8.1+, MySQL 5.7+/MariaDB 10.4+) | PROPOSED |
| N-02 | Pages load fast on mobile data; images optimized, lazy-loaded | PROPOSED |
| N-03 | Documented, tested backup and restore; off-site copies encrypted | BRIEF / PROPOSED (encryption) |
| N-04 | Installation, user, testing and deployment guides | BRIEF |
| N-05 | Time zone Asia/Kolkata, INR, Indian number format | ASSUMPTION |
| N-06 | Accessibility: WCAG 2.1 AA contrast and keyboard navigation for public site | PROPOSED |

## 7. Explicitly not assumed / out of scope

Not requirements unless the client confirms them: construction execution/contracting, material
procurement or resale, turnkey interiors, **payments to construction contractors or vendors**,
payroll, inventory, GST filing, online payment gateway, client portal, mobile app, multi-branch,
multi-currency.

**In scope by client decision:** recording contractor/referral sources and the **commission**
the studio pays them (E-22…E-24). Direction of commission (studio pays partner) is an
ASSUMPTION (A7) pending Q-C1.
