# Project Overview — AJ Design Studio Portfolio Website + ERP

Status tags: **CONFIRMED-REF · CLIENT-DECISION · BRIEF · PROPOSED · ASSUMPTION · PENDING**
(definitions in `CLAUDE.md` §3). Question IDs (`Q-…`) refer to `docs/CLIENT_QUESTIONS.md`.
Last updated: 2026-11-06 · Stage 1 approved 2026-11-06.

## 1. Summary

AJ Design Studio is an architecture and interior design practice led by
Ar. Ajit Kumbhar. The studio **has no website today** [BRIEF]. CodInt Digitech will build,
on one hosting account and the domain `ajdesignstudios.in` [CLIENT-DECISION]:

1. A new **public portfolio website** at `/`.
2. A **private ERP** at `/erp/` for running the studio's office work
   (enquiries → quotations → projects → fees → payments → commission → reports).

The ERP is also the content-management back office for the website's portfolio.

## 2. Stakeholders

| Role | Name / Org | Status |
|---|---|---|
| Client | AJ Design Studio | CONFIRMED-REF |
| Principal Architect, business owner, decision maker and main Admin user | Ar. Ajit Kumbhar | CONFIRMED-REF (name) · CLIENT-DECISION CD-29 (owner, authority, main Admin) |
| Developer | CodInt Digitech | BRIEF |
| ERP users other than the principal | None for now (CD-80); staff roles prepared for later, without financial access (CD-25, CD-83) | CLIENT-DECISION |
| Contractors / referral sources | Bring some projects; may earn commission | CLIENT-DECISION |
| Website visitors | Prospective clients, public | BRIEF |

## 3. Facts gathered from references

### 3.1 Organization details [CONFIRMED-REF]
| Item | Value | Source |
|---|---|---|
| Name | AJ Design Studio | Logo, quotation, visiting card, Instagram |
| Profession | Architect & Interior Designer | Quotation, visiting card, Instagram |
| Principal | Ar. Ajit Arjun Kumbhar | Visiting card, Instagram |
| Address | **Sai Arcade Building**, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan (visiting card spells "Arked") | CLIENT-DECISION CD-45 |
| Area line | Patan, Karad, Satara | Instagram |
| Phones | 8806956877 — WhatsApp and the only published number; 7796877369 on the card, not published | CLIENT-DECISION CD-46 |
| Email | ar.ajitkumbhar16@gmail.com | Quotation, visiting card, Instagram |
| Instagram | @ar.ajkumbhar (display name "AJ DESIGN STUDIO") | Instagram, QR on visiting card |

Contact details come from Instagram and the reference documents [CLIENT-DECISION CD-12]; the address
spelling and the published number are settled (CD-45, CD-46).

### 3.2 Instagram (public, without login, checked 2026-11-06)
- Bio: "Architect & Interior Designer", email, phone, "Patan, Karad, Satara".
- Highlight titles: *Bunglow Project, Temple Work, कोकण शिल्प, Mini Bunglow, Complete Project,
  Interior Site*.
- Posts and images could not be read without login. The client wants website content based on
  this presence [CLIENT-DECISION]; the client will send original photos (CD-43).

### 3.3 Logo and visiting card
- `reference/logo/Logo.jpeg`, 1600×1034 JPEG, no transparency.
- `reference/Visiting Card.jpeg`: front = monogram + letter-spaced "Design Studio" on charcoal;
  back = copper background with name, title, phones, address, email, Instagram QR.

### 3.4 Sample quotation
- 2-page dummy, `Ref: 1/2025`, 15/12/2025, area-based fee 1100 sq.ft × ₹100 = ₹1,10,000.
  Reference only. Analysis: `docs/QUOTATION_ANALYSIS.md`.

### 3.5 Other material in the folder
- `reference/portfolio/Senior office profile.pdf` — profile of **another architect** (Bhushan
  Chakote, Pune). **Not AJ Design Studio content; must never be published as AJ's work.**
  Client confirmed it was a sample only and is not to be used (CD-39).
- `reference/portfolio/` has **no AJ project photos** yet; the client sends originals and marks major projects (CD-43, CD-97).
- `reference/WorkLedger/…zip` — earlier CodInt app; coding-style reference only (D-19).

## 4. Goals

| # | Goal | Status |
|---|---|---|
| G1 | Premium, formal online presence with a portfolio | BRIEF + CLIENT-DECISION (tone) |
| G2 | Capture enquiries from the website (form + WhatsApp) | BRIEF |
| G3 | Manage enquiries, clients and projects in one place | BRIEF |
| G4 | Consistent, professional quotations with revisions/approval | BRIEF + CLIENT-DECISION (format) |
| G5 | Track fees, payments (staged, partial, advances) and expenses per project | CLIENT-DECISION (payments) / PROPOSED (expenses) |
| G6 | Store project documents privately | PROPOSED |
| G7 | Let the studio update the website without a developer | BRIEF |
| G8 | Track direct vs contractor-sourced projects and contractor commission | CLIENT-DECISION |

## 5. Constraints

- Core PHP + MySQL/MariaDB + Bootstrap 5, no heavy frameworks [BRIEF].
- XAMPP for development; production on Hostinger shared hosting (hPanel) [CLIENT-DECISION CD-91], kept portable to cPanel [BRIEF].
- Website and ERP on the same hosting account and domain [CLIENT-DECISION].
- Hosting: Hostinger, plan 10 GB+ with the latest PHP/MySQL [CLIENT-DECISION CD-86, CD-91].
- Budget/timeline not supplied [PENDING].

## 6. Key assumptions and validated items

Full register: `docs/STAGE1_ROADMAP_AND_DECISIONS.md` §4.3.

- A1: Only the Admin uses the ERP for now. [CLIENT-DECISION CD-80]
- A2: Currency **INR only** [CLIENT-DECISION CD-27]; Indian number formatting (1,10,000) [PROPOSED].
- A3: Area unit sq.ft by default, sq.m possible [ASSUMPTION]; all area bases selectable [CLIENT-DECISION CD-54].
- A4: Website and printed documents in English and Marathi; ERP in English. [CLIENT-DECISION CD-50]
- A5: **Single office for now** [CLIENT-DECISION CD-28]; multi-branch out of scope.
- A6: Design and supervision services only, no construction. [CLIENT-DECISION CD-40]
- A7: Commission is paid **by** the studio **to** one contractor/referral partner per project. [CLIENT-DECISION CD-70]
- A8: Ar. Ajit Kumbhar is the business owner, decision authority and main Admin user. [CLIENT-DECISION CD-29]
- A10: Operations mainly within Maharashtra; time zone Asia/Kolkata (IST). [CLIENT-DECISION CD-30]

## 7. Where things stand

Stage 0 was accepted and Stage 1 (architecture and database design) was approved on 2026-11-06
(decision log in `project-context/DEVELOPMENT_ROADMAP.md`). Client decisions CD-01…CD-97 are
recorded in `docs/CLIENT_QUESTIONS.md`; the client's signature of `docs/CLIENT_DECISION_SUMMARY.md`
is pending. Next: Stage 2 — Foundation.
