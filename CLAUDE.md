
# PROJECT: AJ DESIGN STUDIO
## Public Portfolio Website + Private ERP System

| | |
|---|---|
| Developer | CodInt Digitech |
| Client organization | AJ Design Studio |
| Principal Architect | Ar. Ajit Kumbhar (Instagram profile and visiting card: "Ar. Ajit Arjun Kumbhar") |
| Repository | `https://github.com/codintdigitechdev/AJ_Design_Studio` — branch `main` is authoritative. The local folder `R:\CID\Clients\AJ_Design_Studio` is a working copy of it (synchronised 2026-11-06 at commit `12d7634`) |
| Current stage | **Stage 1 – Architecture & database design: documentation corrected, NOT APPROVED.** Stage 0 acceptance is not yet recorded (D-03) |
| Last updated | 2026-11-06 |

> **GATE:** Do not start implementation (PHP code, `database.sql`, `sample_data.sql`,
> UI pages, ERP modules) until requirements, architecture and database design have
> been reviewed and approved. Approval status is tracked in
> `project-context/DEVELOPMENT_ROADMAP.md` §5 (decision log) and
> `docs/STAGE1_ROADMAP_AND_DECISIONS.md`.
>
> **Git:** never commit or push without the developer's explicit permission.

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
- Enquiries, clients, projects, contractor/referral sources and commission, quotations,
  fees, payments, expenses, documents, follow-ups, reports, users/roles, settings,
  portfolio CMS.
- Public visitors must never reach ERP data, files or configuration.

URL structure — domain `ajdesignstudios.in` **[CLIENT-DECISION CD-01; spelling confirmed CD-85]**:

| Area | URL |
|---|---|
| Public website | `https://ajdesignstudios.in/` |
| ERP root | `https://ajdesignstudios.in/erp/` |
| ERP login | `https://ajdesignstudios.in/erp/login` |
| ERP dashboard | `https://ajdesignstudios.in/erp/dashboard` |

Configuration files and examples use the placeholder `<domain>`. How both run on the same
hosting account: `docs/TECHNICAL_REQUIREMENTS.md` §2.

## 2. DOCUMENT MAP (read before working)

### 2.1 Project context (rules and requirements)
| File | Purpose |
|---|---|
| `project-context/PROJECT_OVERVIEW.md` | Facts, stakeholders, reference material, assumptions |
| `project-context/BUSINESS_REQUIREMENTS.md` | Business requirements with status tags, incl. Admin-only finance (E-21) and commission (E-22…E-24) |
| `project-context/MODULES.md` | Website and ERP module specifications |
| `project-context/DATABASE_RULES.md` | Schema conventions, money, soft delete, financial integrity, audit, backups |
| `project-context/SECURITY_RULES.md` | Mandatory security controls, incl. financial-data filtering |
| `project-context/UI_UX_GUIDELINES.md` | Brand, colours, typography, tone, layout rules |
| `project-context/DEVELOPMENT_ROADMAP.md` | Stages, approval gates, **decision log** |

### 2.2 Planning and Stage 1 design (current)
| File | Purpose |
|---|---|
| `docs/PROJECT_SCOPE.md` | In scope / out of scope / pending |
| `docs/QUOTATION_ANALYSIS.md` | Analysis of the sample quotation; quotation model |
| `docs/CLIENT_QUESTIONS.md` | **Master list** of client questions and recorded client decisions |
| `docs/PORTFOLIO_WEBSITE_PLAN.md` | Public website sitemap, content, publishing workflow |
| `docs/TECHNICAL_REQUIREMENTS.md` | Stack, hosting layout, folder structure, deployment, backups |
| `docs/DATABASE_DESIGN.md` | ER diagram and table-by-table design |
| `docs/WORKFLOWS.md` | Enquiry → project → quotation, financial and commission workflows |
| `docs/PERMISSION_MATRIX.md` | Role × module permissions and record-level rules |
| `docs/ERP_PAGES_AND_FIELDS.md` | ERP URL map and field specifications |
| `docs/WIREFRAMES.md` | Text wireframes for website and ERP |
| `docs/STAGE1_ROADMAP_AND_DECISIONS.md` | Stage plan and **register of every open decision** |

### 2.3 Stage 1 audit and correction records
| File | Purpose |
|---|---|
| `docs/STAGE1_CONSOLIDATED_CORRECTION_REPORT.md` | Audit findings that drove the correction (historical; issue IDs are referenced elsewhere) |
| `docs/STAGE1_CORRECTION_TRACKING_MATRIX.md` | Every audit item, its status, affected files and resolution |
| `docs/STAGE1_DOCUMENTATION_CONSISTENCY_REPORT.md` | Final cross-document consistency check |
| `docs/STAGE1_GAP_RESOLUTION.md` | Errata C-01…C-18 and R-01…R-08 (now applied — see its banner) |

