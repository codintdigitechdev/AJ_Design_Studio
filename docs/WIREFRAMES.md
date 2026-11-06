# Essential Wireframes — Public Website and ERP

**Status: APPROVED 2026-11-06 (Stage 1 gate).** Items marked PROPOSED in this document are approved as written; anything still marked PENDING waits for the named answer. Corrected 2026-11-06 (PG-07, PG-09, PG-13).
Tags: `CLAUDE.md` §3.

These are low-fidelity text wireframes: layout, content order and controls only. The look follows
`project-context/UI_UX_GUIDELINES.md` (charcoal + copper from the logo and visiting card, Copperplate Gothic-style headings — CD-51).

**Content rules:**
- `[IMG]` = a real AJ Design Studio project photo. None supplied yet (client sends originals — CD-43). Never an image from
  `reference/portfolio/Senior office profile.pdf` (another architect).
- `‹…›` = text drafted from the Instagram presence and reference documents, in a professional,
  formal and ethical tone, and **pending client review** [CLIENT-DECISION]. No invented numbers,
  awards, clients or testimonials.
- `[LOGO]` = a crop of `reference/logo/Logo.jpeg`, unchanged.
- `[FIN]` = rendered only for ADM; for other roles the element is absent and its data is never sent.

**Contents:** Public — W-P1 Home (desktop), W-P2 Home (mobile), W-P3 Portfolio listing,
W-P4 Project details, W-P5 Contact + enquiry, W-P6 Services.
ERP — W-E1 Login, W-E2 Dashboard, W-E3 List pattern, W-E4 Enquiry detail, W-E5 Project detail,
W-E6 Quotation builder, W-E7 Quotation PDF, W-E8 Payment + allocation, W-E9 Portfolio editor,
W-E10 Mobile site visit, **W-E11 Source & Commission tab**, **W-E12 Commission payment**.

---

## PUBLIC WEBSITE

### W-P1 Home — desktop
```
┌──────────────────────────────────────────────────────────────────────────────┐
│ [LOGO]     Home  About  Services  Portfolio  Contact  [EN | मराठी]  [Enquire ▸] │ ← transparent over hero,
├──────────────────────────────────────────────────────────────────────────────┤   charcoal on scroll
│                         [IMG full-bleed hero / slider]                       │
│                     AJ DESIGN STUDIO                                         │
│                     ‹one-line positioning – pending client review›           │
│                     [Start your project]   [WhatsApp]                        │
├──────────────────────────────────────────────────────────────────────────────┤
│  ‹2–3 line studio intro›                                   About the studio → │
├──────────────────────────────────────────────────────────────────────────────┤
│  SERVICES (confirmed services only — demo items are never public, CD-42)     │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐   …  → /services                │
│  │‹name›  │ │‹name›  │ │‹name›  │ │‹name›  │                                 │
│  └────────┘ └────────┘ └────────┘ └────────┘                                 │
├──────────────────────────────────────────────────────────────────────────────┤
│  FEATURED WORK (projects marked featured; highlighted/major first)           │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐                          │
│  │ [IMG]        │ │ [IMG]        │ │ [IMG]        │  hover: title + category │
│  │ ‹title›      │ │ ‹title›      │ │ ‹title›      │                          │
│  │ ‹city · yr›  │ │ ‹city · yr›  │ │ ‹city · yr›  │        View portfolio →  │
│  └──────────────┘ └──────────────┘ └──────────────┘                          │
├──────────────────────────────────────────────────────────────────────────────┤
│  PROCESS strip – only if the client confirms the process (PENDING)           │
├──────────────────────────────────────────────────────────────────────────────┤
│  ‹CTA line›                         [Send an enquiry]  [WhatsApp]  [Call]    │
├──────────────────────────────────────────────────────────────────────────────┤
│ FOOTER: [LOGO] · Sai Arcade Building, … Patan · 8806956877 · ‹email› ·       │
│ Instagram · Council of Architecture reg. no. ‹…› · Privacy          © year    │
└──────────────────────────────────────────────────────────────────────────────┘
                                                                     (◉) WhatsApp floating
```

