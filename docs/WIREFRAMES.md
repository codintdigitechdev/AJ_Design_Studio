# Essential Wireframes — Public Website and ERP

**Status: PROPOSED — PENDING APPROVAL.**

These are low-fidelity text wireframes. They show layout, content order and controls only —
not visual design. The look follows `project-context/UI_UX_GUIDELINES.md`: charcoal + copper,
light neutral backgrounds, with colours and fonts still PENDING (Q-B2).

**Content rules for these wireframes:**
- `[IMG]` = a real project photo supplied by the client. None has been supplied yet (Q-W1).
- `‹…›` = text the client supplies or approves. No copy, numbers or projects are invented.
- `[LOGO]` = a crop of `reference/logo/Logo.jpeg`, unchanged.

**Contents:**
- **Public website:** W-P1 Home (desktop), W-P2 Home (mobile), W-P3 Portfolio listing,
  W-P4 Project details, W-P5 Contact + enquiry, W-P6 Services
- **ERP:** W-E1 Login, W-E2 Dashboard, W-E3 List page pattern, W-E4 Enquiry detail,
  W-E5 Project detail, W-E6 Quotation builder, W-E7 Quotation PDF, W-E8 Payment + allocation,
  W-E9 Portfolio editor, W-E10 Mobile site visit
- **Approval:** checklist at the end

---

## PUBLIC WEBSITE

### W-P1 Home — desktop
```
┌──────────────────────────────────────────────────────────────────────────────┐
│ [LOGO]        Home  About  Services  Portfolio  Gallery  Contact  [Enquire ▸] │ ← transparent over hero,
├──────────────────────────────────────────────────────────────────────────────┤   charcoal on scroll
│                                                                              │
│                         [IMG full-bleed hero / slider]                       │
│                     AJ DESIGN STUDIO                                         │
│                     ‹one-line positioning – client approved›                 │
│                     [Start your project]   [WhatsApp]                        │
│                                                                              │
├──────────────────────────────────────────────────────────────────────────────┤
│  ‹2–3 line studio intro›                                   About the studio → │
├──────────────────────────────────────────────────────────────────────────────┤
│  SERVICES (approved categories only – Q-S1)                                  │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐                                 │
│  │ icon   │ │ icon   │ │ icon   │ │ icon   │   …  → /services                │
│  │‹name›  │ │‹name›  │ │‹name›  │ │‹name›  │                                 │
│  └────────┘ └────────┘ └────────┘ └────────┘                                 │
├──────────────────────────────────────────────────────────────────────────────┤
│  FEATURED WORK (3–6 projects marked featured in ERP)                         │
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
│ FOOTER (charcoal): [LOGO] · address* · phone* · email* · Instagram · Privacy │
│ *publication PENDING Q-W3/Q-W4                                     © year    │
└──────────────────────────────────────────────────────────────────────────────┘
                                                                     (◉) WhatsApp floating
```

### W-P2 Home — mobile (375 px)
```
┌─────────────────────────┐
│ [LOGO]              ☰   │ ☰ opens a slide-in menu
├─────────────────────────┤
│ [IMG hero]              │
│ AJ DESIGN STUDIO        │
│ ‹positioning›           │
│ [Start your project]    │
├─────────────────────────┤
│ ‹intro›                 │
│ Services (1 column)     │
│ Featured (1 column)     │
│ CTA band                │
│ Footer                  │
├─────────────────────────┤
│ [ Call ] [ WhatsApp ]   │ ← bar fixed to the bottom of the screen
└─────────────────────────┘
```

