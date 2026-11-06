# Client Questions and Client Decisions (master list)

For: Ar. Ajit Kumbhar, AJ Design Studio · Prepared by CodInt Digitech · first issued 2026-11-06 ·
corrected 2026-11-06. Tags: `CLAUDE.md` §3.

Priority: **P1** = needed before Stage 1 approval · **P2** = before the module is built · **P3** = can wait.
Status: **Open** · **Narrowed** (a client decision answers part of it) · **Answered** (by a CD below).
Answers become CLIENT-DECISION only when recorded here **and** in the decision log
(`project-context/DEVELOPMENT_ROADMAP.md` §5).

---

## 0. Client decisions received [CLIENT-DECISION]

**Date:** 2026-11-06. **Decided by:** Ar. Ajit Kumbhar. **Source:** collected by CodInt Digitech and
supplied in the developer's audit brief of 2026-11-06. **Written client confirmation (channel,
signed note or message) is still to be filed** — until then these are recorded as reported.

| ID | Decision | Questions affected |
|---|---|---|
| CD-01 | Domain selected: `ajdesignstudios.in` | Q-H1 |
| CD-02 | Public website and ERP on the same domain: website `/`, ERP `/erp/` | Q-H1 |
| CD-03 | Website content should be detailed and based on the client's Instagram presence | Q-W9, Q-W1 |
| CD-04 | Tone must be professional, formal and ethical | Q-W9 |
| CD-05 | Client will review website content later | Q-W9 |
| CD-06 | Initially use suitable demo services and service categories | Q-S1, Q-S4 |
| CD-07 | Admin must be able to add, update and soft-delete services and categories | Q-S1 |
| CD-08 | Include all major projects and available photographs | Q-W1 |
| CD-09 | Projects may be removed later if required | Q-W1, Q-W5 |
| CD-10 | Sensible display sequence; major projects get priority and can be highlighted | Q-W1 |
| CD-11 | Do not invent project details or publish private client information without appropriate approval | Q-W5 |
| CD-12 | Contact information from Instagram and existing reference documents; a visiting card may be provided later for verification; do not invent contact information | Q-W3, Q-W4 |
| CD-13 | Design a professional quotation format using the supplied logo and visiting-card reference | Q-Q2 |
| CD-14 | Developer may propose quotation numbering | Q-Q1 |
| CD-15 | Support area-based and item-wise quotations | Q-Q4, Q-Q5 |
| CD-16 | Do not make fixed pricing mandatory | Q-Q5 |
| CD-17 | Admin must be able to modify rates | Q-Q4 |
| CD-18 | Do not restrict to agreement-only billing; keep billing flexible | Q-F1 |
| CD-19 | GST optional and configurable | Q-F3 |
| CD-20 | GST not compulsory for every quotation or project | Q-F3 |
| CD-21 | Actual tax treatment must be confirmed appropriately | Q-F3 |
| CD-22 | Staged payments are supported | Q-F2 |
| CD-23 | Partial payments must always be allowed | Q-F2 |
| CD-24 | Advances and payment allocations must be handled correctly | Q-F2, Q-F11 |
| CD-25 | Financial information and financial decisions are Admin-only — everywhere | Q-U1 |
| CD-26 | Projects are Direct or via Contractor/referral source; commission (Yes/No; % or fixed; rate and amount; approval status; paid and outstanding; payment records and dates; remarks; audit history) only when applicable and approved; never automatic on direct projects; Admin-only | new Q-C1…Q-C6 |

**Second set — assumptions answered** (date 2026-11-06; entered by the developer in
`docs/STAGE1_ROADMAP_AND_DECISIONS.md` §4.3, commit `899ce73`; written client confirmation also still
to be filed):

| ID | Decision | Client answer (as entered) | Replaces |
|---|---|---|---|
| CD-27 | Currency is **INR only** | "Yes INR Only" | Assumption A2 |
| CD-28 | **Single office** for now | "Right now just single office only" | Assumption A5 |
| CD-29 | Ar. Ajit Kumbhar is the **business owner, decision authority and main Admin user** | "Yes he is business owner / Main Admin USer as well" | Assumption A8 |
| CD-30 | Operations are **mainly within Maharashtra**; time zone Asia/Kolkata (IST) | "Maharashtra (Mumbai) Not Much Outside Mh now" | Assumption A10 |

