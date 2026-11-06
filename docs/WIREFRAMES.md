# Essential Wireframes — Public Website and ERP

**Status: PROPOSED — Stage 1 not approved.** Corrected 2026-11-06 (PG-07, PG-09, PG-13).
Tags: `CLAUDE.md` §3.

These are low-fidelity text wireframes: layout, content order and controls only. The look follows
`project-context/UI_UX_GUIDELINES.md` (charcoal + copper, light neutrals; colours/fonts PENDING Q-B2).

**Content rules:**
- `[IMG]` = a real AJ Design Studio project photo. None supplied yet (Q-W1). Never an image from
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
│ [LOGO]        Home  About  Services  Portfolio  Gallery  Contact  [Enquire ▸] │ ← transparent over hero,
├──────────────────────────────────────────────────────────────────────────────┤   charcoal on scroll
│                         [IMG full-bleed hero / slider]                       │
│                     AJ DESIGN STUDIO                                         │
│                     ‹one-line positioning – pending client review›           │
│                     [Start your project]   [WhatsApp]                        │
├──────────────────────────────────────────────────────────────────────────────┤
│  ‹2–3 line studio intro›                                   About the studio → │
├──────────────────────────────────────────────────────────────────────────────┤
│  SERVICES (categories marked "show on website"; demo items only if Q-S5)     │
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
│ FOOTER: [LOGO] · ‹address›* · ‹phone 1 / phone 2›* · ‹email› · Instagram ·   │
│ Privacy   *spelling and WhatsApp number PENDING Q-W3/Q-W4          © year    │
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
│ │ ‹address› (Q-W3)          │ │ ENQUIRY FORM               │ │
│ │ ☎ ‹phone 1› ‹phone 2›     │ │ Name*  Mobile*  Email      │ │
│ │ ◉ WhatsApp (Q-W4)         │ │ City / site  Project type  │ │
│ │ ✉ ‹email›                 │ │ Services [☐ ☐ ☐]           │ │
│ │ ‹office hours›            │ │ Approx. area [__][sqft▼]   │ │
│ │ [map – loads on demand]   │ │ Message  Prefer (•)Call    │ │
│ └───────────────────────────┘ │ ☐ I agree to the Privacy*  │ │
│                               │ [ Send enquiry ]           │ │
│                               └────────────────────────────┘ │
└──────────────────────────────────────────────────────────────┘
After sending → /enquiry/thank-you (noindex). Errors under each field; values kept.
```

### W-P6 Services — `/services`
```
┌──────────────────────────────────────────────────────────────┐
│ SERVICES                                                     │
│ ‹Category 1›  [IMG optional]                                 │
│   ‹description›  • ‹item› • ‹item›                           │
│   [ Enquire about this service ] → /enquiry?service=…        │
│ (active, "show on website", not deleted; demo only if Q-S5)  │
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
│ Partners   (ADM; STF only if Q-C5)                                           │
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
[Website – unreviewed (4)] [Open] [Converted] [Lost/Closed] [All]
Filters: Source [▼] Partner [▼]* Assigned [▼] Date [__ to __]  Search [____]  [Export CSV]
┌──────────┬──────────┬───────────┬────────┬────────────┬──────────┬──────────┐
│ No.      │ Date     │ Name      │ Mobile │ Source     │ Status   │ Next F/U │
├──────────┼──────────┼───────────┼────────┼────────────┼──────────┼──────────┤
│ AJDS/E/… │ dd/mm/yy │ ‹name›    │ …      │ Website    │ ●New-unr │ —        │
│ AJDS/E/… │ dd/mm/yy │ ‹name›    │ …      │ Contractor │ Contacted│ dd/mm    │
└──────────┴──────────┴───────────┴────────┴────────────┴──────────┴──────────┘
*Partner filter for STF only if Q-C5 allows. Server-side paging.
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
*Partner shown to STF only if Q-C5 allows.
```

### W-E5 Project detail (tabs)
```
AJDS/P/2026-27/004 · ‹Project name› · ‹Client›     Status: [Design ▼]   [Edit]
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
*Source label for STF only if Q-C5 allows. Tabs absent when role or feature switch disallows them.
```

### W-E6 Quotation builder (Draft revision) [FIN — ADM]
```
Quotation (no. on first send) · R1 (Draft)   Enquiry/Project: ‹…›   [Save draft] [Preview PDF] [Send ▸]
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
│ Discount ◇ [none ▼]               Subtotal                 ₹ …            │
│ ☐ Apply GST (only if registered)  Discount                 ₹ …            │
│ Rounding [none ▼]                 Taxable                  ₹ …            │
│                                   GST lines                ₹ …            │
│                                   Rounding                 ₹ …            │
│                                   GRAND TOTAL              ₹ …            │
└──────────────────────────────────────────────────────────────────────────┘
┌── Optional blocks (all off by default) ──────────────────────────────────┐
│ ☐ Payment schedule  ☐ Terms  ☐ Exclusions  ☐ Bank details  ☐ Acceptance  │
└──────────────────────────────────────────────────────────────────────────┘
Revision history: R0 Superseded dd/mm · R1 Draft            [Compare R0↔R1]
No rate or area is pre-filled unless the ADM set a default. Rates editable by ADM.
```

### W-E7 Quotation PDF (A4) — logo + visiting-card letterhead [CLIENT-DECISION]
```
┌────────────────────────────────────────────────────────────┐
│              ‹"श्री" – optional, Q-Q2›                       │
│ [LOGO]   Ar. Ajit Arjun Kumbhar                              │
│          Architect & Interior Designer                       │
│          ‹address (Q-W3)› · ‹phone 1 / phone 2› · ‹email›     │
│          [Instagram QR – optional, Q-Q2]                     │
├────────────────────────────────────────────────────────────┤
│ Ref: ‹AJDS/Q/2026-27/003-R1›               Date: dd/mm/yyyy  │
│ To: ‹client block› ◇ (Q-Q6)                                 │
│ ‹PROJECT TITLE›  (underlined) · ‹DESIGN WORK›                │
│ ‹Intro line›                                                │
│ 1. ‹Section›  • item • item                                 │
│ 2. ‹Section›  • item …                                      │
│ ‹Inclusion statement›                                       │
│ FEES: description | basis | rate | amount                   │
│ Subtotal · discount ◇ · GST lines (only if applied) · total │
│ Amount in words ◇ · Payment schedule ◇ · Terms ◇ · Bank ◇   │
│                         ‹Signature name› ‹Designation› (Q-Q10)│
│ Client acceptance block ◇                                   │
├────────────────────────────────────────────────────────────┤
│ footer: contact line                         Page 1 of 2     │
└────────────────────────────────────────────────────────────┘
Never printed: commission, partner, internal notes.
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
Any amount is accepted (partial payments allowed). [ Save & print receipt ]
Confirmation: "Posted payments cannot be edited."
```

### W-E9 Portfolio editor
```
Portfolio › ‹Title›   [Draft · Pending client review]   [Preview] [Publish ▸] [Unpublish] [Remove]
 Publish is blocked until: ☑ consent · ★ cover · alt text on all images · review status = Approved