### W-P2 Home — mobile (375 px)
```
┌─────────────────────────┐
│ [LOGO]              ☰   │
├─────────────────────────┤
│ [IMG hero]              │
│ AJ DESIGN STUDIO        │
│ ‹positioning›           │
│ [Start your project]    │
├─────────────────────────┤
│ ‹intro› · Services ·    │
│ Featured · CTA · Footer │
├─────────────────────────┤
│ [ Call ] [ WhatsApp ]   │ ← fixed bottom bar
└─────────────────────────┘
```

### W-P3 Portfolio listing — `/portfolio`
```
┌──────────────────────────────────────────────────────────────┐
│ PORTFOLIO                                                    │
│ [All] [‹category›] [‹category›] [‹category›]                 │
├──────────────────────────────────────────────────────────────┤
│ ┌──────────┐ ┌──────────┐ ┌──────────┐   order: highlighted  │
│ │ [IMG 4:3]│ │ [IMG 4:3]│ │ [IMG 4:3]│   (major) by priority,│
│ │ ‹title›  │ │ ‹title›  │ │ ‹title›  │   then others by      │
│ │ ‹city·yr›│ │ ‹city·yr›│ │ ‹city·yr›│   priority, year, title│
│ └──────────┘ └──────────┘ └──────────┘                       │
│                    [ Load more ]                             │
└──────────────────────────────────────────────────────────────┘
```

### W-P4 Project details — `/portfolio/{slug}`
```
┌──────────────────────────────────────────────────────────────┐
│ [IMG cover, wide]                                            │
│ ‹Project title›  (H1)                                        │
│ │Category │Location (city) │Year │Services │Area* │  *only if show-area is on
│ ‹description – drafted, client-reviewed›                     │
│ GALLERY  [□][□][□][□]  → lightbox (keyboard + swipe)          │
│ ← Previous project                      Next project →       │
│ [ Enquire about a similar project ]  [ WhatsApp ]            │
└──────────────────────────────────────────────────────────────┘
Unpublished/removed project → 410/404 page; old slug → 301 to the new slug.
```

### W-P5 Contact + enquiry — `/contact`
```
┌──────────────────────────────────────────────────────────────┐
│ ┌───────────────────────────┐ ┌────────────────────────────┐ │
│ │ Sai Arcade Building, …    │ │ ENQUIRY FORM               │ │
│ │ ☎ 8806956877 (tap to call)│ │ Name*  Mobile*  Email      │ │
│ │ ◉ WhatsApp 8806956877     │ │ City / site  Project type  │ │
│ │ ✉ ‹email›                 │ │ Services [☐ ☐ ☐]           │ │
│ │ Visits by appointment     │ │ Approx. area [__][sqft▼]   │ │
│ │ [map – loads on demand]   │ │ Message  Prefer (•)Call    │ │
│ └───────────────────────────┘ │ CAPTCHA* [ 3 + 4 = __ ]    │ │
│                               │ ☐ I agree to the Privacy*  │ │
│                               │ [ Send enquiry ]           │ │
│                               └────────────────────────────┘ │
└──────────────────────────────────────────────────────────────┘
After sending → /enquiry/thank-you (noindex). Saved to the Website Enquiries inbox; email to the studio.
Errors under each field; values kept. Available in English and Marathi.
```

### W-P6 Services — `/services`
```
┌──────────────────────────────────────────────────────────────┐
│ SERVICES                                                     │
│ ‹Category 1›  [IMG optional]                                 │
│   ‹description›  • ‹item› • ‹item›                           │
│   [ Enquire about this service ] → /enquiry?service=…        │
│ (active, "show on website", confirmed — never demo items)    │
└──────────────────────────────────────────────────────────────┘
```

---

## ERP