### W-P3 Portfolio listing — `/portfolio`
```
┌──────────────────────────────────────────────────────────────┐
│ header                                                       │
├──────────────────────────────────────────────────────────────┤
│ PORTFOLIO                                                    │
│ [All] [‹category›] [‹category›] [‹category›]   ← Q-S3 / lookups │
├──────────────────────────────────────────────────────────────┤
│ ┌──────────┐ ┌──────────┐ ┌──────────┐                       │
│ │ [IMG 4:3]│ │ [IMG 4:3]│ │ [IMG 4:3]│   3 columns desktop    │
│ │ ‹title›  │ │ ‹title›  │ │ ‹title›  │   2 columns tablet     │
│ │ ‹city·yr›│ │ ‹city·yr›│ │ ‹city·yr›│   1 column mobile      │
│ └──────────┘ └──────────┘ └──────────┘                       │
│                    [ Load more ]                             │
├──────────────────────────────────────────────────────────────┤
│ enquiry CTA band · footer                                    │
└──────────────────────────────────────────────────────────────┘
```

### W-P4 Project details — `/portfolio/{slug}`
```
┌──────────────────────────────────────────────────────────────┐
│ header                                                       │
│ [IMG cover, wide]                                            │
│ ‹Project title›  (H1)                                        │
│ ┌──────────┬──────────┬────────┬──────────────┬───────────┐  │
│ │Category  │Location  │Year    │Services      │Area*      │  │ *only if show-area is on
│ └──────────┴──────────┴────────┴──────────────┴───────────┘  │
│ ‹description – client text›                                  │
│ GALLERY  ┌────┐┌────┐┌────┐┌────┐  click → lightbox          │
│          └────┘└────┘└────┘└────┘  (keyboard + swipe)        │
│ ← Previous project                      Next project →       │
│ [ Enquire about a similar project ]  [ WhatsApp ]            │
│ footer                                                       │
└──────────────────────────────────────────────────────────────┘
```

### W-P5 Contact + enquiry — `/contact`
```
┌──────────────────────────────────────────────────────────────┐
│ CONTACT                                                      │
│ ┌───────────────────────────┐ ┌────────────────────────────┐ │
│ │ ‹address› (Q-W3)          │ │ ENQUIRY FORM               │ │
│ │ ☎ ‹phone› (tap to call)   │ │ Name*        [__________]  │ │
│ │ ◉ WhatsApp (Q-W4)         │ │ Mobile*      [__________]  │ │
│ │ ✉ ‹email›                 │ │ Email        [__________]  │ │
│ │ ‹office hours›            │ │ City / site  [__________]  │ │
│ │ ┌───────────────────────┐ │ │ Project type [▼_________]  │ │
│ │ │ map (loads on click / │ │ │ Services     [☐ ☐ ☐ ☐]     │ │
│ │ │ when scrolled into    │ │ │ Approx. area [____][sqft▼] │ │
│ │ │ view) – Q-W3          │ │ │ Message      [__________]  │ │
│ │ └───────────────────────┘ │ │ Prefer       (•)Call ( )WA │ │
│ └───────────────────────────┘ │ ☐ I agree to the Privacy   │ │
│                               │   notice*                  │ │
│                               │ [ Send enquiry ]           │ │
│                               └────────────────────────────┘ │
└──────────────────────────────────────────────────────────────┘
After sending → /enquiry/thank-you (not indexed by search engines): "Thank you – we will contact you." + WhatsApp link
Errors are shown under each field; values typed so far are kept.
```

### W-P6 Services — `/services`
```
┌──────────────────────────────────────────────────────────────┐
│ SERVICES                                                     │
│ ‹Category 1›  [IMG optional]                                 │
│   ‹description›  • ‹item› • ‹item› • ‹item›                  │
│   [ Enquire about this service ] → /enquiry?service=…        │
│ ‹Category 2› …                                               │
│ (only categories marked "show on website"; list PENDING Q-S1/Q-S4) │
└──────────────────────────────────────────────────────────────┘
```

---

## ERP

