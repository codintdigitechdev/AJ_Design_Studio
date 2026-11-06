# Portfolio Website Plan

**Status: APPROVED 2026-11-06 (Stage 1 gate).** Items marked PROPOSED in this document are approved as written; anything still marked PENDING waits for the named answer. Corrected 2026-11-06.
Tags: `CLAUDE.md` §3.

**Content rules [CLIENT-DECISION]:**
- Content is **drafted by CodInt** from the Instagram presence and the reference documents (CD-03),
  in a **professional, formal and ethical** tone (CD-04), and **reviewed by the client** (CD-05).
- No invented projects, project details, services, statistics, awards, testimonials or contact
  details; no private client information without approval (CD-11, CD-12).
- Nothing from `reference/portfolio/Senior office profile.pdf` (another architect) is ever used (sample only — CD-39).

## 1. Goals
1. Present AJ Design Studio as a professional architecture & interior practice.
2. Showcase real work — all major projects with available photographs (CD-08).
3. Convert visitors into enquiries (form, WhatsApp, call).
4. Local search visibility (Patan, Karad, Satara — keywords to confirm).

## 2. Sitemap and URLs (domain `ajdesignstudios.in` — CD-01, CD-85)

| Page | URL | Content source |
|---|---|---|
| Home | `/` | Website content blocks + featured portfolio |
| About Studio | `/about` | Drafted from Instagram and references; client review |
| Services | `/services` | Confirmed service categories only (CD-42) |
| Portfolio | `/portfolio` (`?category=`) | Published items, highlighted first |
| Project Details | `/portfolio/{slug}` | Published item + gallery |
| Marathi pages | `/mr/…` (e.g. `/mr/portfolio`) | Marathi version of every page (CD-50) |
| Contact | `/contact` | Sai Arcade Building; 8806956877 (CD-45, CD-46) |
| Enquiry | `/enquiry` | Form → ERP enquiries |
| Thank you | `/enquiry/thank-you` | noindex |
| Privacy notice | `/privacy` | Approved text |
| 404 / 410 | — | Branded; 410 for removed portfolio items |
| System | `/sitemap.xml`, `/robots.txt` | Generated from published content; `/erp/` disallowed |

## 3. Page plans

### Home
Hero (real AJ photos only), short intro, services overview, featured work (featured flag; highlighted
first), optional process strip (only if confirmed), CTA band, footer with contacts.

### About Studio
Studio profile and principal's profile (Ar. Ajit Arjun Kumbhar — Architect & Interior Designer;
Patan, Karad, Satara) drafted from Instagram and references; no invented experience figures, awards
or registrations; the Council of Architecture registration number is shown once supplied (CD-49).

### Services
Categories and items marked "show on website". Demo services are used only inside the ERP and are never
shown publicly (CD-42); the page lists the confirmed services — the quotation categories (CD-94), with descriptions drafted by
CodInt for client review. Soft-deleted items disappear from the site.

### Portfolio and Project Details
- Category filter; **display sequence** (PROPOSED): highlighted/major projects by display priority →
  other projects by display priority → completion year (newest first) → title [CD-10].
- Project page: cover, facts (category, city, year, services, optional area), description, gallery,
  previous/next, enquiry CTA.
- Removed or unpublished projects return 410/404 and leave the sitemap; old slugs redirect (301).
- Client names appear only with that client's permission (CD-47).

### Gallery
Merged into Portfolio (CD-44): each project page carries its own gallery; there is no separate Gallery page.

### Contact [CD-12]
Sai Arcade Building, Opp. Shiv Doulat Bank, Karad Chiplun Road, Patan (CD-45); phone and WhatsApp
8806956877 only (CD-46); email; visits **by appointment** (CD-95); map from the address, pin checked on staging (CD-96); enquiry form.

### Enquiry form
Name*, Mobile*, Email, City/site, Project type, Services, Approx. area + unit, Message, preferred
contact, privacy consent*, built-in CAPTCHA (CD-48). Honeypot, minimum fill time, CSRF, rate limit.
Saved to the Website Enquiries inbox (CD-31); notification email to ar.ajitkumbhar16@gmail.com, sent
from a domain mailbox (CD-48).

### WhatsApp
Floating and contact-page button `https://wa.me/91XXXXXXXXXX?text=…` with 8806956877 (CD-46). Each click only increments a daily counter — no personal data, never an enquiry record.

## 4. Content managed from the ERP
| Content | ERP location | Review |
|---|---|---|
| Portfolio items, images, order, featured, highlighted, publish/unpublish/remove | Portfolio module | Item review status |
| Marathi text | Marathi fields on each content item (CD-50) | Same review status |
| Services text | Service master (website fields) | Demo badge |
| Hero, intro, About, contact block, SEO defaults | Settings → Website content | Block review status |
| Enquiries | Enquiry module | — |

## 5. Publishing workflow [CD-08…CD-11] (details `docs/WORKFLOWS.md` Part D)
1. Draft: upload originals (stored privately), write text, record consent.
2. Review: content status "pending client review" → "approved" after the client's review.
3. Publish (Admin): requires consent, cover image, alt text on every image, approved content; web
   versions copied to the public folder; sitemap updated.
4. Unpublish / remove (Admin, reason): public copies withdrawn; listing and sitemap updated; 410/404.

## 6. SEO plan
Unique titles/descriptions, clean slugs, canonical URLs, HTTPS, one H1, `sitemap.xml` (published
only), `robots.txt` disallows `/erp/`, schema.org `LocalBusiness`/`ProfessionalService` (name, Sai Arcade Building
address, 8806956877, sameAs Instagram); hreflang for English and Marathi pages, Open Graph, mandatory alt text, WebP + responsive sizes.

## 7. Responsive behaviour
Mobile first; off-canvas menu; sticky call/WhatsApp bar on mobile; 1/2/3–4 column grids.

## 8. Launch checklist
- [ ] Original photos and details for the major projects (client sends and marks major ones — CD-43, CD-97), with consent; names only with permission (CD-47)
- [ ] All drafted text reviewed by the client (CD-05)
- [ ] Service descriptions reviewed by the client (CD-94)
- [ ] Map pin checked on staging (CD-96); Council of Architecture number received (Q-W7)
- [ ] Logo crops from the supplied file (CD-51)
- [ ] Marathi translations reviewed by the client (CD-50)
- [ ] Privacy notice approved
- [ ] Hostinger plan (10 GB+) purchased (CD-91); staging copy reviewed by the client (CD-87)

## 9. Design direction
`project-context/UI_UX_GUIDELINES.md`: charcoal + copper, image-first, architectural grid, formal tone.
