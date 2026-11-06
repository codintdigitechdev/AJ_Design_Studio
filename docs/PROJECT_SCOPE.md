# Project Scope

Project: AJ Design Studio – Portfolio Website + ERP Management System
Developer: CodInt Digitech · Client: AJ Design Studio · Principal Architect: Ar. Ajit Kumbhar
Version: 0.2 (corrected 2026-11-06) – **not approved**. Tags: `CLAUDE.md` §3.

## 1. Confirmed information
- **[BRIEF]** The client has no existing website; a new public portfolio website and a private ERP will be built.
- **[CLIENT-DECISION]** Same hosting account and domain `ajdesignstudios.in`: `/` public, `/erp/` ERP
  (spelling confirmed — CD-85).
- **[BRIEF]** Stack: Core PHP, MySQL/MariaDB, PDO, Bootstrap 5, HTML5/CSS3/JS, AJAX, XAMPP, cPanel.
- **[CONFIRMED-REF]** Studio identity and contacts from the quotation letterhead, visiting card and
  Instagram (Sai Arcade Building; 8806956877 published — CD-45, CD-46).
- **[CONFIRMED-REF]** Reference work categories from the sample quotation.
- **[BRIEF]** The sample quotation is a dummy, not the final template or pricing policy.
- **[CLIENT-DECISION]** CD-01…CD-90 (`docs/CLIENT_QUESTIONS.md` §0).

## 2. In scope (design PROPOSED, subject to approval)

### 2.1 Public website
Home · About Studio · Services · Portfolio · Project Details (with gallery — CD-44) · Contact · Enquiry form ·
WhatsApp enquiry · SEO · responsive design · content managed from the ERP · **English and Marathi** (CD-50).
**Website content drafting by CodInt** from the Instagram presence and reference documents, in a
professional, formal and ethical tone, for client review [CLIENT-DECISION CD-03…CD-05].

### 2.2 ERP
Dashboard · Website Enquiries inbox (CD-31) · Enquiries · Clients · Projects (+ site-visit log) · Services & categories
(demo first, Admin-managed) · Quotations (area-based and item-wise, revisions, approval, PDF) ·
Fees & billing (per-project method, optional GST) · Payments & receipts (staged, partial, advances,
allocation) · Expenses · Project documents (private) · Portfolio CMS · Follow-ups · Reports ·
Users & roles · Settings · Audit log · **Contractor/referral sources and commission** [CLIENT-DECISION CD-26].
All financial data Admin-only [CLIENT-DECISION CD-25]. Necessity ratings: `project-context/MODULES.md`.

### 2.3 Non-functional
Security controls, tested backup/restore with encrypted off-site copies, documentation set,
installation on XAMPP and cPanel, fictitious sample data.

## 3. Out of scope (unless the client requests and approves a change)
- Construction execution, contracting, material procurement/resale, turnkey interiors (design and supervision only — CD-40).
- **Payments to construction contractors or vendors**, labour/payroll, inventory.
  (Recording contractor/referral **commission** paid by the studio **is in scope** — CD-26.)
- GST return filing, accounting ledger, Tally integration.
- Online payment gateway, client portal (not needed — CD-33), native mobile apps, SMS/WhatsApp API automation.
- Credit transfer between projects (CD-68), emailing quotations from the ERP (CD-57), two-step login (CD-82),
  Marathi ERP screens (CD-50).
- Professional photography; content beyond the agreed website pages.
- Domain purchase, hosting purchase, business email set-up (advice only).
- Historical data migration (none needed — CD-38).
- Any use of `reference/portfolio/Senior office profile.pdf` (another architect's work; sample only — CD-39).

## 4. Assumptions and validated items
- **[CLIENT-DECISION]** INR only (CD-27); single office for now (CD-28); Ar. Ajit Kumbhar is owner and
  main Admin user (CD-29); operations mainly within Maharashtra, IST (CD-30).
- **[CLIENT-DECISION]** Only the Admin uses the ERP for now (CD-80).
- **[CLIENT-DECISION]** DD/MM/YYYY and FY April–March (CD-35, CD-36). **[PROPOSED]** Indian number format.
- **[CLIENT-DECISION]** English + Marathi website and documents; ERP in English (CD-50).
- **[CLIENT-DECISION]** The studio pays one partner per project (CD-70).
- The client supplies original photos and project facts, publishing consent, final service list
  and quotation terms; CodInt drafts text for client review.
- Hosting supports PHP 8.1+, MySQL/MariaDB, HTTPS, cron, GD, mbstring, bcmath, `finfo`, folders outside `public_html`.

## 5. Pending client decisions
Full list: `docs/CLIENT_QUESTIONS.md` §10. Remaining:
1. Hosting provider and plan (Q-H2) — the only P1 item.
2. TDS on commission (Q-C4) — before the commission module is built.
3. Final service list and website descriptions (Q-S1, Q-S4) — before launch.
4. Which projects are "major", office hours and map pin, Council of Architecture number (Q-W1, Q-W3, Q-W7).

## 6. Acceptance (proposed)
Each stage gate in `project-context/DEVELOPMENT_ROADMAP.md` is accepted in writing and logged.
Final acceptance: running application on production hosting, documents delivered, backup/restore
demonstrated, final ZIP handed over.