### Common ERP layout
```
┌────────────┬─────────────────────────────────────────────────────────────────┐
│ [LOGO]     │ ☰  Search [_____________]        🔔 3 due   ‹User› (Role) ▼      │
│            ├─────────────────────────────────────────────────────────────────┤
│ Dashboard  │ Breadcrumb › Page title                       [Primary action]  │
│ Enquiries  │                                                                 │
│ Clients    │  content area (ivory background, white cards)                   │
│ Projects   │                                                                 │
│ Quotations │                                                                 │
│ Fees&Bills◇│                                                                 │
│ Payments   │                                                                 │
│ Expenses ◇ │                                                                 │
│ Portfolio  │                                                                 │
│ Follow-ups │                                                                 │
│ Reports    │                                                                 │
│ ─────────  │                                                                 │
│ Services   │                                                                 │
│ Users      │                                                                 │
│ Settings   │                                                                 │
│ Audit log  │                                                                 │
└────────────┴─────────────────────────────────────────────────────────────────┘
Charcoal sidebar. Menu items appear only if the user's role allows them
(PERMISSION_MATRIX.md). On small screens the sidebar collapses to the monogram only.
```

### W-E1 Login — `/erp/login`
```
┌──────────────────────────────────────────────┐
│            (charcoal panel)                  │
│               [LOGO large]                   │
│   ┌──────────────────────────────────────┐   │
│   │ Username or email [________________] │   │
│   │ Password          [________________] │   │
│   │ [        Sign in        ]            │   │
│   │ Forgot password?                     │   │
│   │ ⚠ Invalid username or password       │   │ ← generic message
│   └──────────────────────────────────────┘   │
└──────────────────────────────────────────────┘
```

### W-E2 Dashboard
```
┌───────────────┬───────────────┬───────────────┬───────────────┐
│ New website   │ Follow-ups    │ Quotations    │ Active        │
│ enquiries  4  │ due/overdue 3 │ awaiting   2  │ projects   7  │
└───────────────┴───────────────┴───────────────┴───────────────┘
┌──── FINANCE (ADM/ACC only) ───────────────────────────────────┐
│ This FY:  Agreed ₹…   Billed ₹…◇   Received ₹…   Outstanding ₹… │
│ This month: Received ₹…   Expenses ₹…◇                         │
└───────────────────────────────────────────────────────────────┘
┌──── Follow-ups due ─────────────┐ ┌──── Projects by stage ──────┐
│ ● 10:30 Call ‹name› (Enquiry)  ✓│ │ Design ███ 3                │
│ ● Overdue: Payment ‹project›   ✓│ │ Working drawings ██ 2       │
│ View all →                      │ │ Under construction █ 1 …    │
└─────────────────────────────────┘ └─────────────────────────────┘
┌──── Recent payments ────────────┐ ┌──── Latest enquiries ───────┐
└─────────────────────────────────┘ └─────────────────────────────┘
SITE role: only "My follow-ups" and "My projects".
```

### W-E3 List page pattern (enquiries shown)
```
Enquiries                                              [+ New enquiry]
[Website – unreviewed (4)] [Open] [Converted] [Lost/Closed] [All]
Filters: Source [▼] Assigned [▼] Date [__ to __]  Search [______]  [Export CSV]
┌──────────┬──────────┬───────────┬────────┬─────────┬──────────┬──────────┐
│ No.      │ Date     │ Name      │ Mobile │ Source  │ Status   │ Next F/U │
├──────────┼──────────┼───────────┼────────┼─────────┼──────────┼──────────┤
│ ENQ-…    │ dd/mm/yy │ ‹name›    │ …      │ Website │ ●New-unr │ —        │
└──────────┴──────────┴───────────┴────────┴─────────┴──────────┴──────────┘
« 1 2 3 »   25 per page   (sorting, filtering and paging done on the server)
```

### W-E4 Enquiry detail
```
ENQ-2026-0012 · ‹name›        Status: [Contacted ▼] [Save]     [Convert to client+project]
┌── Details ─────────────────────────┐ ┌── Actions ──────────────────────────┐
│ Mobile · Email · Preferred contact │ │ [+ Activity] [+ Follow-up]           │
│ Location · Project type · Area     │ │ [+ Quotation]  [Mark spam]           │
│ Services: ‹…›   Source: Website    │ │ ⚠ Possible duplicate: Client ‹…› →   │
│ Message: ‹…›                       │ └──────────────────────────────────────┘
└────────────────────────────────────┘
┌── Timeline (activities + status changes) ─────────────────────────────────┐
│ dd/mm 11:02  Status New → Contacted  (‹user›)                             │
│ dd/mm 10:40  Call: ‹summary›                                              │
└───────────────────────────────────────────────────────────────────────────┘
┌── Quotations ─────────────┐ ┌── Follow-ups ──────────────────────────────┐
│ 3/2026 R1  Sent  ₹…       │ │ dd/mm  Call back re: quotation   ‹user› ☐   │
└───────────────────────────┘ └─────────────────────────────────────────────┘
```