### Common ERP layout
```
┌────────────┬─────────────────────────────────────────────────────────────────┐
│ [LOGO]     │ ☰  Search [_____________]        🔔 3 due   ‹User› (Role) ▼      │
│ Dashboard  ├─────────────────────────────────────────────────────────────────┤
│ Enquiries  │ Breadcrumb › Page title                       [Primary action]  │
│ Clients    │                                                                 │
│ Projects   │  content area (ivory background, white cards)                   │
│ Quotations [FIN]                                                             │
│ Fees&Bills [FIN]                                                             │
│ Payments   [FIN]                                                             │
│ Expenses   [FIN]                                                             │
│ Commission [FIN]                                                             │
│ Partners   (ADM only — CD-74)                                                │
│ Web inbox  (website enquiries — CD-31)                                       │
│ Portfolio  │                                                                 │
│ Follow-ups │                                                                 │
│ Reports    │ (financial reports ADM only)                                    │
│ ─────────  │                                                                 │
│ Services · Users · Settings · Audit log (ADM)                                │
└────────────┴─────────────────────────────────────────────────────────────────┘
Menu items appear only when the role allows them. [FIN] items exist only for ADM.
```

### W-E1 Login — `/erp/login`
```
┌──────────────────────────────────────────────┐
│               [LOGO large]                   │
│   Username or email [________________]       │
│   Password          [________________]       │
│   [        Sign in        ]                  │
│   Forgot password?                           │
│   ⚠ Invalid username or password  (generic)  │
└──────────────────────────────────────────────┘
```

### W-E2 Dashboard
```
┌───────────────┬───────────────┬───────────────┬───────────────┐
│ New website   │ Follow-ups    │ Quotations    │ Active        │
│ enquiries  4  │ due/overdue 3 │ awaiting   2  │ projects   7  │   ← counts only
└───────────────┴───────────────┴───────────────┴───────────────┘
┌──── FINANCE [FIN] (ADM only) ────────────────────────────────────────┐
│ This FY:  Agreed ₹…   Billed ₹… (bills-method)   Received ₹…        │
│           Outstanding ₹…   Credit held ₹…                           │
│ This month: Received ₹…   Expenses ₹…                               │
│ Commission: awaiting approval 1 · outstanding ₹…                    │
└─────────────────────────────────────────────────────────────────────┘
┌──── Follow-ups due ─────────────┐ ┌──── Projects by stage ──────┐
│ ● 10:30 Call ‹name› (Enquiry)  ✓│ │ Design ███ 3                │
│ ● Payment ‹project› [FIN]      ✓│ │ Working drawings ██ 2       │
└─────────────────────────────────┘ └─────────────────────────────┘
┌──── Recent payments [FIN] ──────┐ ┌──── Latest enquiries ───────┐
└─────────────────────────────────┘ └─────────────────────────────┘
STF: no FINANCE panel, no payment follow-ups, no recent payments. SITE: "My follow-ups", "My projects".
```

### W-E3 List page pattern (enquiries)
```
Enquiries                                              [+ New enquiry]
[Open] [Converted] [Lost/Closed] [All]              [Delete by date range…] (ADM)
Filters: Source [▼] Partner [▼]* Assigned [▼] Date [__ to __]  Search [____]  [Export CSV]
┌──────────┬──────────┬───────────┬────────┬────────────┬──────────┬──────────┐
│ No.      │ Date     │ Name      │ Mobile │ Source     │ Status   │ Next F/U │
├──────────┼──────────┼───────────┼────────┼────────────┼──────────┼──────────┤
│ AJDS/E/… │ dd/mm/yy │ ‹name›    │ …      │ Website    │ New      │ —        │
│ AJDS/E/… │ dd/mm/yy │ ‹name›    │ …      │ Contractor │ Contacted│ dd/mm    │
└──────────┴──────────┴───────────┴────────┴────────────┴──────────┴──────────┘
*Partner filter ADM only. Website submissions have their own inbox (CD-31). Server-side paging.
```