### 2.4 Superseded (kept for history only — do not use as a reference)
| File | Superseded by |
|---|---|
| `docs/STAGE1_REVIEW_PACKAGE.md` | The current documents above |
| `docs/STAGE1_REVIEW_PACKAGENew.md` | The current documents above |

## 3. STATUS TAGS (use exactly these in every document)

| Tag | Meaning | Usable as a design basis? |
|---|---|---|
| **CONFIRMED-REF** | Stated in a reference file on disk (logo, sample quotation, visiting card, public Instagram profile) | Yes |
| **CLIENT-DECISION** | A decision of the client. Each one is listed with date and source in `docs/CLIENT_QUESTIONS.md` §0 and the decision log | Yes |
| **BRIEF** | Required by the developer brief (not on disk); developer may re-affirm or change it | Yes, provisionally |
| **PROPOSED** | Developer recommendation; needs approval | Only as a draft |
| **ASSUMPTION** | Working assumption; must be validated | Only as a draft |
| **PENDING** | A client or developer decision is required; the question ID says which | No — document the impact instead |

Rules:
- Never turn PENDING, PROPOSED or ASSUMPTION into CLIENT-DECISION without a written record
  (date, source) in the decision log.
- A design that implements a client decision is still **PROPOSED** until the developer
  approves it.
- Older documents may show legacy wording (`[CONFIRMED]`, "CONFIRMED (brief)", "PENDING APPROVAL").
  Read them as CONFIRMED-REF, BRIEF and PENDING respectively.

## 4. REFERENCE MATERIAL (actual file names on disk)

| Reference | Actual path | Notes |
|---|---|---|
| Logo | `reference/logo/Logo.jpeg` | 1600×1034 JPEG, opaque charcoal background. Brief calls it `AJ_Design_Studio_Logo.jpeg`; not renamed |
| Visiting card | `reference/Visiting Card.jpeg` | Front: logo with letter-spaced "Design Studio" wordmark on charcoal. Back (copper): "Ar. Ajit Arjun Kumbhar, Architect & Interior Designer", phones **8806956877 / 7796877369**, address "AJ Design Studio, Sai **Arked** Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan", email, Instagram QR code. Client-named reference for contacts and quotation design |
| Sample quotation | `reference/quotation-samples/work pfd & fees structure.pdf` | 2 pages, dummy/sample (address spelled "Sai **Arcade** Building") |
| Senior office profile | `reference/portfolio/Senior office profile.pdf` | 4-page "Architectural Profile" of **another architect (Bhushan Chakote, Kothrud, Pune)**. **Not AJ Design Studio content.** Its projects, awards and text must never be used as AJ's work. Client confirmed: sample only, **do not use** (CD-39) |
| WorkLedger | `reference/WorkLedger/WorkLedger_Multilingual_EN_HI_MR.zip` | Earlier CodInt Digitech PHP app. Possible coding-style reference only. Do not copy its default passwords or `fix_login.php` pattern |
| Instagram | https://www.instagram.com/ar.ajkumbhar | Public profile header only (posts need login) |

`reference/portfolio/` contains **no AJ Design Studio project photos** yet (the client will send originals — CD-43).
Do not modify, rename or delete anything under `reference/`.

## 5. BRAND IDENTITY

- Logo: copper triangular "AJ" monogram above "DESIGN STUDIO", charcoal background, decorative
  copper dot column. The visiting card shows the same monogram with a lighter, letter-spaced
  "Design Studio" wordmark and a copper reverse side.
- Sampled colours (approximate): charcoal `#54545C`, copper `#AF7B4C`, tan `#A78A5E` **[CONFIRMED-REF]**.
- **Do not replace, redraw, recolour or distort the logo.** Derivatives are crops/resizes of the
  supplied files only; the client chose to use them as given (CD-51). Headings follow the visiting card's
  Copperplate Gothic style (CD-51).
- Website tone: **professional, formal and ethical** **[CLIENT-DECISION]** — no unverifiable
  claims, no invented numbers, awards or testimonials.
- Details: `project-context/UI_UX_GUIDELINES.md`.

## 6. BUSINESS PROFILE

Confirmed facts **[CONFIRMED-REF]** (quotation letterhead, visiting card, Instagram):
- AJ Design Studio — Architect & Interior Designer.
- Address: **Sai Arcade Building** (CD-45), Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan. Instagram area line: Patan, Karad, Satara.
- Phone/WhatsApp 8806956877 — the only published number (CD-46); 7796877369 on the card, not
  published; email ar.ajitkumbhar16@gmail.com.
- Reference work categories (sample quotation): floor plans, working drawings (sections,
  elevations, municipal drawing), exterior 3D, interior design layouts, interior 3D,
  construction-stage site visits, material & colour selection.
- Instagram highlight titles (labels only): Bunglow Project, Temple Work, कोकण शिल्प,
  Mini Bunglow, Complete Project, Interior Site.

