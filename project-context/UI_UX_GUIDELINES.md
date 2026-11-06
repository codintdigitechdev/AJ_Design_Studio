# UI / UX Guidelines

## 1. Brand source
- Only source: `reference/logo/Logo.jpeg` (1600×1034, JPEG, opaque charcoal background).
- **Do not redraw, recolour, re-typeset, stretch or add effects to the logo.**
- Request from client: original vector (AI/SVG/PDF/CDR) or a transparent PNG (Q-B1).
  Until then, derivatives are made **only by cropping/resizing** the supplied JPEG,
  keeping its charcoal background.

### Planned logo derivatives (made in implementation stage, not now)
| Use | Plan |
|---|---|
| Website header | Full logo crop (monogram + wordmark) on charcoal header band, ~48–64 px tall |
| ERP sidebar | Same crop on charcoal sidebar; collapsed state = monogram-only crop |
| Login screen | Full logo, larger, centred on charcoal panel |
| Favicon / app icon | Monogram-only square crop on charcoal, 32/180/192/512 px + `favicon.ico` |
| PDF letterhead | High-res crop; on white paper either keep charcoal block or use vector once supplied |
| Open Graph image | 1200×630 on charcoal with logo centred |

Note: the sample quotation letterhead uses a **red** text heading ("A J D E S I G N S T U D I O")
and "श्री" at top, not the logo. Which letterhead style the client wants on generated
PDFs is PENDING (Q-Q2).

## 2. Colour palette (PROPOSED; sampled from logo, to be approved — Q-B2)
| Token | Hex | Use |
|---|---|---|
| `--ajds-charcoal` | `#54545C` | Logo background, header/footer, ERP sidebar |
| `--ajds-charcoal-dark` | `#3A3A40` | Text on light, hover states, footer |
| `--ajds-copper` | `#AF7B4C` | Primary accent, buttons, links, highlights |
| `--ajds-copper-dark` | `#8E5F36` | Button hover, small text on light backgrounds (contrast) |
| `--ajds-tan` | `#A78A5E` | Secondary accent (from logo detail), dividers |
| `--ajds-ivory` | `#F7F4EF` | Light neutral page background |
| `--ajds-stone` | `#E8E3DB` | Section alternation, cards, borders |
| `--ajds-white` | `#FFFFFF` | Cards, forms |
| Status colours | Bootstrap success/warning/danger/info, slightly desaturated | ERP badges only |

Contrast rule: copper `#AF7B4C` on white is below 4.5:1 for body text — use it for large
text, icons and buttons with white/charcoal text checked; use `--ajds-copper-dark` for small copper text.
All text must meet WCAG AA.

## 3. Typography (PROPOSED — Q-B2)
- Headings: a clean geometric/architectural sans or elegant serif — candidates
  *Montserrat* / *Jost* (sans) or *Cormorant Garamond* (serif) — self-hosted, max 2 families.
- Body: *Inter* / *Source Sans 3*, 16 px base, 1.6 line-height.
- Uppercase + letter-spacing for small section labels echoes the logo's spaced capitals.
- Devanagari fallback (*Noto Sans Devanagari*) if Marathi content is approved (Q-W8).

## 4. Public website look & feel
- Image-first, generous white space, restrained copy, thin lines and grid alignment.
- Full-bleed hero image/slider (real project photos only — none supplied yet).
- Portfolio grid with consistent aspect-ratio crops; hover reveals title + category.
- Project details: large cover, facts strip (category, location, year, services), story,
  gallery with lightbox (keyboard + swipe).
- Sticky header, transparent over hero then charcoal on scroll; mobile off-canvas menu.
- Floating WhatsApp button (bottom-right), click-to-call on mobile.
- Subtle motion only (fade/slide on scroll), respect `prefers-reduced-motion`.
- No stock photos presented as studio work. Placeholder images during development must be
  clearly marked and removed before launch.

## 5. ERP look & feel
- Bootstrap 5 admin layout: charcoal left sidebar with logo, light ivory content area, white cards.
- Copper primary buttons; status badges consistent across modules.
- Data tables: search, filter, sort, pagination (server-side for large lists), CSV export.
- Forms: grouped sections, required-field markers, inline validation messages, sticky Save bar on long forms.
- Money right-aligned, Indian grouping (₹1,10,000.00); dates `DD/MM/YYYY` (matches sample) — Q-G8.
- Confirmation dialogs for destructive/irreversible actions (cancel bill, reverse payment).
- Fully usable on tablet; key screens (enquiries, follow-ups, site visits) usable on mobile.

## 6. Print / PDF documents
- A4 portrait, letterhead header, footer with contact line and page numbers.
- Quotation layout mirrors sample order: letterhead → Ref/Date → project title → scope sections
  → fee summary → signature block. Improvements (table for fees, client block, terms) PROPOSED.
- Amount in words (Indian system: lakh/crore).

## 7. Accessibility & performance
- Semantic HTML, alt text required on every published image (ERP enforces).
- Keyboard focus visible, form labels, colour not the only status indicator.
- Responsive images (`srcset`, WebP + JPEG fallback), lazy loading, target LCP < 2.5 s on 4G.
