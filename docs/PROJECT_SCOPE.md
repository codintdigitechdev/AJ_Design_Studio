# Project Scope

Project: AJ Design Studio – Portfolio Website + ERP Management System
Developer: CodInt Digitech · Client: AJ Design Studio · Principal Architect: Ar. Ajit Kumbhar
Version: 0.1 draft (2026-11-06) – **not approved**

## 1. Confirmed information
- The client has **no existing website**; a new public portfolio website will be built. (brief)
- A private ERP will be built; both on the **same hosting account and domain**:
  `/` public, `/erp/` ERP, `/erp/login` login. Domain to be configured later. (brief)
- Stack: Core PHP, MySQL/MariaDB, PDO, Bootstrap 5, HTML5/CSS3/JS, AJAX where required,
  XAMPP dev, cPanel deployment. (brief)
- Studio identity: Architect, Interior Designer; Patan (Karad–Chiplun Road), Satara district;
  phone 8806956877; email ar.ajitkumbhar16@gmail.com. (quotation letterhead, Instagram)
- Reference work categories (from sample quotation): floor plans, working drawings,
  municipal drawings, exterior 3D, interior design layouts, interior 3D, construction-stage
  site visits, material and colour selection.
- Sample quotation is a **dummy**, not the final template or pricing policy. (brief)
- Final deliverable list and ZIP name. (brief)

## 2. In scope (proposed, subject to approval)

### 2.1 Public website
Home · About Studio · Services · Portfolio · Project Details · Gallery · Contact · Enquiry form ·
WhatsApp enquiry · SEO (meta, sitemap, schema) · responsive design · content from ERP.

### 2.2 ERP
Dashboard · Enquiries (incl. website) · Clients · Projects (+ site-visit log) · Services &
work categories · Quotations (configurable, revisions, approval, PDF/print) · Fees & billing ·
Payments & receipts · Expenses · Project documents (private) · Portfolio & gallery CMS ·
Follow-ups & reminders · Reports · Users & roles · Organization settings · Audit log.
Module necessity ratings: `project-context/MODULES.md`.

### 2.3 Non-functional
Security controls (`project-context/SECURITY_RULES.md`), backups and restore, documentation set,
installation on XAMPP and cPanel, sample data (fictitious).

## 3. Out of scope (unless the client requests and approves a change)
- Construction execution, contracting, material procurement/resale, vendor/contractor
  billing, labour/payroll, inventory.
- GST return filing / accounting ledger / Tally integration.
- Online payment gateway.
- Client login portal.
- Native mobile apps.
- SMS/WhatsApp Business API automation.
- Content writing and professional photography (client supplies texts and photos; we can
  structure and proof-read).
- Domain purchase, hosting purchase, business email setup (we can advise).
- Migration of historical data (unless provided as spreadsheets — Q-G10).

## 4. Assumptions
- Small team (1–5 ERP users); single office.
- INR only; Indian number format; dates DD/MM/YYYY; FY April–March.
- English website and ERP for v1; Marathi optional.
- The client provides: photos, project descriptions, approval to publish each project,
  final service list, about-studio text, quotation terms.
- Hosting supports PHP 8.1+, MySQL/MariaDB, HTTPS, cron, GD, mbstring, bcmath, `finfo`.

## 5. Pending client decisions
All tracked in `docs/CLIENT_QUESTIONS.md`. Highest priority:
1. Final service list and what "Temple Work", "कोकण शिल्प" and "Complete Project" mean for the website.
2. Fee/billing model (area rate vs fixed, stages, GST registration, receipts).
3. Users and roles.
4. Portfolio content availability and publishing consent.
5. Domain and hosting.
6. Website-first phased launch or everything together.

## 6. Acceptance (proposed)
Each stage gate in `project-context/DEVELOPMENT_ROADMAP.md` is accepted in writing.
Final acceptance: running application on production hosting, documents delivered,
backup/restore demonstrated, final ZIP handed over.