Client decisions (2026-11-06) **[CLIENT-DECISION]** — full list `docs/CLIENT_QUESTIONS.md` §0:
- Projects arrive **directly** or **through contractors/referral sources**; commission may
  apply to the latter, only when applicable and approved, Admin-only.
- Use suitable **demo** services initially; Admin manages services (add/update/soft-delete).
- Website content is drafted from the Instagram presence and reference documents; the client
  reviews it later. Contact details come from Instagram and the reference documents.
- All major projects and available photographs may be included; projects can be removed later.
- Design and supervision only (CD-40); only the Admin uses the ERP for now (CD-80); website and ERP
  delivered together (CD-37); public website and printed documents in English and Marathi (CD-50).

Out of scope by client decision: construction execution, contracting, material procurement, turnkey
work (CD-40). Contractor *commission* is in scope; paying construction contractors is not.
Nothing private about a client is published without approval; client names only with permission (CD-47).

## 7. QUOTATION AND FINANCE RULES

- The sample (`Ref 1/2025`, 1100 sq.ft × ₹100/sq.ft = ₹1,10,000) is a **dummy**. Never hardcode
  the rate, area or total.
- Area-based and item-wise quotations are supported; fixed pricing is never mandatory; the Admin
  can modify rates **[CLIENT-DECISION]**.
- Quotation format uses the logo and the visiting-card reference **[CLIENT-DECISION]**;
  quotation number `AJDS/Q/{fy}/{seq3}` **[CLIENT-DECISION CD-52]**.
- Billing is flexible, not agreement-only; staged and **partial payments are always allowed**;
  advances and allocations must be handled correctly **[CLIENT-DECISION]**.
  Design: per-project billing method (PROPOSED, D-26).
- **GST is optional and configurable, never compulsory for a quotation or project**
  **[CLIENT-DECISION]**. Design: per-document "Apply GST" (PROPOSED, D-27). The studio is **not GST-registered** today
  (CD-60), so GST stays off.
- Discount max 5% (CD-61); stages as % of total incl. GST (CD-59); all standard term sections drafted by
  CodInt for client review (CD-56); extra charges billed separately (CD-62); refunds with % deduction and
  Admin-only write-offs (CD-66, CD-67); no credit transfer between projects (CD-68).
- Full analysis: `docs/QUOTATION_ANALYSIS.md`; workflows: `docs/WORKFLOWS.md`.

## 8. TECHNICAL STACK

Core PHP (8.1+ proposed) · MySQL/MariaDB · PDO prepared statements · Bootstrap 5 ·
HTML5/CSS3/vanilla JS · AJAX where useful · XAMPP for development · cPanel deployment.
Avoid frameworks and unnecessary dependencies. Details: `docs/TECHNICAL_REQUIREMENTS.md`.

## 9. SECURITY AND DATA RULES (summary — full text in `project-context/SECURITY_RULES.md`)

- **Financial information and financial decisions are Admin-only** **[CLIENT-DECISION]** —
  on every page, report, dashboard, export, PDF, API/AJAX response, notification and activity
  timeline. Non-Admin roles receive no financial fields from the server. The definition of
  "financial data" is in `BUSINESS_REQUIREMENTS.md` E-21.
- `password_hash()`/`password_verify()`; role-based authorization on every ERP request.
- CSRF token on every state-changing request; server-side validation always.
- PDO prepared statements only.
- Application code, config, private documents, portfolio originals and backups live **outside
  the web root**.
- Uploads: whitelist + MIME sniffing, random file names, no script execution in upload dirs.
- Separate ERP session cookie (path `/erp`, HttpOnly, Secure, SameSite).
- Audit log for important business operations, including every financial and commission action.
- Soft delete for ordinary master records; financial transactions (incl. commission) are never
  silently overwritten — corrections/reversals only. DECIMAL for money, area and rates.

## 10. DEVELOPMENT RULES

- Inspect existing files before changing them; do not delete existing files.
- Keep documentation, schema and SQL scripts synchronized.
- No duplicate files. Build and test module by module.
- Never claim tests passed unless actually executed (PHP/MySQL are not on the shell PATH of this
  machine; XAMPP location to be confirmed).
- Do not invent client requirements, services, projects or company claims.
- Record unresolved decisions in `docs/CLIENT_QUESTIONS.md` and
  `docs/STAGE1_ROADMAP_AND_DECISIONS.md`; record decisions in the decision log.
- Git: the folder is a working copy of GitHub `main`. Commit or push only with explicit permission.

## 11. FINAL DELIVERABLE

Complete running application: public website, ERP, full PHP source, `database.sql`,
`sample_data.sql` (fictitious data only), assets/branding, installation guide, user
guide, testing documentation, deployment instructions, backup & restore instructions.

Final ZIP: `AJ_Design_Studio_Portfolio_ERP.zip`