### W-E4 Enquiry detail
```
AJDS/E/2026-27/0012 · ‹name›   Status: [Contacted ▼] [Save]   [Convert to client+project]
┌── Details ─────────────────────────┐ ┌── Actions ──────────────────────────┐
│ Mobile · Email · Preferred contact │ │ [+ Activity] [+ Follow-up]           │
│ Location · Project type · Area     │ │ [+ Quotation] (ADM)  [Mark spam]     │
│ Services: ‹…›                      │ │ ⚠ Possible duplicate: Client ‹…› →   │
│ Source: Contractor · ‹partner›*    │ └──────────────────────────────────────┘
│ Message: ‹…›                       │
└────────────────────────────────────┘
┌── Timeline (no amounts) ──────────────────────────────────────────────────┐
│ dd/mm 11:02  Status New → Contacted  (‹user›)                             │
│ dd/mm 10:40  Call: ‹summary›                                              │
└───────────────────────────────────────────────────────────────────────────┘
┌── Quotations ───────────────────────┐ ┌── Follow-ups ──────────────────────┐
│ AJDS/Q/2026-27/003 R1  Sent         │ │ dd/mm Call back  ‹user› ☐          │
│ ₹… [FIN] (ADM only)                 │ └────────────────────────────────────┘
└─────────────────────────────────────┘
*Source and partner shown to ADM only (CD-74).
```

### W-E5 Project detail (tabs)
```
AJDS/P/2026-27/004 · ‹Project name› · ‹Client›     Status: [OnGoing ▼]  [Edit]
Source: Contractor · ‹partner›*        Billing method: Agreement [FIN]
[Overview] [Quotations][FIN] [Fees & Bills][FIN] [Payments][FIN] [Expenses][FIN]
[Source & Commission][FIN] [Documents] [Site visits] [Timeline]
┌── Overview ─────────────────────────────┐ ┌── Money [FIN] (ADM only) ──────┐
│ Type · Site · City · Plot/Built-up area │ │ Agreed       ₹…                │
│ Floors · Start · Expected completion    │ │ Billed       ₹… (bills method) │
│ Services: ‹…›                           │ │ Received     ₹…                │
│ Team: ‹user› (role), ‹user› (role)      │ │ Outstanding  ₹…                │
└─────────────────────────────────────────┘ │ Credit       ₹…                │
                                            │ Commission o/s ₹…              │
                                            └────────────────────────────────┘
*Source shown to ADM only (CD-74). Tabs absent when role or feature switch disallows them.
```

### W-E6 Quotation builder (Draft revision) [FIN — ADM]
```
Quotation (no. on first send) · R1 (Draft)   Enquiry/Project: ‹…›   [Save draft] [PDF EN/MR] [Send ▸] [Share on WhatsApp]
┌── Header ────────────────────────────────────────────────────────────────┐
│ Date [dd/mm/yyyy]  Valid until [____]◇  Subject [_______________________] │
│ Site location [__________]  Area [_____] Basis [▼] Unit [sqft ▼]          │
│ Intro [____________________________________________________________]      │
└──────────────────────────────────────────────────────────────────────────┘
┌── Scope of work ─────────────────────────────── [+ Add from services] ───┐
│ ≡ 1. ‹All floor plans›                                     [edit][×]     │
│      ≡ • ‹Ground floor plan›      (Included ▼)  [Demo]     [×]           │
│ ≡ 2. ‹Working drawings› …                                                 │
└──────────────────────────────────────────────────────────────────────────┘
┌── Fees ────────────────────────────────────────────────── [+ Fee line] ──┐
│ Type        Description        Qty/Area   Unit   Rate      Amount        │
│ [Area ▼]    ‹Design fee›       [____]     sqft   [_____]   ₹ (auto)      │
│ [Item ▼]    ‹Interior 3D view› [__]       nos    [_____]   ₹ (auto)      │
│ [Custom ▼]  ‹…›                                            [_____]       │
├──────────────────────────────────────────────────────────────────────────┤
│ Discount [none ▼] (≤ 5%)          Subtotal                 ₹ …            │
│ ☐ Apply GST (only if registered)  Discount                 ₹ …            │
│ Rounding [none ▼]                 Taxable                  ₹ …            │
│                                   GST lines                ₹ …            │
│                                   Rounding                 ₹ …            │
│                                   GRAND TOTAL              ₹ …            │
└──────────────────────────────────────────────────────────────────────────┘
┌── Blocks ────────────────────────────────────────────────────────────────┐
│ ☐ Payment schedule  ☑ Terms  ☐ Exclusions  ☐ Bank details  ☑ Acceptance  │
└──────────────────────────────────────────────────────────────────────────┘
Revision history: R0 Superseded dd/mm · R1 Draft            [Compare R0↔R1]
No rate or area is pre-filled unless the ADM set a default. Rates editable by ADM.
```

