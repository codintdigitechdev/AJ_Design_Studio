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

Note: the visiting card (CD-12) is already in the repository (`reference/Visiting Card.jpeg`).

---

## 1. General workflow (G)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-G1 | P1 | How do you track enquiries, quotations, payments, expenses and drawings today? | Open |
| Q-G2 | P1 | Usual sequence: quote at enquiry stage, or open a project first? When is something a "project"? | Open (both paths designed) |
| Q-G3 | P3 | *(internal)* Use WorkLedger as a reference? | Open (D-19) |
| Q-G4 | P2 | One enquiry list for website and phone/walk-in enquiries (recommended)? | Open (designed as one list) |
| Q-G5 | P2 | Reminders: dashboard only, daily email, or other? | Open |
| Q-G6 | P3 | Client portal needed? (out of scope) | Open |
| Q-G7 | P3 | How long to keep non-converted enquiries? | Open |
| Q-G8 | P3 | Date format DD/MM/YYYY and financial year April–March? | Open |
| Q-G9 | P1 | Website first, or everything together? | Open |
| Q-G10 | P2 | Existing data to import? | Open |
| **Q-G11** | P1 | `reference/portfolio/Senior office profile.pdf` is the profile of another architect (Bhushan Chakote, Pune). Why was it supplied — layout/style reference, a previous employer, or something else? (It will **never** be published as AJ's work.) | Open — new |

## 2. Services (S)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-S1 | P1 | Final list of services and sub-items | **Narrowed** by CD-06/CD-07: demo services first, Admin maintains them. Final list still needed |
| Q-S2 | P1 | What do **Temple Work**, **कोकण शिल्प** and **Complete Project** mean? Design-only, or also execution/turnkey? | Open |
| Q-S3 | P2 | Project types to use | Open |
| Q-S4 | P2 | Which services appear on the website, with what description? | **Narrowed** by CD-06 |
| **Q-S5** | P1 | May **demo** services appear on the **live** public website before you confirm them, or only in the ERP and on staging? | Open — new (default: not public) |

## 3. Website (W) and brand (B)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-W1 | P1 | Which projects are "major"? Please supply original photos and project details, or give access to the Instagram posts (not readable without login). | **Narrowed** by CD-03/CD-08/CD-10 |
| Q-W2 | P2 | Separate Gallery page, or merged with Portfolio? | Open |
| Q-W3 | P1 | Address spelling: "Sai **Arcade** Building" (quotation) or "Sai **Arked** Building" (visiting card)? Map location and office hours? | **Narrowed** by CD-12 |
| Q-W4 | P1 | Two numbers on the card — **8806956877** and **7796877369**. Which is primary, which is WhatsApp, and may both be published? | **Narrowed** by CD-12 |
| Q-W5 | P1 | Client permission to publish; client names shown or hidden? | **Narrowed** by CD-09/CD-11 (approval required; process still needed) |
| Q-W6 | P2 | Who receives enquiry emails? CAPTCHA if spam occurs? | Open |
| Q-W7 | P3 | Testimonials (with permission), registrations (e.g. Council of Architecture no.)? | Open |
| Q-W8 | P2 | English only, or English + Marathi? | Open |
| Q-W9 | P2 | About Studio text | **Answered** by CD-03/CD-04/CD-05: CodInt drafts from Instagram and references, formal tone, client reviews later |
| **Q-W11** | P2 | May anyone other than you publish or unpublish portfolio items? | Open — new (default: Admin only) |
| Q-B1 | P1 | Vector (AI/SVG/PDF/CDR) or transparent PNG logo? | Open |
| Q-B2 | P2 | Approve colours and font style | Open |

## 4. Quotation (Q)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-Q1 | P1 | Quotation number format | **Answered** by CD-14: developer proposes (proposal D-28: `AJDS/Q/{fy}/{seq3}`) — proposal needs your approval |
| Q-Q2 | P1 | Letterhead | **Narrowed** by CD-13 (logo + visiting card). Still open: keep "श्री" at the top? Show the Instagram QR code? |
| Q-Q3 | P1 | Area basis (built-up / carpet / plot / all floors) and unit | Open |
| Q-Q4 | P1 | One composite rate or separate rates? | **Answered** by CD-15/CD-17: both supported; Admin sets rates |
| Q-Q5 | P1 | Fixed and item-wise fees? | **Answered** by CD-15/CD-16 |
| Q-Q6 | P2 | Amount in words, client block, acceptance block? | Open |
| Q-Q7 | P1 | Standard terms: validity, revisions, visits, extra charges, exclusions, cancellation, drawing ownership | Open |
| Q-Q8 | P2 | Separate approval step before sending? (Only Admin sends either way — CD-25) | **Narrowed** by CD-25 |
| Q-Q9 | P2 | Email quotations from the ERP, or download and share? | Open |
| Q-Q10 | P3 | Signature wording ("Ar. Ajit Arjun Kumbhar" or "Ar. Ajit Kumbhar"), signature image/stamp? | Open |

## 5. Fees, billing, payments, expenses (F)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-F1 | P1 | Bills, or payments against the agreement? | **Answered** by CD-18: flexible. Design: per-project billing method (D-26, proposed) |
| Q-F2 | P1 | Payment stages | **Narrowed** by CD-22/CD-23. Still open: are stage percentages on the total **including or excluding GST**? |
| Q-F3 | P1 | Is the studio GST-registered? GSTIN, rate, SAC, invoice format, tax on advances? To be confirmed with your tax adviser | **Narrowed** by CD-19/20/21 (optional, never compulsory). Registration status open |
| Q-F4 | P2 | Discounts given? Approval threshold? | Open |
| Q-F5 | P2 | Extra charges billed separately (visits, travel, printing)? | Open |
| Q-F6 | P1 | Receipt format and numbering | Open (numbering proposal D-28) |
| Q-F7 | P2 | Payment modes used | Open |
| Q-F8 | P2 | Which expenses to track? Reimbursements? | Open |
| **Q-F9** | P2 | Do you ever refund money to clients? | Open — new |
| **Q-F10** | P2 | Allow writing off an unpaid balance (Admin only)? | Open — new |
| **Q-F11** | P2 | Transfer credit from one project to another of the same client? | Open — new |
| **Q-F12** | P2 | Do you ever receive an advance **before** a project is opened (at enquiry stage)? | Open — new |

## 6. Contractor / referral commission (C) — new
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| **Q-C1** | P1 | Direction and parties: does the studio pay commission **to** the contractor/referrer? Can one project have more than one partner or commission? | Open (ASSUMPTION A7: studio pays one partner) |
| **Q-C2** | P1 | Is a non-contractor referrer (friend, previous client, agent) recorded as "Contractor", or as a separate source "Referral"? | Open |
| **Q-C3** | P1 | Percentage of what — quoted total, agreed fee **excluding GST**, or amounts actually received? When is it payable — on agreement, as the client pays, or on completion? Do fee variations, refunds or write-offs change it? | Open |
| **Q-C4** | P1 | Is tax deducted at source on commission, or any GST involved? (Confirm with your tax adviser; PAN needed?) | Open |
| **Q-C5** | P2 | May office staff see partner names/phones, select a partner on an enquiry, and see source labels and counts? (Commission amounts stay Admin-only regardless) | Open (default: no) |
| **Q-C6** | P2 | If a project is cancelled or the client does not pay, what happens to approved or partly paid commission? How long are partner records kept? | Open |

## 7. Projects & documents (P, D)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-P1 | P2 | Project statuses | Open |
| Q-P2 | P2 | Project code format | **Narrowed** by CD-14 (proposal D-28: `AJDS/P/{fy}/{seq3}`) |
| Q-P3 | P2 | Log site visits in the ERP? Visit limits? | Open |
| **Q-P4** | P2 | Meetings/site visits before a project is confirmed — record them on the enquiry? | Open — new |
| Q-D1 | P2 | File types and sizes to store | Open |

## 8. Users & reports (U, R)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-U1 | P1 | Who will use the ERP and what may each person do? | **Narrowed** by CD-25 (finance Admin-only) and CD-29 (Ar. Ajit Kumbhar is the main Admin user). Other users still open |
| Q-U2 | P2 | Mobile use at site? | Open |
| Q-U3 | P3 | Two-step login for Admin? | Open |
| **Q-U4** | P1 | Within "finance is Admin-only": may staff (a) draft quotation **scope** without prices, (b) send a quotation you have approved, (c) submit expense claims for your approval? | Open — new (default: no to all) |
| Q-R1 | P2 | Most needed reports (incl. source and commission reports) | Open |

## 9. Hosting & technical (H, T)
| ID | Pri | Question | Status / answer |
|---|---|---|---|
| Q-H1 | P1 | Domain | **Answered** by CD-01: `ajdesignstudios.in`. Please **confirm the exact spelling** ("studio**s**", plural, while the brand is "AJ Design Studio") before DNS/SSL set-up |
| Q-H2 | P1 | Hosting provider/plan, PHP/MySQL versions, storage, cron, SSL | Open |
| Q-H3 | P3 | Password-protected staging copy? | Open |
| Q-H4 | P2 | Off-site backup destination and responsibility | Open |
| Q-H5 | P2 | Business email on the domain for notifications? | Open |
| Q-T1 | P2 | *(internal)* PDF library | Open (D-18) |

---

## 10. Summary of open P1 items (blocking the Stage 1 gate)
Q-G1, Q-G2, Q-G9, Q-G11, Q-S1 (final list), Q-S2, Q-S5, Q-W1, Q-W3, Q-W4, Q-W5 (process), Q-B1,
Q-Q2 (श्री/QR), Q-Q3, Q-Q7, Q-F2 (GST basis), Q-F3 (registration), Q-F6, Q-C1, Q-C2, Q-C3, Q-C4,
Q-U1, Q-U4, Q-H1 (spelling), Q-H2.