Notes: CD-28 and CD-30 describe the present ("right now", "now"); a later change would be a new
decision. CD-30 suggests most clients are in the same state as the studio, which matters for the
GST place-of-supply split — but the GST rule itself stays PENDING Q-F3.

**Third set — answers to the question list** (date 2026-11-06; source: the developer's answers typed into
the "Status / answer" column below, plus follow-up choices made in the development session the same day;
written client confirmation still to be filed). The typed answers are kept unchanged in the tables below.

| ID | Decision | Question |
|---|---|---|
| CD-31 | Website enquiries are kept as a **separate list** (inbox), distinct from manually entered enquiries | Q-G4 |
| CD-32 | Reminders on the **dashboard**, plus **emails for priority items** | Q-G5 |
| CD-33 | **No client portal** | Q-G6 |
| CD-34 | Non-converted enquiries are kept **until deleted**; Admin gets a **date-wise delete** option | Q-G7 |
| CD-35 | Financial year **April–March** | Q-G8 |
| CD-36 | Date format **DD/MM/YYYY** | Q-G8 |
| CD-37 | Website and ERP are delivered **together** (no website-first phase) | Q-G9 |
| CD-38 | **No existing data** to import | Q-G10 |
| CD-39 | `Senior office profile.pdf` was a sample only — **do not use it** (client considers its design poor) | Q-G11 |
| CD-40 | Studio does **design and supervision only** (no construction execution). Instagram labels (Temple Work, कोकण शिल्प, Complete Project…) are local descriptive terms for completed work | Q-S2 |
| CD-41 | Project types: **Architectural, Civil, Interior, Landscape** | Q-S3 |
| CD-42 | Demo services stay **inside the ERP**; the public site shows confirmed services only | Q-S5 |
| CD-43 | The client sends **original project photos** and details | Q-W1 |
| CD-44 | **Gallery merged into Portfolio** (no separate Gallery page) | Q-W2 |
| CD-45 | Address: **Sai Arcade Building**, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan | Q-W3 |
| CD-46 | **8806956877** is the WhatsApp number and the **only number published** on the website | Q-W4 |
| CD-47 | Client names appear on portfolio items **only with that client's permission** | Q-W5 |
| CD-48 | Enquiry emails go to the visiting-card email (ar.ajitkumbhar16@gmail.com); **simple built-in CAPTCHA**; emails are sent from a **domain mailbox** (e.g. noreply@ajdesignstudios.in) | Q-W6, Q-H5 |
| CD-49 | Testimonials only with permission; **Council of Architecture registration number** to be shown (number to be supplied) | Q-W7 |
| CD-50 | **English + Marathi** for the public website **and printed documents**; ERP screens in English | Q-W8 |
| CD-51 | Use the **given logo**; colours from the logo and visiting card; **visiting-card "Copperplate Gothic" style** headings (free look-alike) with a clean sans-serif body | Q-B1, Q-B2 |
| CD-52 | Quotation number **`AJDS/Q/{fy}/{seq3}`** (e.g. AJDS/Q/2026-27/001), revision shown as -R1, -R2 | Q-Q1 |
| CD-53 | Letterhead: logo + visiting card, **"श्री" kept**, **no Instagram QR** | Q-Q2 |
| CD-54 | **All area bases** selectable (built-up, carpet, plot, all floors) | Q-Q3 |
| CD-55 | Quotation includes an **acceptance block** (amount in words and client block not requested) | Q-Q6 |
| CD-56 | **All standard term sections** (validity, revisions, visits, extra charges, exclusions, cancellation, drawing ownership); **CodInt drafts the wording, client reviews** | Q-Q7 |
| CD-57 | Quotations are **downloaded and shared through WhatsApp**; no emailing from the ERP | Q-Q9 |
| CD-58 | Signature wording **"Ar. Ajit Kumbhar"** | Q-Q10 |
| CD-59 | Stage percentages are of the **total including GST** | Q-F2 |
| CD-60 | Studio is **not GST-registered** today; GST stays off until registration | Q-F3 |
| CD-61 | Discount **maximum 5%** | Q-F4 |
| CD-62 | **Extra charges billed separately** (visits, travel, printing) | Q-F5 |
| CD-63 | Receipts are **numbered** | Q-F6 |
| CD-64 | Payment modes: **Online, Cash, UPI** | Q-F7 |
| CD-65 | Expenses to track: **rent, travel and similar** | Q-F8 |
| CD-66 | **Refunds** can happen, with a **percentage deduction** | Q-F9 |
| CD-67 | **Write-offs** allowed, **Admin only** | Q-F10 |
| CD-68 | **No credit transfer** between projects | Q-F11 |
| CD-69 | **Advances before a project is opened** are possible | Q-F12 |
| CD-70 | The **studio pays** commission, to **one partner per project** | Q-C1 |
| CD-71 | **Referral** is a separate source from **Contractor** | Q-C2 |
| CD-72 | Commission percentage is of the **final fee excluding GST (incl. variations)**; **payable on completion**; changes in charges change it | Q-C3 |
| CD-73 | Tax on commission: **TDS to be decided later**; **GST may be involved** — keep it available | Q-C4 |
| CD-74 | Staff **may not** see partners, partner selection, source labels or source counts | Q-C5 |
| CD-75 | On cancellation or non-payment, **Admin decides** the commission each time; partner records kept **until removed** | Q-C6 |
| CD-76 | Project statuses: **Planned, OnGoing, OnHold, Completed, HandOver, Cancelled** | Q-P1 |
| CD-77 | Site visits are **logged, without limits** | Q-P3 |
| CD-78 | Pre-project meetings/site visits are **recorded on the enquiry** | Q-P4 |
| CD-79 | File types and sizes kept **to the minimum the server supports** | Q-D1 |
| CD-80 | **Only the Admin** uses the ERP for now (staff roles prepared for later) | Q-U1 |
| CD-81 | **Mobile use** allowed | Q-U2 |
| CD-82 | **No two-step login** | Q-U3 |
| CD-83 | Staff: **no** scope drafting, **no** sending, **no** expense claims | Q-U4 |
| CD-84 | **All proposed reports** are needed | Q-R1 |
| CD-85 | Domain spelling confirmed: **ajdesignstudios.in** | Q-H1 |
| CD-86 | Hosting not finalised; latest PHP/MySQL; plan a **10 GB or larger** hosting plan (500 MB is too small) | Q-H2 |
| CD-87 | A **password-protected staging copy** for client review before launch | Q-H3 |
| CD-88 | **CodInt Digitech** takes the weekly off-site backup | Q-H4 |
| CD-89 | Both workflow paths are used (quote first, or project first) | Q-G2 |
| CD-90 | Records today are kept in a **mix** of notebooks, files and WhatsApp | Q-G1 |

