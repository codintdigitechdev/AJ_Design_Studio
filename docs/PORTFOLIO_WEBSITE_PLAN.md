# Portfolio Website Plan

Status: **PROPOSED** — no UI pages are created before approval. Corrected 2026-11-06 for CD-01…CD-12.
Tags: `CLAUDE.md` §3.

**Content rules [CLIENT-DECISION]:**
- Content is **drafted by CodInt** from the Instagram presence and the reference documents (CD-03),
  in a **professional, formal and ethical** tone (CD-04), and **reviewed by the client** (CD-05).
- No invented projects, project details, services, statistics, awards, testimonials or contact
  details; no private client information without approval (CD-11, CD-12).
- Nothing from `reference/portfolio/Senior office profile.pdf` (another architect) is ever used (Q-G11).

## 1. Goals
1. Present AJ Design Studio as a professional architecture & interior practice.
2. Showcase real work — all major projects with available photographs (CD-08).
3. Convert visitors into enquiries (form, WhatsApp, call).
4. Local search visibility (Patan, Karad, Satara — keywords to confirm).

## 2. Sitemap and URLs (domain `ajdesignstudios.in` — CD-01; spelling Q-H1)

| Page | URL | Content source |
|---|---|---|
| Home | `/` | Website content blocks + featured portfolio |
| About Studio | `/about` | Drafted from Instagram and references; client review |
| Services | `/services` | Service categories with "show on website" (demo only if Q-S5) |
| Portfolio | `/portfolio` (`?category=`) | Published items, highlighted first |
| Project Details | `/portfolio/{slug}` | Published item + gallery |
| Gallery | `/gallery` | Images with "show in gallery" (Q-W2) |
| Contact | `/contact` | Studio settings (CD-12; Q-W3, Q-W4) |
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
or registrations (Q-W7).

### Services
Categories and items marked "show on website". Initially demo services [CD-06]; public display of
demo items only if Q-S5 allows. Soft-deleted items disappear from the site.

### Portfolio and Project Details
- Category filter; **display sequence** (PROPOSED): highlighted/major projects by display priority →
  other projects by display priority → completion year (newest first) → title [CD-10].
- Project page: cover, facts (category, city, year, services, optional area), description, gallery,
  previous/next, enquiry CTA.
- Removed or unpublished projects return 410/404 and leave the sitemap; old slugs redirect (301).

### Gallery
Published images with "show in gallery" on, category filter, lightbox, link to the project.

### Contact [CD-12]
Address (spelling Q-W3), phone 1 / phone 2 and WhatsApp (Q-W4), email, office hours, map on demand,
enquiry form.

### Enquiry form
Name*, Mobile*, Email, City/site, Project type, Services, Approx. area + unit, Message, preferred
contact, privacy consent*. Honeypot, minimum fill time, CSRF, rate limit. Saved as an enquiry
(source Website, "New – unreviewed"); optional email to the studio (Q-W6).

### WhatsApp
Floating and contact-page button `https://wa.me/91XXXXXXXXXX?text=…` with the number from Settings
(Q-W4). Each click only increments a daily counter — no personal data, never an enquiry record.

## 4. Content managed from the ERP
| Content | ERP location | Review |
|---|---|---|
| Portfolio items, images, order, featured, highlighted, publish/unpublish/remove | Portfolio module | Item review status |
| Gallery images | Portfolio images (gallery switch) | — |
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
only), `robots.txt` disallows `/erp/`, schema.org `LocalBusiness`/`ProfessionalService` (name, address,
phone, sameAs Instagram — after Q-W3/Q-W4), Open Graph, mandatory alt text, WebP + responsive sizes.

## 7. Responsive behaviour
Mobile first; off-canvas menu; sticky call/WhatsApp bar on mobile; 1/2/3–4 column grids.

## 8. Launch checklist
- [ ] Original photos and details for the major projects, with publishing consent (Q-W1, Q-W5)
- [ ] All drafted text reviewed by the client (CD-05)
- [ ] Final or approved-for-public services (Q-S1, Q-S5)
- [ ] Address spelling, phone/WhatsApp numbers, office hours, map pin (Q-W3, Q-W4)
- [ ] Vector/transparent logo (Q-B1)
- [ ] Privacy notice approved
- [ ] Domain spelling confirmed and hosting ready (Q-H1, Q-H2)

## 9. Design direction
`project-context/UI_UX_GUIDELINES.md`: charcoal + copper, image-first, architectural grid, formal tone.
