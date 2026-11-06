# Quotation Analysis

Source: `reference/quotation-samples/work pfd & fees structure.pdf` (2 pages) **[CONFIRMED-REF]**.
**Status: dummy/sample supplied for reference [BRIEF]. Not an approved template or pricing policy.**
Client-identifying content from the sample (the project/client surname) must not be used in demo
data or on the website. Corrected 2026-11-06 for CD-13…CD-23. Tags: `CLAUDE.md` §3.

## 1. Structure of the sample (as read) [CONFIRMED-REF]

| # | Element | Content in sample | Notes |
|---|---|---|---|
| 1 | Invocation | "श्री" (Devanagari, red) at top centre | Optional letterhead setting (Q-Q2) |
| 2 | Letterhead title | "A J D E S I G N S T U D I O" in red spaced capitals | Not used going forward — the client chose logo + visiting card (CD-13) |
| 3 | Profession line | "ARCHITECT / INTERIOR DESIGNER" | |
| 4 | Address | Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan | Visiting card spells "Sai Arked" (Q-W3) |
| 5 | Contact | 8806956877, ar.ajitkumbhar16@gmail.com | Card adds 7796877369 (Q-W4) |
| 6 | Reference | "Ref: 1/2025" | Format appears `{sequence}/{year}` |
| 7 | Date | 15/12/2025 | DD/MM/YYYY |
| 8 | Title | "<Surname> BUNGLOW PROJECT" | "Buglow" typo |
| 9 | Sub-title | "DESIGN WORK" | |
| 10 | Intro line | "This is drawings for <Surname> Bunglow at Karad." | |
| 11 | Scope sections 1–6 | Numbered categories with bullet sub-items (§2) | |
| 12 | Inclusion statement | "This works & visits are includes design fees" | |
| 13 | Fee block | 1100 sq.f × 100 ru. per sq.ft = 1,10,000 | Area-based |
| 14 | Signature | "Ar. Ajit kumbhar (Principal Architect)" | No signature image |

## 2. Work categories and items in the sample [CONFIRMED-REF]

1. **All floor plans** — Ground, First, Second floor plans; Terrace plan.
2. **Working drawings** — Sections; Elevations; Municipal drawing.
3. **3D work** — Exterior 3D.
4. **Interior design** — Furniture layout; Ceiling; Electrical; Tiles; Plumbing; Room-wise sectional elevation; Furniture working drawings.
5. **Interior 3D** — Living room, Kitchen, Bedrooms.
6. **Site visits** — Centerline layout; Footing checking; PCC level; Wall level; 7′ level; Slab; Plaster;
   Tiles fitting; Interior work; Ceiling design; Electrical checking; Furniture layout explanation;
   Material selection; Colour selection; Surprise visits.

These become the **reference/demo** service seed (`content_origin` = reference/demo) [CLIENT-DECISION
CD-06: demo services initially], editable and soft-deletable by Admin (CD-07). Floor-plan and room
items vary per project and are edited per quotation.

## 3. Fee calculation in the sample

```
Total area 1100 sq.ft × ₹100 per sq.ft = ₹1,10,000   (one composite rate for all six sections)
```
No break-up, tax, discount or rounding visible. **These figures are sample values only; nothing
defaults to 1100 or ₹100** [CLIENT-DECISION CD-16: fixed pricing never mandatory].

## 4. What is missing from the sample

Client name/address/contact · site details · area basis (Q-Q3) · area unit · per-category break-up ·
GST treatment (Q-F3) · payment schedule (Q-F2) · validity · revisions included · site-visit count and
extra-visit charge (Q-Q7, Q-F5) · exclusions · scope-change rule · terms, cancellation, drawing ownership
· bank/UPI details · acceptance section · amount in words · page numbers and version · logo.

## 5. Quotation model (design PROPOSED; decisions tagged)

**Letterhead [CLIENT-DECISION CD-13]:** logo + visiting-card layout (name, title, phones, address,
email, optional Instagram QR); "श्री" optional (Q-Q2). Commission and partner data are never printed.

**Numbering [CLIENT-DECISION CD-14: developer proposes]:** proposal `AJDS/Q/{fy}/{seq3}` with `-R{n}`
for the revision, number taken on first send (D-28, PROPOSED).

**Header:** number, revision, date, validity (optional), client, project, site, area + basis + unit, subject, intro.

**Scope:** categories → items from the service master (demo items allowed), text editable, inclusion marker.

**Fee lines (combinable) [CLIENT-DECISION CD-15: area-based and item-wise]:**
| Method | Formula |
|---|---|
| Area-based | area × rate |
| Area-based per category | area × category rate |
| Fixed fee | lump sum (never mandatory — CD-16) |
| Item-wise | qty × rate |
| Custom charge | text + amount |
Rates are entered or changed by the **Admin** [CLIENT-DECISION CD-17]; no rate is pre-filled unless the
Admin set a default.

**GST [CLIENT-DECISION CD-19/CD-20]:** "Apply GST" per revision, available only when the studio is
GST-registered, **off by default**, never compulsory. Treatment PENDING Q-F3.

**Optional blocks (off by default):** discount, rounding, payment schedule (stages — CD-22), terms,
exclusions, bank details, acceptance block, amount in words.

**Lifecycle:** Draft → Sent → Accepted / Rejected / Expired / Cancelled; older revisions become
**Superseded** (no "Revised" status — C-04). Each sent revision is frozen. Sending and deciding are
**Admin-only** [CLIENT-DECISION CD-25].

**After acceptance:** conversion if needed → fee agreement (with the revision's GST switch and stages)
→ billing per the project's billing method (agreement or bills — D-26) → if the project's source is
Contractor, a commission record in Draft (`docs/WORKFLOWS.md` Part C).

## 6. Questions for the client
`docs/CLIENT_QUESTIONS.md` §4 (Q-Q*), §5 (Q-F*), §6 (Q-C*).
