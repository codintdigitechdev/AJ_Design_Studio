
# PROJECT: AJ DESIGN STUDIO
## Public Portfolio Website + Private ERP System

| | |
|---|---|
| Developer | CodInt Digitech |
| Client organization | AJ Design Studio |
| Principal Architect | Ar. Ajit Kumbhar (Instagram profile shows "Ar. Ajit Arjun Kumbhar") |
| Current stage | **Stage 0 – Documentation & requirements (awaiting client/developer approval)** |
| Last updated | 2026-11-06 |

> **GATE:** Do not start implementation (PHP code, `database.sql`, `sample_data.sql`,
> UI pages, ERP modules) until requirements, architecture and database design have
> been reviewed and approved. Current approval status is tracked in
> `project-context/DEVELOPMENT_ROADMAP.md`.

---

## 1. PROJECT VISION

One integrated web application, deployed on **one hosting account and one domain**,
with two independent user experiences:

**A. Public portfolio website** (new — the client has **no existing website**)
- Open to everyone, no login. Premium architecture/interior portfolio.
- Projects, services, galleries, contact, enquiry form, WhatsApp enquiry.
- Responsive, SEO-friendly. Content managed from the ERP.

**B. Private ERP**
- Separate secure login, authorized organization users only.
- Enquiries, clients, projects, quotations, fees, payments, expenses,
  documents, follow-ups, reports, users/roles, settings, portfolio CMS.
- Public visitors must never reach ERP data, files or configuration.

URL structure (domain to be configured later):

| Area | URL |
|---|---|
| Public website | `https://<domain>/` |
| ERP root | `https://<domain>/erp/` |
| ERP login | `https://<domain>/erp/login` |
| ERP dashboard | `https://<domain>/erp/dashboard` |

How both run on the same hosting account: see `docs/TECHNICAL_REQUIREMENTS.md` §2.

## 2. DOCUMENT MAP (read before working)

| File | Purpose |
|---|---|
| `project-context/PROJECT_OVERVIEW.md` | Facts, stakeholders, confirmed vs. assumed |
| `project-context/BUSINESS_REQUIREMENTS.md` | Business requirements with status tags |
| `project-context/MODULES.md` | Proposed ERP + website module specifications |
| `project-context/DATABASE_RULES.md` | Schema conventions, money, soft delete, audit |
| `project-context/SECURITY_RULES.md` | Mandatory security controls |
| `project-context/UI_UX_GUIDELINES.md` | Brand, colours, typography, layout rules |
| `project-context/DEVELOPMENT_ROADMAP.md` | Stages, approval gates, decision log |
| `docs/PROJECT_SCOPE.md` | In scope / out of scope / pending |
| `docs/QUOTATION_ANALYSIS.md` | Analysis of the sample quotation |
| `docs/CLIENT_QUESTIONS.md` | Open questions for the client (master list) |
| `docs/PORTFOLIO_WEBSITE_PLAN.md` | Public website sitemap and page plans |
| `docs/TECHNICAL_REQUIREMENTS.md` | Stack, hosting layout, folder structure, deployment |

## 3. STATUS TAGS (use consistently in every document)

- **[CONFIRMED]** – stated in a supplied reference (logo, sample quotation, public Instagram profile) or by the developer brief.
- **[PROPOSED]** – our recommendation; needs approval.
- **[ASSUMPTION]** – working assumption; must be validated.
- **[PENDING]** – client decision required; see `docs/CLIENT_QUESTIONS.md`.

Never upgrade a tag to CONFIRMED without a written client/developer decision
recorded in the decision log (`project-context/DEVELOPMENT_ROADMAP.md` §5).

## 4. REFERENCE MATERIAL (actual file names on disk)

| Reference | Actual path | Notes |
|---|---|---|
| Logo | `reference/logo/Logo.jpeg` | 1600×1034 JPEG, opaque charcoal background. Brief calls it `AJ_Design_Studio_Logo.jpeg`; file was **not renamed**. |
| Sample quotation | `reference/quotation-samples/work pfd & fees structure.pdf` | 2 pages, dummy/sample. Brief calls it `work_pfd_fees_structure.pdf`. |
| Portfolio images | `reference/portfolio/` | **Empty.** No project photos supplied yet. |
| WorkLedger | `reference/WorkLedger/WorkLedger_Multilingual_EN_HI_MR.zip` | Earlier CodInt Digitech PHP app (staff work/wages, EN/HI/MR). Not mentioned in the brief; treated only as a possible coding-style reference. Do not copy its default passwords or `fix_login.php` pattern. |
| Instagram | https://www.instagram.com/ar.ajkumbhar | Public profile header only (posts need login). |