### W-E7 Quotation PDF (A4) — logo + visiting-card letterhead [CLIENT-DECISION]
```
┌────────────────────────────────────────────────────────────┐
│                       "श्री"                                 │
│ [LOGO]   Ar. Ajit Arjun Kumbhar                              │
│          Architect & Interior Designer                       │
│          Sai Arcade Building, … Patan · 8806956877 · ‹email› │
├────────────────────────────────────────────────────────────┤
│ Ref: ‹AJDS/Q/2026-27/003-R1›               Date: dd/mm/yyyy  │
│ To: ‹client block› (off — not requested, CD-55)             │
│ ‹PROJECT TITLE›  (underlined) · ‹DESIGN WORK›                │
│ ‹Intro line›                                                │
│ 1. ‹Section›  • item • item                                 │
│ 2. ‹Section›  • item …                                      │
│ ‹Inclusion statement›                                       │
│ FEES: description | basis | rate | amount                   │
│ Subtotal · discount ◇ · GST lines (only if applied) · total │
│ Payment schedule ◇ · Terms (standard sections) · Bank ◇     │
│                         Ar. Ajit Kumbhar · ‹Designation›     │
│ Client acceptance block                                     │
├────────────────────────────────────────────────────────────┤
│ footer: contact line                         Page 1 of 2     │
└────────────────────────────────────────────────────────────┘
Never printed: commission, partner, internal notes. No QR code (CD-53). Printable in English or
Marathi (CD-50). Shared by download + WhatsApp (CD-57).
```

### W-E8 Payment entry with allocation [FIN — ADM]
```
Record payment                                                    Receipt no.: (auto)
Client [‹search›▼]  Project [‹…›▼] (method: Bills)  Date [dd/mm/yyyy]  Amount [₹ ______]
Mode [UPI ▼]  Reference / UTR [________]  Bank [______]  Notes [__________]
┌── Allocate (one target per row) ─────────────────────────────────────────┐
│ Bills method:     Bill        Date    Total   Open    Allocate            │
│                   AJDS/B/…/03 dd/mm   ₹ …     ₹ …     [₹ ____] [Fill]      │
│ Agreement method: Stage       Due     Amount  Open    Allocate            │
│                   ‹Advance›   dd/mm   ₹ …     ₹ …     [₹ ____] [Fill]      │
│                   Agreement (no stages)       ₹ …     [₹ ____]             │
├──────────────────────────────────────────────────────────────────────────┤
│ Allocated ₹ …        Unallocated → Advance / credit ₹ …                   │
└──────────────────────────────────────────────────────────────────────────┘
Any amount is accepted (partial payments allowed). Modes: Online / Cash / UPI. An advance can also
be recorded against an enquiry (CD-69).   [ Save & print receipt ]
Confirmation: "Posted payments cannot be edited."
```

