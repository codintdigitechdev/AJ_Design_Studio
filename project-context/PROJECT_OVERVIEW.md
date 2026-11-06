# Project Overview — AJ Design Studio Portfolio Website + ERP

Status tags: **[CONFIRMED] [PROPOSED] [ASSUMPTION] [PENDING]** (see `CLAUDE.md` §3).
Last updated: 2026-11-06 · Stage 0 (documentation).

## 1. Summary

AJ Design Studio is an architecture and interior design practice led by
Ar. Ajit Kumbhar. The studio **has no website today** [CONFIRMED – developer brief].
CodInt Digitech will build, on one hosting account and one domain:

1. A new **public portfolio website** at `/`.
2. A **private ERP** at `/erp/` for running the studio's office work
   (enquiries → quotations → projects → fees → payments → reports).

The ERP is also the content-management back office for the website's portfolio.

## 2. Stakeholders

| Role | Name / Org | Status |
|---|---|---|
| Client | AJ Design Studio | CONFIRMED |
| Principal Architect / decision maker | Ar. Ajit Kumbhar | CONFIRMED (decision authority ASSUMPTION) |
| Developer | CodInt Digitech | CONFIRMED |
| ERP users other than the principal | Unknown (staff, accountant, site engineer?) | PENDING – Q-U1 |
| Website visitors | Prospective clients, public | CONFIRMED |

## 3. Facts gathered from references

### 3.1 Organization details [CONFIRMED]
| Item | Value | Source |
|---|---|---|
| Name | AJ Design Studio | Logo, quotation, Instagram |
| Profession | Architect, Interior Designer | Quotation letterhead, Instagram bio |
| Address | Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan | Quotation letterhead |
| Area line | Patan, Karad, Satara | Instagram bio |
| Phone | 8806956877 | Quotation, Instagram |
| Email | ar.ajitkumbhar16@gmail.com | Quotation, Instagram |
| Instagram | @ar.ajkumbhar (display name "AJ DESIGN STUDIO") | Instagram |

Whether these are the details to publish on the website (and whether the phone is
also the WhatsApp number) is **[PENDING – Q-W3, Q-W4]**.

### 3.2 Instagram (public, without login, checked 2026-11-06)
- Bio: "Architect & Interior Designer", email, phone, "Patan, Karad, Satara".
- Story-highlight titles: *Bunglow Project, Temple Work, कोकण शिल्प, Mini Bunglow,
  Complete Project, Interior Site*.
- Posts and images were not readable without login. **No project names, photos or
  descriptions have been taken from Instagram.** Highlight titles are recorded only
  as hints for questions (e.g. is temple work a service? what does "Complete Project" mean?).

### 3.3 Logo
- `reference/logo/Logo.jpeg`, 1600×1034 px JPEG, no transparency.
- Copper (~`#AF7B4C`) triangular "AJ" monogram, "DESIGN STUDIO" wordmark, charcoal
  (~`#54545C`) background, dotted column ornament on the left.

### 3.4 Sample quotation
- 2-page dummy quotation, `Ref: 1/2025`, dated 15/12/2025, for a bungalow project
  at Karad, area-based fee 1100 sq.ft × ₹100 = ₹1,10,000. Treated as **reference only**.
- Full analysis: `docs/QUOTATION_ANALYSIS.md`.

### 3.5 Other material in the folder
- `reference/portfolio/` is empty — **no portfolio photos supplied yet**.
- `reference/WorkLedger/…zip` — an earlier CodInt Digitech PHP/MySQL app (staff,
  work entries, wages, payments, EN/HI/MR translations). Not referenced in the brief.
  Possible use: house coding style and multilingual approach. **[PENDING – Q-G3]**

## 4. Goals

| # | Goal | Status |
|---|---|---|
| G1 | Establish a premium online presence with a portfolio | CONFIRMED |
| G2 | Capture enquiries from the website (form + WhatsApp) | CONFIRMED |
| G3 | Manage enquiries, clients and projects in one place | CONFIRMED (brief) |
| G4 | Produce consistent, professional quotations with revisions/approval | CONFIRMED (brief) |
| G5 | Track fees billed, payments received and expenses per project | PROPOSED |
| G6 | Store project documents privately | PROPOSED |
| G7 | Let the studio update the website without a developer | CONFIRMED (brief) |

## 5. Constraints

- Core PHP + MySQL/MariaDB + Bootstrap 5, no heavy frameworks [CONFIRMED].
- XAMPP for development, cPanel shared hosting for production [CONFIRMED].
- Website and ERP on the same hosting account and domain [CONFIRMED].
- Domain and hosting provider not yet chosen [PENDING – Q-H1, Q-H2].
- Budget/timeline not supplied [PENDING].

## 6. Key assumptions (to validate)

- A1: The studio is small (1–5 ERP users). [ASSUMPTION]
- A2: Currency is INR only; Indian number formatting (1,10,000). [ASSUMPTION]
- A3: Area unit is sq.ft by default, possibly sq.m too. [ASSUMPTION]
- A4: English is the website language; Marathi may be wanted. [ASSUMPTION → Q-W8]
- A5: Single office/branch. [ASSUMPTION]
- A6: The studio provides design and supervision services, not construction. [ASSUMPTION → Q-S2]

## 7. Where things stand

Stage 0 documentation is complete and awaiting review. Next: client answers to
`docs/CLIENT_QUESTIONS.md`, then Stage 1 (architecture + database design for approval).
