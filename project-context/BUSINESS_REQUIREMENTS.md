# Business Requirements

Status tags: **[CONFIRMED]** (in brief or references) · **[PROPOSED]** (our recommendation) ·
**[ASSUMPTION]** · **[PENDING]** (question ID in `docs/CLIENT_QUESTIONS.md`).

"CONFIRMED (brief)" means the developer brief requires it; the client has not yet
validated it against their workflow.

---

## 1. Current situation (as understood)

- No website; online presence is the Instagram profile @ar.ajkumbhar. [CONFIRMED]
- Quotations appear to be typed as documents (Word/PDF) with a letterhead and a
  manually numbered reference ("Ref: 1/2025"). [ASSUMPTION from the sample]
- How enquiries, payments, expenses and documents are tracked today is unknown. [PENDING – Q-G1]

## 2. Proposed core business flow [PROPOSED]

```
Website form / WhatsApp / phone / walk-in / referral
          │
          ▼
     ENQUIRY ──► follow-ups ──► (lost / dropped)
          │ converted
          ▼
     CLIENT ──► PROJECT (site, type, area)
                   │
                   ▼
              QUOTATION (draft → revision n → sent → accepted/rejected)
                   │ accepted
                   ▼
              FEE SCHEDULE / BILLS ──► PAYMENTS & RECEIPTS
                   │
                   ├── project stages & site visits
                   ├── documents (drawings, 3D, municipal)
                   ├── expenses
                   └── (optional) publish to PORTFOLIO
```

Whether this matches the studio's real sequence (e.g. are projects opened before
the quotation?) is **[PENDING – Q-G2]**.

## 3. Public website requirements

| ID | Requirement | Status |
|---|---|---|
| W-01 | Public pages without login: Home, About Studio, Services, Portfolio, Project Details, Gallery, Contact, Enquiry | CONFIRMED (brief) |
| W-02 | Premium, professional look aligned with logo colours | CONFIRMED |
| W-03 | Responsive: mobile, tablet, desktop | CONFIRMED |
| W-04 | High-quality project galleries | CONFIRMED |
| W-05 | Contact details + WhatsApp enquiry button | CONFIRMED (number PENDING – Q-W4) |
| W-06 | Enquiry form saved into ERP | CONFIRMED |
| W-07 | SEO-friendly URLs, meta tags, sitemap | CONFIRMED |
| W-08 | Portfolio and selected page content editable from ERP | CONFIRMED |
| W-09 | Email notification to studio on new enquiry | PROPOSED (PENDING – Q-W6) |
| W-10 | Google Map of office | PROPOSED (PENDING – Q-W3) |
| W-11 | Testimonials | PROPOSED, only with real client consent (PENDING – Q-W7) |
| W-12 | Marathi language version | PENDING – Q-W8 |
| W-13 | Spam protection on forms (honeypot + rate limit; no CAPTCHA by default) | PROPOSED |

## 4. ERP requirements

| ID | Requirement | Status |
|---|---|---|
| E-01 | Separate secure login at `/erp/login` | CONFIRMED |
| E-02 | Role-based access for authorized users only | CONFIRMED |
| E-03 | Enquiry management (website + manual) with status and follow-ups | CONFIRMED (brief) |
| E-04 | Client master | CONFIRMED (brief) |
| E-05 | Project management (site, type, area, status, stages) | CONFIRMED (brief) |
| E-06 | Service / work-category master (configurable, not hardcoded) | CONFIRMED (brief) |
| E-07 | Quotations: configurable calculation, PDF, print, revisions, approval status | CONFIRMED (brief) |
| E-08 | Design fees and billing | CONFIRMED (brief); billing model PENDING – Q-F1..F5 |
| E-09 | Payments and receipts | CONFIRMED (brief); receipt format PENDING – Q-F6 |
| E-10 | Expenses | CONFIRMED (brief); scope PENDING – Q-F8 |
| E-11 | Project documents and attachments (private) | CONFIRMED (brief) |
| E-12 | Portfolio and gallery management | CONFIRMED |
| E-13 | Follow-ups and reminders | CONFIRMED (brief); channel PENDING – Q-G5 |
| E-14 | Reports | CONFIRMED (brief); list PENDING – Q-R1 |
| E-15 | User and role management | CONFIRMED (brief); roles PENDING – Q-U1 |
| E-16 | Organization settings (letterhead, numbering, tax, terms) | CONFIRMED (brief) |
| E-17 | Audit log of important operations | CONFIRMED |
| E-18 | Financial corrections via reversal, never silent overwrite | CONFIRMED |
| E-19 | Site-visit log against a project (date, stage, notes, photos) | PROPOSED (sample lists many visit stages) – PENDING Q-P3 |
| E-20 | Client portal / client login | NOT IN SCOPE unless requested – Q-G6 |

## 5. Quotation business rules

| ID | Rule | Status |
|---|---|---|
| Q-R01 | Calculation methods: area-based, fixed fee, item-wise, custom charges | PROPOSED |
| Q-R02 | Rate, area unit, rounding are entered per quotation, with optional defaults in settings | PROPOSED |
| Q-R03 | No hardcoded ₹100/sq.ft or 1100 sq.ft | CONFIRMED |
| Q-R04 | GST/tax, discounts, payment schedule, validity, terms: configurable, default **off/blank** until approved | CONFIRMED (brief) |
| Q-R05 | Scope of work built from service categories with editable sub-items (as in sample sections 1–6) | PROPOSED |
| Q-R06 | Every change after "sent" creates a new revision; old revisions read-only | PROPOSED |
| Q-R07 | Statuses: Draft, Sent, Revised, Accepted, Rejected, Expired, Cancelled | PROPOSED – Q-Q8 |
| Q-R08 | Reference number format configurable (sample: `1/2025`) | PROPOSED – Q-Q1 |
| Q-R09 | Amount in words on PDF (Indian system) | PROPOSED – Q-Q6 |

## 6. Non-functional requirements

| ID | Requirement | Status |
|---|---|---|
| N-01 | Works on cPanel shared hosting (PHP 8.1+, MySQL 5.7+/MariaDB 10.4+) | PROPOSED |
| N-02 | Pages load fast on mobile data; images optimized, lazy-loaded | PROPOSED |
| N-03 | Documented backup and restore | CONFIRMED |
| N-04 | Installation, user, testing and deployment guides | CONFIRMED |
| N-05 | Time zone Asia/Kolkata, INR, Indian number format | ASSUMPTION |
| N-06 | Accessibility: WCAG 2.1 AA contrast and keyboard navigation for public site | PROPOSED |

## 7. Explicitly not assumed

The following are **not** requirements unless the client confirms them:
construction execution/contracting, material procurement or resale, turnkey
interiors, vendor/contractor payments, payroll, inventory, GST filing, online
payment gateway, client portal, mobile app, multi-branch, multi-currency.