### W-E5 Project detail (tabs)
```
AJ-2026-004 · ‹Project name› · ‹Client›            Status: [Design ▼]   [Edit]
[Overview] [Quotations] [Fees & Bills] [Payments] [Expenses] [Documents] [Site visits] [Timeline]
┌── Overview ─────────────────────────────┐ ┌── Money (ADM/ACC) ─────────────┐
│ Type · Site · City · Plot/Built-up area │ │ Agreed fee      ₹…             │
│ Floors · Start · Expected completion    │ │ Billed ◇        ₹…             │
│ Services: ‹…›                           │ │ Received        ₹…             │
│ Team: ‹user› (role), ‹user› (role)      │ │ Outstanding     ₹…             │
└─────────────────────────────────────────┘ │ Credit          ₹…             │
                                            └────────────────────────────────┘
Tabs are hidden when the role or the feature switch does not allow them.
```

### W-E6 Quotation builder (Draft revision)
```
Quotation 3/2026 · R1 (Draft)   Enquiry/Project: ‹…›     [Save draft] [Preview PDF] [Send ▸]
┌── Header ────────────────────────────────────────────────────────────────┐
│ Date [dd/mm/yyyy]  Valid until [____]◇  Subject [_______________________] │
│ Site location [__________]  Area [_____] Basis [Built-up ▼] Unit [sqft ▼] │
│ Intro [____________________________________________________________]      │
└──────────────────────────────────────────────────────────────────────────┘
┌── Scope of work ─────────────────────────────── [+ Add from services] ───┐
│ ≡ 1. ‹All floor plans›                                     [edit][×]     │
│      ≡ • ‹Ground floor plan›            (Included ▼)       [×]           │
│      ≡ • ‹First floor plan›             (Included ▼)       [×]           │
│      [+ item]                                                             │
│ ≡ 2. ‹Working drawings› …                                                 │
└──────────────────────────────────────────────────────────────────────────┘
┌── Fees ────────────────────────────────────────────────── [+ Fee line] ──┐
│ Type        Description        Qty/Area   Unit   Rate      Amount        │
│ [Area ▼]    ‹Design fee›       [____]     sqft   [_____]   ₹ (auto)      │
│ [Item ▼]    ‹Interior 3D view› [__]       nos    [_____]   ₹ (auto)      │
│ [Custom ▼]  ‹…›                                            [_____]       │
├──────────────────────────────────────────────────────────────────────────┤
│ Discount ◇ [none ▼]          Subtotal                 ₹ …                │
│ Tax ◇ (only if enabled)      Discount                 ₹ …                │
│ Rounding [none ▼]            Taxable                  ₹ …                │
│                              Tax                      ₹ …                │
│                              Rounding                 ₹ …                │
│                              GRAND TOTAL              ₹ …                │
│                              ‹Amount in words› ◇                          │
└──────────────────────────────────────────────────────────────────────────┘
┌── Optional blocks (all off by default) ──────────────────────────────────┐
│ ☐ Payment schedule  ☐ Terms  ☐ Exclusions  ☐ Bank details  ☐ Acceptance  │
└──────────────────────────────────────────────────────────────────────────┘
Revision history: R0 Superseded dd/mm · R1 Draft            [Compare R0↔R1]
No default values for rate or area are filled in (CLAUDE.md §7).
```

