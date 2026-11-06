# Quotation Analysis

Source: `reference/quotation-samples/work pfd & fees structure.pdf` (2 pages).
**Status: dummy/sample supplied for reference. Not an approved template or pricing policy.**
Client-identifying content from the sample (e.g. the project/client surname) must not be
used in demo data or on the website.

## 1. Structure of the sample (as read)

| # | Element | Content in sample | Notes |
|---|---|---|---|
| 1 | Invocation | "श्री" (Devanagari, red) at top centre | Cultural header; keep as configurable option |
| 2 | Letterhead title | "A J D E S I G N S T U D I O" in red spaced capitals | Not the logo; logo not used |
| 3 | Profession line | "ARCHITECT / INTERIOR DESIGNER" | |
| 4 | Address | AJ Design Studio, Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan | |
| 5 | Contact | Contact no. 8806956877, E-mail ar.ajitkumbhar16@gmail.com | |
| 6 | Reference | "Ref: 1/2025" | Format appears `{sequence}/{year}` |
| 7 | Date | 15/12/2025 | DD/MM/YYYY |
| 8 | Title | "<Surname> BUNGLOW PROJECT" (underlined) | Project name; "Buglow" typo in title |
| 9 | Sub-title | "DESIGN WORK" | Document type |
| 10 | Intro line | "This is drawings for <Surname> Bunglow at Karad." | Project + location |
| 11 | Scope sections 1–6 | Numbered categories with bullet sub-items (see §2) | Core of the document |
| 12 | Inclusion statement | "This works & visits are includes design fees" | All scope included in one fee |
| 13 | Fee block | Total area 1100 sq.f; design fees 100 ru. per square foot; total 1,10,000 | Area-based |
| 14 | Signature | "Ar. Ajit kumbhar (Principal Architect)" | No signature image/stamp |

## 2. Work categories and items in the sample

1. **All floor plans** — Ground floor plan; First floor plan; Second floor plan; Terrace plan.
2. **Working drawings** — Sections; Elevations; Municipal drawing.
3. **3D work** — Exterior 3D.
4. **Interior design** — Floor plan with furniture layout; Ceiling layout; Electrical layout;
   Tiles layout; Plumbing layout; Room-wise sectional elevation; Furniture working drawings.
5. **Interior 3D** — Living room, Kitchen, Bedrooms.
6. **Site visits** — Centerline layout; Footing layout checking; PCC level; Wall construction level;
   7′ construction level; Slab checking; Plaster work checking; Tiles fitting checking;
   Interior work; Ceiling design; Electrical layout checking; Furniture layout explanation visit;
   Material selection; Colour selection; Surprise visits.

Observations:
- Floor-plan items depend on the number of floors → should be generated/edited per project, not fixed.
- Interior 3D rooms vary per project → editable list.
- Site visits are listed as **stages**, without a number of visits → visit count/limits unknown.
- "Municipal drawing" sits under working drawings; whether municipal **approval liaison** is included is unknown.
- Spelling in sample (Buglow, Muncipal, explaination, "sq.f", "ru.") — the system should use
  corrected standard text; the client should confirm wording.

## 3. Fee calculation in the sample

```
Total area        = 1100 sq.ft          (which area? built-up / carpet / plot — unknown)
Rate              = ₹100 per sq.ft       (single rate covering ALL six sections)
Design fee total  = 1100 × 100 = ₹1,10,000
```
- One composite rate covers architecture + interiors + 3D + site visits.
- No per-category break-up, no tax, no discount, no rounding visible.
- Amount written with Indian grouping (1,10,000), no "₹" symbol, no amount in words.

**These figures are sample values only. Nothing in the system will default to 1100 or ₹100.**

## 4. What is missing from the sample

| Missing item | Why it matters |
|---|---|
| Client name, address, contact | Needed for a formal quotation and later billing |
| Site address / plot details | Only "at Karad" |
| Area basis (built-up / carpet / plot / per floor) | Directly drives the fee |
| Area unit choice (sq.ft vs sq.m) | |
| Per-category fee break-up | Needed if client may accept only part of the scope |
| GST / tax treatment, GSTIN, SAC code | Depends on registration status |
| Payment schedule / stages | Needed for billing and reminders |
| Validity of quotation | |
| Number of design revisions included | Common dispute area |
| Number of site visits included; extra-visit charge | Sample lists stages but no count |
| Exclusions (structural design, MEP design, liaison fees, printing, travel, govt. fees) | |
| Additional-area / scope-change rule | |
| Terms & conditions, cancellation, ownership/copyright of drawings | |
| Bank / UPI details | If wanted on quotation |
| Acceptance section (client signature) | For approval tracking |
| Amount in words | Common on Indian commercial documents |
| Page numbers / quotation version | Needed for revisions |
| Logo on letterhead | Sample uses text heading only |

## 5. Proposed configurable quotation model [PROPOSED]

**Header:** quotation no. (format configurable, sample-like `{seq}/{yyyy}`), revision no., date,
validity (optional), client, project, site location, area + area basis + unit, subject, intro text.

**Scope:** categories → items, picked from Service master, all text editable per quotation,
add/remove/reorder, optional per-item "included / optional / excluded" marker.

**Fee lines — methods (combinable):**
| Method | Formula | Example usage (illustrative only) |
|---|---|---|
| Area-based | area × rate per unit | Composite design fee as in sample |
| Area-based per category | area × category rate | Architecture rate + interior rate |
| Fixed fee | lump sum | Small renovation, temple work |
| Item-wise | qty × rate | n interior 3D views, n extra visits |
| Custom charge | free text + amount | Travel, plotting |

**Optional blocks (all OFF by default until approved):** discount (amount / %), tax lines
(configurable rate, name, SAC), rounding rule, payment schedule (stage, %, or amount),
terms & conditions, exclusions, bank details, client acceptance block, amount in words.

**Lifecycle:** Draft → Sent → (Revised n) → Accepted / Rejected / Expired / Cancelled.
Each sent revision frozen; history and comparison available; who/when/remark on each status change.

**Output:** print-ready HTML + PDF (A4), letterhead from Settings, signature block configurable
(default text "Ar. Ajit Kumbhar, Principal Architect" — pending confirmation of exact wording).

**After acceptance:** accepted revision becomes the project's fee agreement; payment schedule
(if used) generates expected milestones for billing and reminders.

## 6. Questions for the client
See `docs/CLIENT_QUESTIONS.md` §4 (Q-Q*) and §5 (Q-F*).