### W-E9 Portfolio editor
```
Portfolio › ‹Title›   [Draft · Pending client review]   [Preview] [Publish ▸] [Unpublish] [Remove]
 Publish is blocked until: ☑ consent · ★ cover · alt text on all images · review status = Approved
┌── Details ─────────────────────────────┐ ┌── Images (originals private) ───────────┐
│ Title · Slug · Category · Location     │ │ [Upload images]  drag to reorder        │
│ Year · Area [☐ show]                   │ │ ┌────┐ alt* [____] caption [___]        │
│ Services [☐ ☐ ☐]                       │ │ │IMG │ ★ cover                          │
│ ☐ Featured (home) ☐ Highlighted (major)│ │ └────┘                                  │
│ Display priority [__]                  │ └─────────────────────────────────────────┘
│ Short/long description (EN + मराठी)    │
│ Review status [Pending client review ▼]│
│ SEO title / description                │
│ ☐ Client permission obtained* + note   │
│ Client name [____] ☐ show (permission) │
│   [attach consent record]              │
└────────────────────────────────────────┘
Unpublish / Remove ask for a reason and withdraw the public images.
```

### W-E10 Mobile site-visit entry (CD-77, CD-81)
```
┌─────────────────────────┐
│ ← AJDS/P/…/004 Site visit│
│ Date   [dd/mm/yyyy]     │
│ Stage  [Slab checking ▼]│
│ By     ‹current user›   │
│ Observations [        ] │
│ [📷 Add photos]          │
│ [   Save visit   ]      │   (chargeable flag: ADM only)
└─────────────────────────┘
```

### W-E11 Project — Source & Commission tab [FIN — ADM]
```
Source: ( ) Direct (•) Contractor ( ) Referral    Partner: ‹name, firm› [change]
┌── Commission ────────────────────────────────────────────────────────────┐
│ Commission applicable: [ Yes ▼ ]   (must be chosen; never defaulted)     │
│ Type: (•) Percentage ( ) Fixed     Rate [__.__ %]  /  Amount [₹ ______]  │
│ Base: final agreed fee excl. GST incl. variations (CD-72)    ₹ …         │
│ Commission amount ₹ … (auto)                                             │
│ Status: Pending approval        [Approve] [Reject] (remark required)     │
│ Remarks [___________________________________________]                    │
├──────────────────────────────────────────────────────────────────────────┤
│ Payable from: ‹completion date›   Payable ₹ …  Paid ₹ …  Outstanding ₹ … │
│                                              [+ Adjustment] [+ Payment] │
│ Payments: AJDS/CP/…/0004  dd/mm  ₹ …  UPI  [Voucher] [Reverse]           │
│ History: dd/mm Draft → Pending approval (‹user›) · Approved (remark) …   │
└──────────────────────────────────────────────────────────────────────────┘
Direct project: the commission panel is not shown and the server rejects commission actions.
```

### W-E12 Commission payment [FIN — ADM]
```
Commission payment — ‹partner› · ‹project›          Payment no.: (auto)
Outstanding ₹ …
Date [dd/mm/yyyy]  Amount [₹ ______] (partial allowed, ≤ outstanding)
Mode [Online ▼]  Reference [________]  GST [₹ ____] (if charged)  TDS [₹ ____] (off — CD-92)
Allowed only after the project is Completed / HandOver (CD-72).
Proof [attach]  Notes [______________]
[ Save ]   "Posted commission payments cannot be edited — reverse instead."
```

---

## Wireframe approval checklist — PENDING
- [ ] Public navigation incl. EN/मराठी switch (Gallery merged — CD-44)
- [ ] Home sections incl. process strip; tone of drafted text (client review)
- [ ] Enquiry form fields (W-P5)
- [ ] ERP menu and dashboard widgets (financial widgets ADM only)
- [ ] Quotation builder and PDF letterhead (CD-52…CD-58)
- [ ] Payment allocation by billing method (D-26)
- [ ] Source & Commission tab and commission payment (CD-70…CD-75)
- [ ] Portfolio editor publish/unpublish/remove rules
- [ ] Mobile screens (allowed — CD-81)