### W-E7 Quotation PDF (A4) — layout follows the order of the sample
```
┌────────────────────────────────────────────┐
│        ‹invocation e.g. "श्री" – optional›  │  Q-Q2
│  [LOGO] or ‹text heading›                  │  Q-Q2
│  ARCHITECT / INTERIOR DESIGNER             │
│  ‹address› · ‹phone› · ‹email›             │
├────────────────────────────────────────────┤
│ Ref: ‹3/2026› (R1)            Date: dd/mm/yyyy │
│ To: ‹client block› ◇ (Q-Q6)                │
│ ‹PROJECT TITLE›  (underlined)              │
│ ‹Sub-title e.g. DESIGN WORK›               │
│ ‹Intro line›                               │
│ 1. ‹Section›  • item • item                │
│ 2. ‹Section›  • item …                     │
│ ‹Inclusion statement›                      │
│ FEES table: description | basis | rate | amount │
│ Totals · amount in words ◇                 │
│ Payment schedule ◇ · Terms ◇ · Bank ◇      │
│                     ‹Signature name›       │
│                     ‹Designation› (Q-Q10)  │
│ Client acceptance block ◇                  │
├────────────────────────────────────────────┤
│ footer: contact line            Page 1 of 2 │
└────────────────────────────────────────────┘
```

### W-E8 Payment entry with allocation
```
Record payment                                                    Receipt no.: (auto)
Client [‹search›▼]  Project [‹…›▼]  Date [dd/mm/yyyy]  Amount [₹ ______]
Mode [UPI ▼]  Reference / UTR [________]  Bank [______]  Notes [__________]
┌── Allocate to open bills (Mode A) ───────────────────────────────────────┐
│ Bill        Date      Total      Open       Allocate                     │
│ B/26-27/03  dd/mm     ₹ …        ₹ …        [₹ ______]  [Fill]           │
│ B/26-27/05  dd/mm     ₹ …        ₹ …        [₹ ______]  [Fill]           │
├──────────────────────────────────────────────────────────────────────────┤
│ Allocated ₹ …    Unallocated → client credit (advance) ₹ …               │
└──────────────────────────────────────────────────────────────────────────┘
Mode B: no grid; shows "Agreed ₹… · Received so far ₹… · Outstanding after this ₹…"
[ Save & print receipt ]          Confirmation: "Posted payments cannot be edited."
```

### W-E9 Portfolio editor
```
Portfolio › ‹Title›   [Draft]                 [Preview] [Publish ▸] (blocked until ☑ consent + cover + alt text)
┌── Details ─────────────────────────────┐ ┌── Images ───────────────────────────────┐
│ Title · Slug · Category · Location     │ │ [Upload images]  drag to reorder        │
│ Year · Area [☐ show]                   │ │ ┌────┐ alt* [____] caption [___] ☐gallery│
│ Services [☐ ☐ ☐]  Featured ☐           │ │ │IMG │ ★ cover                          │
│ Short description*                     │ │ └────┘                                  │
│ Long description (rich text)           │ │ ┌────┐ alt* [____] …                    │
│ SEO title / description                │ │ └────┘                                  │
│ ☐ Client permission obtained* (Q-W5)   │ └─────────────────────────────────────────┘
└────────────────────────────────────────┘
```

### W-E10 Mobile site-visit entry ◇ (Q-P3, Q-U2)
```
┌─────────────────────────┐
│ ← AJ-2026-004 Site visit│
│ Date   [dd/mm/yyyy]     │
│ Stage  [Slab checking ▼]│
│ By     ‹current user›   │
│ Observations            │
│ [                     ] │
│ [📷 Add photos]          │
│ ☐ Chargeable ◇          │
│ [   Save visit   ]      │
└─────────────────────────┘
```

---

## Wireframe approval checklist — PENDING APPROVAL
- [ ] Public navigation items, and whether there is a separate Gallery page (Q-W2)
- [ ] Home page sections, including whether the process strip is used
- [ ] Enquiry form fields (W-P5)
- [ ] ERP menu and dashboard widgets
- [ ] Quotation builder sections and PDF layout (Q-Q2, Q-Q6, Q-Q10)
- [ ] Payment allocation screen (depends on Q-F1)
- [ ] Mobile screens needed (Q-U2)