Do not modify, rename or delete anything under `reference/`.

## 5. BRAND IDENTITY

- Logo: copper triangular "AJ" monogram above "DESIGN STUDIO" in bold condensed
  capitals, on charcoal grey, with a decorative copper dot column on the left.
- Sampled colours (from the JPEG, approximate): charcoal `#54545C`, copper `#AF7B4C`,
  secondary tan accent `#A78A5E`.
- Direction: charcoal grey + copper/bronze, light neutral backgrounds, premium
  architectural presentation, clean typography, elegant galleries.
- **Do not replace, redraw, recolour or distort the logo.** Derivatives (header,
  ERP sidebar, login, favicon) are crops/resizes of the supplied file only.
  A vector/transparent original has been requested from the client.
- Details: `project-context/UI_UX_GUIDELINES.md`.

## 6. BUSINESS PROFILE (confirmed facts only)

From the sample quotation letterhead and the public Instagram profile:
- AJ Design Studio — **Architect, Interior Designer**.
- Address on letterhead: Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan.
- Instagram location line: Patan, Karad, Satara.
- Contact on both: 8806956877, ar.ajitkumbhar16@gmail.com.
- Reference work categories from the quotation: floor plans, working drawings
  (sections, elevations, municipal drawing), exterior 3D, interior design layouts,
  interior 3D, construction-stage site visits, material & colour selection.
- Instagram highlight titles (labels only, not confirmed services): Bunglow Project,
  Temple Work, कोकण शिल्प, Mini Bunglow, Complete Project, Interior Site.

Do **not** assume construction execution, contracting, material procurement,
turnkey work or any other service without written approval. Do not publish
contact details, project names or client names on the website until approved.

## 7. QUOTATION RULES

The sample (`Ref 1/2025`, 1100 sq.ft × ₹100/sq.ft = ₹1,10,000) is a **dummy**.
- Never hardcode ₹100/sq.ft, the area, or the total.
- Do not assume GST, payment schedule, discounts, terms, validity, extra-visit
  charges or revision limits. All are configurable and pending approval.
- Proposed calculation methods: area-based, fixed fee, item-wise, custom charges.
- Required capabilities: PDF + print, revision history, approval status.
- Full analysis: `docs/QUOTATION_ANALYSIS.md`.

## 8. TECHNICAL STACK

Core PHP (8.1+ proposed) · MySQL/MariaDB · PDO prepared statements · Bootstrap 5 ·
HTML5/CSS3/vanilla JS · AJAX where useful · XAMPP for development · cPanel deployment.
Avoid frameworks and unnecessary dependencies. Modular PHP. Details and the
proposed folder layout: `docs/TECHNICAL_REQUIREMENTS.md`.

## 9. SECURITY AND DATA RULES (summary — full text in `project-context/SECURITY_RULES.md`)

- `password_hash()`/`password_verify()`; role-based authorization on every ERP request.
- CSRF token on every state-changing request; server-side validation always.
- PDO prepared statements only; no string-built SQL with user input.
- Application code, config, private documents and backups live **outside the web root**.
- Uploads: whitelist + MIME sniffing, random file names, no script execution in upload dirs.
- Separate ERP session cookie (path `/erp`, HttpOnly, Secure, SameSite).
- Audit log for important business operations.
- Soft delete for ordinary master records; financial transactions are never silently
  overwritten — use corrections/reversals. DECIMAL for money, area and rates.

## 10. DEVELOPMENT RULES

- Inspect existing files before changing them; do not delete existing files.
- Keep documentation, schema and SQL scripts synchronized.
- No duplicate files. Build and test module by module.
- Never claim tests passed unless actually executed (PHP/MySQL are not on the
  shell PATH of this machine; XAMPP location to be confirmed).
- Do not invent client requirements, services, projects or company claims.
- Record unresolved decisions in `docs/CLIENT_QUESTIONS.md` and the decision log.
- The project folder is **not yet a Git repository**; initialise Git at the start of
  Stage 1 and commit at each milestone.

## 11. FINAL DELIVERABLE

Complete running application: public website, ERP, full PHP source, `database.sql`,
`sample_data.sql` (fictitious data only), assets/branding, installation guide, user
guide, testing documentation, deployment instructions, backup & restore instructions.

Final ZIP: `AJ_Design_Studio_Portfolio_ERP.zip`
