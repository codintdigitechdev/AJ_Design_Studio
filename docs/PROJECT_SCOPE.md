# Project Scope

Project: AJ Design Studio – Portfolio Website + ERP Management System
Developer: CodInt Digitech · Client: AJ Design Studio · Principal Architect: Ar. Ajit Kumbhar
Version: 0.2 (corrected 2026-11-06) – **not approved**. Tags: `CLAUDE.md` §3.

## 1. Confirmed information
- **[BRIEF]** The client has no existing website; a new public portfolio website and a private ERP will be built.
- **[CLIENT-DECISION]** Same hosting account and domain `ajdesignstudios.in`: `/` public, `/erp/` ERP
  (spelling confirmation Q-H1).
- **[BRIEF]** Stack: Core PHP, MySQL/MariaDB, PDO, Bootstrap 5, HTML5/CSS3/JS, AJAX, XAMPP, cPanel.
- **[CONFIRMED-REF]** Studio identity and contacts from the quotation letterhead, visiting card and
  Instagram (address spelling and WhatsApp number: Q-W3, Q-W4).
- **[CONFIRMED-REF]** Reference work categories from the sample quotation.
- **[BRIEF]** The sample quotation is a dummy, not the final template or pricing policy.
- **[CLIENT-DECISION]** CD-01…CD-26 (`docs/CLIENT_QUESTIONS.md` §0).

## 2. In scope (design PROPOSED, subject to approval)

### 2.1 Public website
Home · About Studio · Services · Portfolio · Project Details · Gallery · Contact · Enquiry form ·
WhatsApp enquiry · SEO · responsive design · content managed from the ERP.
**Website content drafting by CodInt** from the Instagram presence and reference documents, in a
professional, formal and ethical tone, for client review [CLIENT-DECISION CD-03…CD-05].

### 2.2 ERP
Dashboard · Enquiries (incl. website) · Clients · Projects (+ site-visit log) · Services & categories
(demo first, Admin-managed) · Quotations (area-based and item-wise, revisions, approval, PDF) ·
Fees & billing (per-project method, optional GST) · Payments & receipts (staged, partial, advances,
allocation) · Expenses · Project documents (private) · Portfolio CMS · Follow-ups · Reports ·
Users & roles · Settings · Audit log · **Contractor/referral sources and commission** [CLIENT-DECISION CD-26].
All financial data Admin-only [CLIENT-DECISION CD-25]. Necessity ratings: `project-context/MODULES.md`.

### 2.3 Non-functional
Security controls, tested backup/restore with encrypted off-site copies, documentation set,
installation on XAMPP and cPanel, fictitious sample data.

## 3. Out of scope (unless the client requests and approves a change)
- Construction execution, contracting, material procurement/resale, turnkey interiors.
- **Payments to construction contractors or vendors**, labour/payroll, inventory.
  (Recording contractor/referral **commission** paid by the studio **is in scope** — CD-26.)
- GST return filing, accounting ledger, Tally integration.
- Online payment gateway, client portal, native mobile apps, SMS/WhatsApp API automation.
- Professional photography; content beyond the agreed website pages.
- Domain purchase, hosting purchase, business email set-up (advice only).
- Historical data migration (unless supplied as spreadsheets — Q-G10).
- Any use of `reference/portfolio/Senior office profile.pdf` content (another architect's work) on the website.

## 4. Assumptions [ASSUMPTION]
- Small team (1–5 ERP users); single office.
- INR only; Indian number format; DD/MM/YYYY; FY April–March.
- English website and ERP for v1; Marathi optional.
- The studio pays commission to the partner (A7, Q-C1).
- The client supplies original photos and project facts, publishing consent, final service list
  and quotation terms; CodInt drafts text for client review.
- Hosting supports PHP 8.1+, MySQL/MariaDB, HTTPS, cron, GD, mbstring, bcmath, `finfo`, folders outside `public_html`.

## 5. Pending client decisions
Full list: `docs/CLIENT_QUESTIONS.md` §10. Highest impact:
1. Commission rules — direction, base, timing, tax (Q-C1…Q-C4).
2. GST registration status (Q-F3).
3. Limits of "Admin-only finance" for staff (Q-U4) and the actual users (Q-U1).
4. Portfolio photos and "major" projects (Q-W1); purpose of the non-AJ profile PDF (Q-G11).
5. Services: meaning of Instagram categories (Q-S2); demo services in public (Q-S5).
6. Domain spelling (Q-H1) and hosting plan (Q-H2).

## 6. Acceptance (proposed)
Each stage gate in `project-context/DEVELOPMENT_ROADMAP.md` is accepted in writing and logged.
Final acceptance: running application on production hosting, documents delivered, backup/restore
demonstrated, final ZIP handed over.