**Fourth set — last open items** (date 2026-11-06; follow-up choices in the development session;
written confirmation via `docs/CLIENT_DECISION_SUMMARY.md`):

| ID | Decision | Question |
|---|---|---|
| CD-91 | Hosting: **Hostinger** shared hosting with **hPanel** (design kept portable to cPanel) | Q-H2 |
| CD-92 | TDS on commission: **field kept but off**; partner PAN not collected for now | Q-C4 |
| CD-93 | **No separate approval step** before sending a quotation | Q-Q8 |
| CD-94 | Final website service list = the **quotation categories** (architectural drawings, working & municipal drawings, exterior 3D, interior design, interior 3D, site supervision visits, material & colour selection); CodInt drafts descriptions for client review | Q-S1, Q-S4 |
| CD-95 | Office hours shown as **"Visits by appointment"** | Q-W3 |
| CD-96 | Map taken **from the address**; the client checks the pin on the staging copy | Q-W3 |
| CD-97 | The client **marks the major projects** when sending photos; Admin can change it later | Q-W1 |

Note: the visiting card (CD-12) is already in the repository (`reference/Visiting Card.jpeg`).

---

## 1. General workflow (G)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-G1 | P1 | How do you track enquiries, quotations, payments, expenses and drawings today? | Mix of notebooks, files and WhatsApp (session answer) → CD-90 |
| Q-G2 | P1 | Usual sequence: quote at enquiry stage, or open a project first? When is something a "project"? | Both paths happen (session answer) → CD-89 |
| Q-G3 | P3 | *(internal)* Use WorkLedger as a reference? | Style reference only — D-19 approved |
| Q-G4 | P2 | One enquiry list for website and phone/walk-in enquiries (recommended)? | Keep distinct → CD-31 |
| Q-G5 | P2 | Reminders: dashboard only, daily email, or other? | Dashnboard with Priority Emails → CD-32 |
| Q-G6 | P3 | Client portal needed? (out of scope) | Not Necessary → CD-33 |
| Q-G7 | P3 | How long to keep non-converted enquiries? | Until Deleted give delete Options datewise → CD-34 |
| Q-G8 | P3 | Date format DD/MM/YYYY and financial year April–March? | financial year April–March; DD/MM/YYYY (session answer) → CD-35, CD-36 |
| Q-G9 | P1 | Website first, or everything together? | together → CD-37 |
| Q-G10 | P2 | Existing data to import? | No → CD-38 |
| **Q-G11** | P1 | `reference/portfolio/Senior office profile.pdf` is the profile of another architect (Bhushan Chakote, Pune). Why was it supplied — layout/style reference, a previous employer, or something else? (It will **never** be published as AJ's work.) | Dont Use it just for sample but its design is worst → CD-39 |

## 2. Services (S)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-S1 | P1 | Final list of services and sub-items | Quotation categories become the final list (session answer) → CD-94 |
| Q-S2 | P1 | What do **Temple Work**, **कोकण शिल्प** and **Complete Project** mean? Design-only, or also execution/turnkey? | They are complted n कोकण शिल्प  etc.are Some local terms to describe project; design + supervision only (session answer) → CD-40 |
| Q-S3 | P2 | Project types to use | Architectural/ Civil/ Interier/ Landscape → CD-41 |
| Q-S4 | P2 | Which services appear on the website, with what description? | Quotation categories; CodInt drafts, client reviews → CD-94 |
| **Q-S5** | P1 | May **demo** services appear on the **live** public website before you confirm them, or only in the ERP and on staging? | ERP only, not public (session answer) → CD-42 |

## 3. Website (W) and brand (B)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-W1 | P1 | Which projects are "major"? Please supply original photos and project details, or give access to the Instagram posts (not readable without login). | Client sends originals (session answer) → CD-43. Client marks major projects when sending photos → CD-97 |
| Q-W2 | P2 | Separate Gallery page, or merged with Portfolio? | Merge → CD-44 |
| Q-W3 | P1 | Address spelling: "Sai **Arcade** Building" (quotation) or "Sai **Arked** Building" (visiting card)? Map location and office hours? | Sai Arcade Building (session answer) → CD-45. Visits by appointment; map from the address, pin checked on staging → CD-95, CD-96 |
| Q-W4 | P1 | Two numbers on the card — **8806956877** and **7796877369**. Which is primary, which is WhatsApp, and may both be published? | 8806956877 for WhatsApp; only this number published (session answer) → CD-46 |
| Q-W5 | P1 | Client permission to publish; client names shown or hidden? | Names shown only with that client's permission (session answer) → CD-47 |
| Q-W6 | P2 | Who receives enquiry emails? CAPTCHA if spam occurs? | Mail ID from Visiting Card /CAPTCHA; simple built-in CAPTCHA; sent from a domain mailbox (session answer) → CD-48 |
| Q-W7 | P3 | Testimonials (with permission), registrations (e.g. Council of Architecture no.)? | with permission, Council of Architecture no → CD-49. Number to be sent by the client (open, not blocking) |
| Q-W8 | P2 | English only, or English + Marathi? | English + Marathi; website and printed documents, ERP in English (session answer) → CD-50 |
| Q-W9 | P2 | About Studio text | **Answered** by CD-03/CD-04/CD-05: CodInt drafts from Instagram and references, formal tone, client reviews later |
| **Q-W11** | P2 | May anyone other than you publish or unpublish portfolio items? | Admin only — only the Admin uses the ERP for now (CD-80) |
| Q-B1 | P1 | Vector (AI/SVG/PDF/CDR) or transparent PNG logo? | Use Given → CD-51 |
| Q-B2 | P2 | Approve colours and font style | Colours - Logo n Visiting Card Style, Gothic Font Family; visiting-card Copperplate Gothic style (session answer) → CD-51 |

## 4. Quotation (Q)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-Q1 | P1 | Quotation number format | **Answered** by CD-14: developer proposes (proposal D-28: `AJDS/Q/{fy}/{seq3}`) — `AJDS/Q/2026-27/001` approved (session answer) → CD-52 |
| Q-Q2 | P1 | Letterhead | **Narrowed** by CD-13 (logo + visiting card). Still open: keep "श्री" at the top? Show the Instagram QR code? | Go Same; "श्री" kept, no QR (session answer) → CD-53 |
| Q-Q3 | P1 | Area basis (built-up / carpet / plot / all floors) and unit | All → CD-54 |
| Q-Q4 | P1 | One composite rate or separate rates? | **Answered** by CD-15/CD-17: both supported; Admin sets rates |
| Q-Q5 | P1 | Fixed and item-wise fees? | **Answered** by CD-15/CD-16 |
| Q-Q6 | P2 | Amount in words, client block, acceptance block? | acceptance block → CD-55 |
| Q-Q7 | P1 | Standard terms: validity, revisions, visits, extra charges, exclusions, cancellation, drawing ownership | All; CodInt drafts, client reviews (session answer) → CD-56 |
| Q-Q8 | P2 | Separate approval step before sending? (Only Admin sends either way — CD-25) | No separate step (session answer) → CD-93 |
| Q-Q9 | P2 | Email quotations from the ERP, or download and share? | Download add Share through whatsapp → CD-57 |
| Q-Q10 | P3 | Signature wording ("Ar. Ajit Arjun Kumbhar" or "Ar. Ajit Kumbhar"), signature image/stamp? | Ar. Ajit Kumbhar → CD-58. Signature image: not requested (off) |

## 5. Fees, billing, payments, expenses (F)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-F1 | P1 | Bills, or payments against the agreement? | **Answered** by CD-18: flexible. Design: per-project billing method (D-26, proposed) |
| Q-F2 | P1 | Payment stages | **Narrowed** by CD-22/CD-23. Stage percentages on the total including GST (session answer) → CD-59 |
| Q-F3 | P1 | Is the studio GST-registered? GSTIN, rate, SAC, invoice format, tax on advances? To be confirmed with your tax adviser | Not registered today (session answer) → CD-60. GST stays off; tax treatment to be confirmed with the tax adviser if the studio registers |
| Q-F4 | P2 | Discounts given? Approval threshold? | Max 5% → CD-61 |
| Q-F5 | P2 | Extra charges billed separately (visits, travel, printing)? | Yes Keep them separate → CD-62 |
| Q-F6 | P1 | Receipt format and numbering | Numbering → CD-63 (format AJDS/R/{fy}/{seq4} proposed, D-28) |
| Q-F7 | P2 | Payment modes used | Online/ Cash / UPI → CD-64 |
| Q-F8 | P2 | Which expenses to track? Reimbursements? | Rents Travel etc. → CD-65. Reimbursement by clients: not requested (off) |
| **Q-F9** | P2 | Do you ever refund money to clients? | In case by percentage cutting → CD-66 |
| **Q-F10** | P2 | Allow writing off an unpaid balance (Admin only)? | Admin only → CD-67 |
| **Q-F11** | P2 | Transfer credit from one project to another of the same client? | No → CD-68 |
| **Q-F12** | P2 | Do you ever receive an advance **before** a project is opened (at enquiry stage)? | Yes Possible → CD-69 |

## 6. Contractor / referral commission (C) — new
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| **Q-C1** | P1 | Direction and parties: does the studio pay commission **to** the contractor/referrer? Can one project have more than one partner or commission? | Studio pays; one partner per project (session answer) → CD-70 |
| **Q-C2** | P1 | Is a non-contractor referrer (friend, previous client, agent) recorded as "Contractor", or as a separate source "Referral"? | Separate → CD-71 |
| **Q-C3** | P1 | Percentage of what — quoted total, agreed fee **excluding GST**, or amounts actually received? When is it payable — on agreement, as the client pays, or on completion? Do fee variations, refunds or write-offs change it? | On Completion, Yes Charges changes; % of final fee excl. GST incl. variations (session answer) → CD-72 |
| **Q-C4** | P1 | Is tax deducted at source on commission, or any GST involved? (Confirm with your tax adviser; PAN needed?) | Decide it later Keep it GST involved → CD-73; TDS field kept but off, no PAN for now (session answer) → CD-92 |
| **Q-C5** | P2 | May office staff see partner names/phones, select a partner on an enquiry, and see source labels and counts? (Commission amounts stay Admin-only regardless) | No → CD-74 |
| **Q-C6** | P2 | If a project is cancelled or the client does not pay, what happens to approved or partly paid commission? How long are partner records kept? | Till Removed; Admin decides on cancellation/non-payment (session answer) → CD-75 |

## 7. Projects & documents (P, D)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-P1 | P2 | Project statuses | Planned/OnGoing/OnHold/Completed/HandOver; plus Cancelled (session answer) → CD-76 |
| Q-P2 | P2 | Project code format | **Narrowed** by CD-14 (proposal D-28: `AJDS/P/{fy}/{seq3}`, same pattern as the approved quotation number) |
| Q-P3 | P2 | Log site visits in the ERP? Visit limits? | Log them, Dont put limits → CD-77 |
| **Q-P4** | P2 | Meetings/site visits before a project is confirmed — record them on the enquiry? | Yes Record them → CD-78 |
| Q-D1 | P2 | File types and sizes to store | Keep on basic Server capabilty minimum as possible → CD-79 |

## 8. Users & reports (U, R)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-U1 | P1 | Who will use the ERP and what may each person do? | **Narrowed** by CD-25 (finance Admin-only) and CD-29 (Ar. Ajit Kumbhar is the main Admin user). Admin only for now (session answer) → CD-80 |
| Q-U2 | P2 | Mobile use at site? | Allow → CD-81 |
| Q-U3 | P3 | Two-step login for Admin? | No → CD-82 |
| **Q-U4** | P1 | Within "finance is Admin-only": may staff (a) draft quotation **scope** without prices, (b) send a quotation you have approved, (c) submit expense claims for your approval? | No to all → CD-83 |
| Q-R1 | P2 | Most needed reports (incl. source and commission reports) | Yes → CD-84 |

## 9. Hosting & technical (H, T)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-H1 | P1 | Domain | **Answered** by CD-01: `ajdesignstudios.in`. Please **confirm the exact spelling** ("studio**s**", plural, while the brand is "AJ Design Studio") before DNS/SSL set-up. Spelling confirmed (session answer) → CD-85 |
| Q-H2 | P1 | Hosting provider/plan, PHP/MySQL versions, storage, cron, SSL | Hosting Not Finalized, PHP/MySQL Latest, Storage 500MB, -, -; plan for 10 GB+ (session answer) → CD-86. Hostinger with hPanel (session answer) → CD-91 |
| Q-H3 | P3 | Password-protected staging copy? | Yes (session answer) → CD-87 |
| Q-H4 | P2 | Off-site backup destination and responsibility | Developer Company(CodInt) will take it Weekly → CD-88 |
| Q-H5 | P2 | Business email on the domain for notifications? | On Visiting Card → CD-48 (send from a domain mailbox, deliver to the visiting-card email) |
| Q-T1 | P2 | *(internal)* PDF library | mPDF — D-18 approved |

---

## 10. Items still open
No P1 item is open; Stage 1 was approved on 2026-11-06.

Waiting for the client (not blocking the design): Council of Architecture registration number (Q-W7);
original photos with "major" marks (CD-43, CD-97); review of the drafted website text, service
descriptions, quotation terms and Marathi translations; signature of `docs/CLIENT_DECISION_SUMMARY.md`.
