# Portfolio Website Plan

Status: **[PROPOSED]** — no UI pages are created in Stage 0.
Content rule: **no invented projects, services, statistics, awards or testimonials.**
All copy and images come from the client or from approved drafts.

## 1. Goals
1. Present AJ Design Studio as a premium architecture & interior practice.
2. Showcase real work through strong photography and renders.
3. Convert visitors into enquiries (form, WhatsApp, call).
4. Be found in local search (Patan, Karad, Satara region — keywords to confirm).

## 2. Sitemap and URLs (pretty URLs via `.htaccess`)

| Page | URL | Source of content |
|---|---|---|
| Home | `/` | Settings → Website content + featured portfolio |
| About Studio | `/about` | Settings → About (client text, Q-W9) |
| Services | `/services` | Service categories with "show on website" flag |
| Portfolio | `/portfolio` (+ `?category=`) | Published portfolio projects |
| Project Details | `/portfolio/{slug}` | One portfolio project + gallery |
| Gallery | `/gallery` | Published gallery images (may merge with Portfolio — Q-W2) |
| Contact | `/contact` | Settings → contact block, map |
| Enquiry | `/enquiry` (also embedded on Contact/Home) | Form → ERP enquiries |
| Thank you | `/enquiry/thank-you` | Static, noindex |
| Privacy notice | `/privacy` | Approved text |
| 404 | — | Branded page |
| System | `/sitemap.xml`, `/robots.txt` | Generated |

## 3. Page plans

### Home
- Hero: full-width real project image(s), studio name, one-line positioning (client-approved), CTA "Start your project" + WhatsApp.
- Short intro (2–3 lines) → link to About.
- Services overview (icons/cards for approved categories).
- Featured projects grid (3–6, from ERP "featured").
- Process strip (e.g. Consultation → Design → Drawings → Site supervision) — only if client confirms process.
- Enquiry CTA band; footer.

### About Studio
- Studio profile, principal's profile and photo, philosophy, (registration no. if provided),
  service area. No made-up numbers ("100+ projects") unless the client supplies them.

### Services
- One section per approved category with sub-items (e.g. from sample: architectural plans,
  working & municipal drawings, exterior 3D, interior design layouts, interior 3D, site supervision,
  material & colour selection) — **only after Q-S1 confirmation**.
- CTA to enquiry with service pre-selected.

### Portfolio
- Category filter (categories configurable, e.g. Bungalow, Interior, Temple… pending Q-S3).
- Grid of cover images, title, location (city), year. Pagination or "load more".

### Project Details
- Cover image, title, facts strip (category, location, year, services, optional area),
  description, gallery with lightbox, previous/next project, enquiry CTA.
- Schema.org `CreativeWork`/`ImageGallery` markup, OG image = cover.

### Gallery
- Masonry/grid of all published images with category filter and lightbox, each linking to its project.

### Contact
- Address, phone (click-to-call), WhatsApp, email, map embed (lazy-loaded), office hours, enquiry form.

### Enquiry form (fields — PROPOSED)
Name*, Mobile*, Email, City/site location, Project type, Services interested (multi-select),
Approx. area + unit, Message, preferred contact method; consent tick for privacy notice.
Hidden honeypot + timestamp; CSRF token. On submit → saved as enquiry (source = Website),
optional email notification to studio, thank-you page. No auto-reply to visitor by default (Q-W6).

### WhatsApp enquiry
Floating button + Contact page button: `https://wa.me/91XXXXXXXXXX?text=<encoded message>`;
number from Settings (Q-W4). Optionally logs a "WhatsApp click" event (count only, no personal data).

## 4. Content managed from ERP
| Content | ERP location |
|---|---|
| Portfolio projects, images, order, featured, publish | Portfolio module |
| Gallery images | Portfolio module (images flagged for gallery) |
| Services text | Service master (website fields) |
| Home hero, intro, about text, contact block, social links, SEO defaults | Settings → Website content |
| Enquiries | Enquiry module |

## 5. SEO plan
- Unique `<title>` and meta description per page/project (editable, with defaults).
- Clean slugs, canonical URLs, HTTPS only, one H1 per page.
- `sitemap.xml` generated from published content; `robots.txt` disallows `/erp/`.
- Schema.org `LocalBusiness`/`ProfessionalService` (name, address, phone, geo, sameAs Instagram).
- Open Graph + Twitter cards (cover images).
- Image alt text mandatory; WebP + responsive sizes; lazy loading.
- Google Business Profile & Search Console setup advice at launch (client's account).

## 6. Responsive behaviour
- Mobile first; breakpoints per Bootstrap 5.
- Mobile: off-canvas menu, single-column grids, sticky call/WhatsApp bar.
- Tablet: 2-column grids. Desktop: 3–4 column grids, wide hero.

## 7. Content checklist for launch (client to provide)
- [ ] 4–10 best projects with 5–20 good images each, details and publishing consent
- [ ] About text and principal photo
- [ ] Final services list and descriptions
- [ ] Address, map pin, phone, WhatsApp, email, office hours
- [ ] Logo vector/transparent file
- [ ] Privacy notice approval
- [ ] Domain and hosting

## 8. Design direction
Per `project-context/UI_UX_GUIDELINES.md`: charcoal + copper on light neutrals, image-first,
architectural grid, restrained typography, subtle motion.