┌── Details ─────────────────────────────┐ ┌── Images (originals private) ───────────┐
│ Title · Slug · Category · Location     │ │ [Upload images]  drag to reorder        │
│ Year · Area [☐ show]                   │ │ ┌────┐ alt* [____] caption [___] ☐gallery│
│ Services [☐ ☐ ☐]                       │ │ │IMG │ ★ cover                          │
│ ☐ Featured (home) ☐ Highlighted (major)│ │ └────┘                                  │
│ Display priority [__]                  │ └─────────────────────────────────────────┘
│ Short description* · Long description  │
│ Review status [Pending client review ▼]│
│ SEO title / description                │
│ ☐ Client permission obtained* + note   │
│   [attach consent record]              │
└────────────────────────────────────────┘
Unpublish / Remove ask for a reason and withdraw the public images.
```

### W-E10 Mobile site-visit entry ◇ (Q-P3, Q-U2)
```
┌─────────────────────────┐
│ ← AJDS/P/…/004 Site visit│
│ Date   [dd/mm/yyyy]     │
│ Stage  [Slab checking ▼]│
│ By     ‹current user›   │
│ Observations [        ] │
│ [📷 Add photos]          │
│ [   Save visit   ]      │   (chargeable flag: ADM only, ◇)
└─────────────────────────┘
```

### W-E11 Project — Source & Commission tab [FIN — ADM]
```
Source: (•) Contractor ( ) Direct      Partner: ‹name, firm› [change]
┌── Commission ────────────────────────────────────────────────────────────┐
│ Commission applicable: [ Yes ▼ ]   (must be chosen; never defaulted)     │
│ Type: (•) Percentage ( ) Fixed     Rate [__.__ %]  /  Amount [₹ ______]  │
│ Base: [‹agreed fee excl. GST› ▼]  (PENDING Q-C3)   Base amount ₹ …      │
│ Commission amount ₹ … (auto)                                             │
│ Status: Pending approval        [Approve] [Reject] (remark required)     │
│ Remarks [___________________________________________]                    │
├──────────────────────────────────────────────────────────────────────────┤
│ Payable ₹ …   Paid ₹ …   Outstanding ₹ …      [+ Adjustment] [+ Payment] │
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
Mode [Bank transfer ▼]  Reference [________]  TDS [₹ ____] (only if Q-C4)
Proof [attach]  Notes [______________]
[ Save ]   "Posted commission payments cannot be edited — reverse instead."
```

---

## Wireframe approval checklist — PENDING
- [ ] Public navigation, separate Gallery page (Q-W2)
- [ ] Home sections incl. process strip; tone of drafted text (client review)
- [ ] Enquiry form fields (W-P5)
- [ ] ERP menu and dashboard widgets (financial widgets ADM only)
- [ ] Quotation builder and PDF letterhead (Q-Q2, Q-Q6, Q-Q10)
- [ ] Payment allocation by billing method (D-26)
- [ ] Source & Commission tab and commission payment (Q-C1…Q-C6)
- [ ] Portfolio editor publish/unpublish/remove rules
- [ ] Mobile screens needed (Q-U2)
