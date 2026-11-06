# UI / UX Guidelines

Status tags: `CLAUDE.md` §3. Visual choices are PROPOSED unless marked.

## 1. Brand sources [CONFIRMED-REF]
- `reference/logo/Logo.jpeg` (1600×1034, JPEG, opaque charcoal background).
- `reference/Visiting Card.jpeg` — same monogram; letter-spaced light "Design Studio" wordmark on
  charcoal (front); copper reverse with name, title, phones, address, email, Instagram QR.
- **Do not redraw, recolour, re-typeset, stretch or add effects to the logo.** Derivatives are crops
  or resizes of the supplied files only. The client chose to use the supplied files as given (CD-51).

### Planned logo derivatives (implementation stage)
| Use | Plan |
|---|---|
| Website header | Logo crop on charcoal band, ~48–64 px tall |
| ERP sidebar | Same crop; collapsed = monogram-only crop |
| Login screen | Full logo centred on charcoal panel |
| Favicon / app icon | Monogram-only square crop, 32/180/192/512 px + `favicon.ico` |
| Quotation / bill / receipt PDF letterhead | **Logo + visiting-card layout** [CD-13, CD-53]: "श्री" at the top, logo block, "Architect & Interior Designer", Sai Arcade Building address, 8806956877, email; no QR code; signature "Ar. Ajit Kumbhar" (CD-58); English or Marathi (CD-50) |
| Open Graph image | 1200×630, logo centred on charcoal |

The sample quotation's red text heading is **not** used; "श्री" is kept at the top (CD-53).

## 2. Colour palette [CLIENT-DECISION CD-51: colours from the logo and visiting card; exact tones PROPOSED]
| Token | Hex | Use |
|---|---|---|
| `--ajds-charcoal` | `#54545C` | Header/footer, ERP sidebar, card front |
| `--ajds-charcoal-dark` | `#3A3A40` | Text on light, hover, footer |
| `--ajds-copper` | `#AF7B4C` | Primary accent, buttons, highlights, card back |
| `--ajds-copper-dark` | `#8E5F36` | Hover; small copper text (contrast) |
| `--ajds-tan` | `#A78A5E` | Secondary accent, dividers |
| `--ajds-ivory` | `#F7F4EF` | Light page background |
| `--ajds-stone` | `#E8E3DB` | Section alternation, cards, borders |
| `--ajds-white` | `#FFFFFF` | Cards, forms |
Copper on white is below 4.5:1 for body text — use copper-dark for small text. WCAG AA throughout.

## 3. Typography [CLIENT-DECISION CD-51: visiting-card "Gothic" style]
- Headings: wide, letter-spaced capitals in the visiting card's **Copperplate Gothic** style — a licensed
  web font or a free look-alike, chosen and shown to the client in Stage 3 (font choice PROPOSED).
- Body: a clean sans-serif (e.g. Inter / Source Sans 3), 16 px, 1.6 line-height. Max 2 families, self-hosted.
- Marathi pages, Marathi documents and "श्री": Noto Sans Devanagari (CD-50, CD-53).

## 4. Tone of voice [CLIENT-DECISION]
- **Professional, formal and ethical.** Plain factual statements; no superlatives ("best", "No. 1"),
  no unverifiable claims, no invented numbers, awards, clients or testimonials.
- Drafted from the Instagram presence and reference documents; every block is marked
  "pending client review" until the client reviews it (W-16).
- Marathi text is translated from the approved English text and reviewed by the client (CD-50).

## 5. Public website look & feel
- Image-first, generous white space, architectural grid, restrained copy.
- Hero uses **real AJ project photos only** (originals to be sent by the client — CD-43). Nothing from the
  "Senior office profile" PDF may appear.
- Portfolio grid: highlighted (major) projects first; consistent crops; hover shows title + category.
- Project details: cover, facts strip, description, lightbox gallery.
- Sticky header with an **EN | मराठी** switch (CD-50), mobile off-canvas menu, floating WhatsApp button
  (8806956877), click-to-call. No separate Gallery page — each project has its own gallery (CD-44).
- Subtle motion; respect `prefers-reduced-motion`. Placeholders clearly marked, removed before launch.

## 6. ERP look & feel
- Bootstrap 5 admin layout: charcoal sidebar with logo, ivory content area, white cards, copper buttons.
- Menus, tabs, columns and widgets appear only when the role allows them; **financial menus, tabs,
  columns and widgets exist only for ADM** (SECURITY_RULES §8.1).
- Data tables: server-side search/filter/sort/pagination; CSV export (financial exports ADM only).
- Money right-aligned, Indian grouping (₹1,10,000.00); dates DD/MM/YYYY (CD-36). ERP screens work on mobile (CD-81).
- Confirmation dialogs for irreversible actions (issue, cancel, reverse, approve commission).
- Badges: "Demo" on demo services; "Pending client review" on website content; "Website" on web enquiries.

## 7. Print / PDF documents
- A4 portrait, logo + visiting-card letterhead, footer with contact line and page numbers.
- Quotation order follows the sample: letterhead → Ref/Date → project title → scope → fee table
  → totals → blocks → acceptance block (CD-55) → signature "Ar. Ajit Kumbhar" (CD-58).
- Amount in words off (not requested). Documents printable in English or Marathi (CD-50); shared by
  download + WhatsApp (CD-57).
- **Never print commission, partner or internal notes on client documents.**

## 8. Accessibility & performance
- Semantic HTML; alt text required on every published image.
- Visible keyboard focus; labels on every field; colour never the only indicator.
- Responsive images (`srcset`, WebP + JPEG), lazy loading; LCP < 2.5 s on 4G (target).
