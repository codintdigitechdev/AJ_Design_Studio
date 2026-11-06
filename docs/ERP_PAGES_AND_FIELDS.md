# ERP Pages, URLs and Module-wise Field Specifications

**Status: PROPOSED — Stage 1 not approved.** Corrected 2026-11-06 (PG-01…PG-15). Tags: `CLAUDE.md` §3.

**URL rules:**
- All ERP URLs sit under `/erp/` and go through the ERP front controller (`docs/TECHNICAL_REQUIREMENTS.md` §2.2).
- Any page that changes data uses **POST with a CSRF token**. GET pages only display data.
- **[FIN]** marks a page, field or endpoint that is ADM-only. For non-ADM users these routes return
  **403** and financial fields are omitted from every response (`SECURITY_RULES.md` §8.1).

**Permission column:** row numbers from `docs/PERMISSION_MATRIX.md`.

**Field types:** T text (max length) · TA long text · N number · M money (₹, 2 dp, ≥ 0) · D date
(DD/MM/YYYY) · DT date-time · SEL one of list · MSEL several · CHK checkbox · FILE upload · RO read-only · AUTO system-filled.

---

## 1. Page and URL list

### 1.1 Authentication
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/login` | GET, POST | Login | public |
| `/erp/logout` | POST | Log out | any user |
| `/erp/forgot-password` | GET, POST | Request reset (same message always) | public |
| `/erp/reset-password?token=…` | GET, POST | Set new password | valid token |
| `/erp/change-password` | GET, POST | Change own password | any user |
| `/erp/profile` | GET, POST | Own profile | any user |

### 1.2 Dashboard and follow-ups
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/` → `/erp/dashboard` | GET | Dashboard (financial widgets ADM only) | 1 / 1a |
| `/erp/follow-ups` | GET | Follow-ups (financial follow-ups ADM only) | 13 / 13a |
| `/erp/follow-ups/new`, `/{id}/edit` | GET, POST | Add / edit | 13 / 13a |
| `/erp/follow-ups/{id}/done` | POST | Mark done with outcome | 13 / 13a |

### 1.3 Enquiries
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/enquiries` | GET | List; "Website – unreviewed" queue; filters incl. source and partner | 2 |
| `/erp/enquiries/new` | GET, POST | New enquiry | 2 C |
| `/erp/enquiries/{id}` | GET | Detail: activities, follow-ups, quotations (number + status only for non-ADM) | 2 V |
| `/erp/enquiries/{id}/edit` | GET, POST | Edit | 2 E |
| `/erp/enquiries/{id}/status` | POST | Change status with reason | 2 S |
| `/erp/enquiries/{id}/activities` | POST | Add activity | 2 E |
| `/erp/enquiries/{id}/convert` | GET, POST | Convert wizard (copies source + partner) | 2b |
| `/erp/enquiries/{id}/spam` | POST | Mark spam | 2a |

### 1.4 Clients
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/clients` | GET | List | 3 V |
| `/erp/clients/new`, `/{id}/edit` | GET, POST | New / edit (GSTIN field ADM only) | 3 C/E, 3a |
| `/erp/clients/{id}` | GET | Detail; financial summary panel ADM only | 3 V / 3a |
| `/erp/clients/{id}/deactivate` | POST | Deactivate | 3 D |

### 1.5 Projects
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/projects` | GET | List: status, type, client, member, source | 4 V |
| `/erp/projects/new`, `/{id}/edit` | GET, POST | New / edit (billing method ADM only) | 4 C/E, 4b |
| `/erp/projects/{id}` | GET | Overview (money panel ADM only) | 4 V |
| `/erp/projects/{id}/status` | POST | Change status | 4 S |
| `/erp/projects/{id}/members` | POST | Team | 4 E |
| `/erp/projects/{id}/quotations` | GET | [FIN] Quotations tab | 6 |
| `/erp/projects/{id}/fees` | GET | [FIN] Agreement, variations, stages, bills | 4b |
| `/erp/projects/{id}/payments` | GET | [FIN] Payments, allocations, credit, refunds | 4b |
| `/erp/projects/{id}/expenses` | GET | [FIN] Expenses tab | 9 |
| `/erp/projects/{id}/commission` | GET | [FIN] **Source & Commission tab** | 4c, 19 |
| `/erp/projects/{id}/documents` | GET | Documents (financial categories ADM only) | 10 / 10a |
| `/erp/projects/{id}/site-visits` | GET | Site visits ◇ | 4a |
| `/erp/projects/{id}/timeline` | GET | Activities and status history (no amounts) | 4 V |

### 1.6 Site visits ◇ (Q-P3)
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/projects/{id}/site-visits/new` | GET, POST | New visit (photos optional) | 4a C |
| `/erp/site-visits/{id}`, `/{id}/edit` | GET, POST | View / edit | 4a |

### 1.7 Documents and private files (PG-10, D-34)
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/projects/{id}/documents/upload` | GET, POST | Upload document or new version | 10 / 10a |
| `/erp/files/{id}/download` | GET | **Single private-file route** for documents, site-visit photos, expense attachments, commission proofs, consent records and portfolio originals. Resolves the owner (`files.owner_type/owner_id`) and applies that owner's permission, SITE assignment and the financial rule. Financial downloads always audited | owner's row |
| `/erp/documents/{id}/delete` | POST | Soft delete | 10 D |

### 1.8 Services (PG-08)
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/services` | GET | Categories and items; "Demo" badge; rates column ADM only | 5 / 5a |
| `/erp/services/categories/new`, `/{id}/edit` | GET, POST | Add / edit category | 5 C/E |
| `/erp/services/categories/{id}/delete` | POST | **Soft delete** category | 5 D |
| `/erp/services/items/new`, `/{id}/edit` | GET, POST | Add / edit item (default rate ADM only) | 5 C/E, 5a |
| `/erp/services/items/{id}/delete` | POST | **Soft delete** item | 5 D |
| `/erp/services/reorder` | POST | Display order | 5 E |

### 1.9 Quotations [FIN]
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/quotations` | GET | Register | 6 |
| `/erp/quotations/new?enquiry={id}` / `?project={id}` | GET, POST | Create R0 | 6 C |
| `/erp/quotations/{id}` | GET | Header, current revision, history | 6 V |
| `/erp/quotations/{id}/revisions/{rev}/edit` | GET, POST | Builder (Draft only) | 6 E |
| `/erp/quotations/{id}/revisions/{rev}/scope` | GET, POST | Scope-only drafting without prices ◇ (only if Q-U4 allows) | 6 (STF ◇) |
| `/erp/quotations/{id}/revisions/{rev}` | GET | Frozen revision | 6 V |
| `/erp/quotations/{id}/revisions/{rev}/print`, `/pdf` | GET | Print / PDF (logo + visiting-card letterhead) | 6 V/X |
| `/erp/quotations/{id}/compare?a=&b=` | GET | Compare revisions | 6 V |
| `/erp/quotations/{id}/approve` | POST | Approve ◇ | 6b |
| `/erp/quotations/{id}/send` | POST | Mark sent (number taken on first send) | 6a |
| `/erp/quotations/{id}/new-revision` | POST | Next revision | 6 E |
| `/erp/quotations/{id}/decision` | POST | Accept (→ conversion → fee agreement) / reject / expire / cancel | 6a |
| `/erp/quotations/{id}/email` | GET, POST | Email PDF ◇ (Q-Q9) | 6a |

### 1.10 Fees, bills and credit notes [FIN]
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/projects/{id}/billing-method` | POST | Change billing method (blocked once a bill is issued) | 4b |
| `/erp/projects/{id}/fee-agreement/new` | GET, POST | Manual agreement | 7 |
| `/erp/fee-agreements/{id}/cancel` | POST | Cancel (reason) | 7 |
| `/erp/fee-agreements/{id}/variations/new` | GET, POST | Variation (with Apply GST) | 7 |
| `/erp/fee-agreements/{id}/stages` | GET, POST | Payment stages | 7 |
| `/erp/bills` | GET | Bill register | 7a |
| `/erp/bills/new?project={id}` | GET, POST | New draft (with or without agreement) | 7a |
| `/erp/bills/{id}`, `/{id}/edit` | GET, POST | View / edit draft | 7a |
| `/erp/bills/{id}/issue` | POST | Issue | 7a |
| `/erp/bills/{id}/cancel` | POST | Cancel | 7b |
| `/erp/bills/{id}/pdf` | GET | PDF | 7a |
| `/erp/bills/{id}/apply-credit` | POST | Apply credit | 8a |
| `/erp/bills/{id}/credit-notes/new` | GET, POST | Credit note | 7b |
| `/erp/credit-notes/{id}`, `/{id}/pdf`, `/{id}/cancel` | GET, POST | View / print / cancel | 7b |

### 1.11 Payments, credit, refunds, write-offs [FIN]
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/payments` | GET | Collection register | 8 |
| `/erp/payments/new?project={id}` | GET, POST | Record payment + allocation | 8 |
| `/erp/payments/{id}` | GET | Detail with allocations | 8 |
| `/erp/payments/{id}/allocate` | GET, POST | Allocate / de-allocate | 8a |
| `/erp/payments/{id}/reverse` | GET, POST | Reverse | 8b |
| `/erp/payments/{id}/receipt` | GET | Receipt print / PDF | 8 |
| `/erp/credit-transfers/new?client={id}` | GET, POST | Credit transfer ◇ (Q-F11) | 8a |
| `/erp/refunds/new?project={id}`, `/erp/refunds/{id}`, `/{id}/reverse` | GET, POST | Refund ◇ | 8c |
| `/erp/write-offs/new?project={id}`, `/{id}/reverse` | GET, POST | Write-off ◇ | 8c |

### 1.12 Expenses [FIN]
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/expenses` | GET | List | 9 |
| `/erp/expenses/new` | GET, POST | New expense | 9 |
| `/erp/expenses/{id}` | GET | View | 9 |
| `/erp/expenses/{id}/reverse` | POST | Reverse | 9 |
| `/erp/expense-claims/new`, `/erp/expense-claims/{id}/decision` | GET, POST | Staff claim ◇ / ADM decision (only if Q-U4 allows) | 9 |

### 1.13 Portfolio (PG-09)
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/portfolio` | GET | Items: draft / pending review / published / unpublished; highlighted; featured | 11 V |
| `/erp/portfolio/new`, `/{id}/edit` | GET, POST | Add / edit | 11 C/E |
| `/erp/portfolio/{id}/images` | GET, POST | Upload (private originals), reorder, alt text, gallery switch | 11 E |
| `/erp/portfolio/{id}/preview` | GET | Preview (ERP session only) | 11 V |
| `/erp/portfolio/reorder` | POST | Display priority | 11 E |
| `/erp/portfolio/{id}/publish` | POST | Publish (checks consent, cover, alt text, review status) | 11a |
| `/erp/portfolio/{id}/unpublish` | POST | Unpublish with reason (withdraws public images) | 11a |
| `/erp/portfolio/{id}/delete` | POST | Remove (soft delete, reason, withdraws public images) | 11a |

### 1.14 Contractor / referral partners and commission (PG-01) [FIN except partner contacts]
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/partners` | GET | Partner list (contact columns; financial columns ADM only) | 18 |
| `/erp/partners/new`, `/{id}/edit` | GET, POST | Add / edit (bank/tax fields ADM only) | 18 / 18a |
| `/erp/partners/{id}` | GET | Detail: projects; commission summary ADM only | 18 / 19 |
| `/erp/partners/{id}/deactivate` | POST | Deactivate (blocked while commission outstanding) | 18 D |
| `/erp/commissions` | GET | Commission register (partner, status, outstanding) | 19 |
| `/erp/projects/{id}/commission/edit` | GET, POST | Set applicable / type / rate or amount / base / remarks (Draft) | 19 |
| `/erp/commissions/{id}/submit`, `/approve`, `/reject`, `/cancel`, `/not-applicable` | POST | Status actions, remark required | 19 |
| `/erp/commissions/{id}/adjustments/new` | GET, POST | Signed adjustment with reason | 19 |
| `/erp/commissions/{id}/payments/new` | GET, POST | Commission payment (partial allowed) | 19 |
| `/erp/commission-payments/{id}`, `/{id}/reverse`, `/{id}/voucher` | GET, POST | View / reverse / internal voucher PDF | 19 |

### 1.15 Reports (Q-R1)
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/reports` | GET | Index (financial reports listed for ADM only) | 14 |
| `/erp/reports/enquiries` | GET | Enquiry report; `?format=csv` | 14 |
| `/erp/reports/quotations` | GET | Register — counts/status for STF; values for ADM | 14 / 14b |
| `/erp/reports/projects` | GET | Project status | 14 |
| `/erp/reports/sources` | GET | Enquiries/projects by source and partner (counts) | 14a |
| `/erp/reports/outstanding` | GET | [FIN] Agreed / billed / received / outstanding | 14b |
| `/erp/reports/collections` | GET | [FIN] Collections, refunds, credit | 14b |
| `/erp/reports/expenses` | GET | [FIN] Expenses | 14b |
| `/erp/reports/commission` | GET | [FIN] Commission payable/paid/outstanding by partner and project | 14b |
| `/erp/reports/commission-payments` | GET | [FIN] Commission payment register | 14b |
| `/erp/reports/profitability` | GET | [FIN] Profitability ◇ (fees received − expenses − commission paid) | 14b |

### 1.16 Administration
| URL | Method | Page / action | Permission |
|---|---|---|---|
| `/erp/users`, `/new`, `/{id}/edit` | GET, POST | Users | 15 |
| `/erp/users/{id}/reset-password`, `/{id}/unlock` | POST | Admin actions | 15 |
| `/erp/roles`, `/erp/roles/{id}/permissions` | GET, POST | Role grid (financial permissions locked to ADM) | 15 |
| `/erp/settings/studio` | GET, POST | Studio profile (phone 1, phone 2, WhatsApp, address) | 16 |
| `/erp/settings/letterhead` | GET, POST | Letterhead / PDF | 16 |
| `/erp/settings/numbering` | GET, POST | Numbering formats | 16 |
| `/erp/settings/finance` | GET, POST | [FIN] Default billing method, rounding, lock date | 16a |
| `/erp/settings/gst` | GET, POST | [FIN] GST profile (dormant until Q-F3) | 16a |
| `/erp/settings/features` | GET, POST | [FIN] Optional-feature switches | 16a |
| `/erp/settings/website` | GET, POST | Website content blocks + review status | 12 |
| `/erp/settings/security` | GET, POST | Timeouts, password policy | 16 |
| `/erp/settings/lookups/{list_type}` | GET, POST | Master lists | 16 |
| `/erp/settings/backup` | GET, POST | Backup download | 16b |
| `/erp/audit-log` | GET | Audit log | 17 |

### 1.17 Background (AJAX, JSON only) (PG-15)
| URL | Method | Purpose | Permission |
|---|---|---|---|
| `/erp/api/duplicate-check` | GET | Matching mobile/email | 2 C |
| `/erp/api/partners?search=` | GET | Partner name/phone lookup | 2c |
| `/erp/api/service-items?category={id}` | GET | Items (rates included only for ADM) | 5 / 5a |
| `/erp/api/quotation-preview-totals` | POST | [FIN] Recalculate totals | 6 |
| `/erp/api/open-targets?project={id}` | GET | [FIN] Open bills / stages / agreement for allocation | 8 |
| `/erp/api/commission-preview` | POST | [FIN] Calculate commission amount | 19 |

Public pages: `docs/PORTFOLIO_WEBSITE_PLAN.md` §2.

---

## 2. Field specifications by module

Every field is validated on the server. Lengths are proposed.

### 2.1 Login
Username or email T 100*; password*; generic failure message; lockout per `SECURITY_RULES.md` §3.

### 2.2 Enquiry (ERP form) (PG-02)
| Field | Type | Req. | Notes |
|---|---|---|---|
| Enquiry no. | AUTO | — | Sequence (D-28) |
| Enquiry date | D | Y | ≤ today |
| Source | SEL (`enquiry_source`) | Y | Includes Contractor, Referral; "Website" set by the system |
| Contractor / referral partner | SEL (search) | When source = Contractor/Referral | Visible to STF only if Q-C5 allows; quick-add partner (ADM) |
| Name | T 120 | Y | |
| Mobile | T 15 | Y | Indian mobile, optional +91; duplicate check |
| Email | T 150 | N | |
| Preferred contact | SEL | N | phone / WhatsApp / email |
| Location / site | T 200 | N | |
| Project type | SEL | N | Q-S3 |
| Approx. area + unit | AREA + SEL | N | > 0 |
| Services interested | MSEL | N | Demo services allowed in the ERP |
| Budget | T 60 | N | Free text from the prospect; no amount assumed |
| Message | TA 2000 | N | |
| Assigned to | SEL users | N | |
| Next follow-up | DT | N | Creates a follow-up |
| Status | SEL | Y | `WORKFLOWS.md` A.2 |
| Lost / close reason | SEL + TA | When Lost/Closed | |
| Consent timestamp | RO | — | Website only |

### 2.3 Public enquiry form (website)
Name*, Mobile*, Email, City/site, Project type, Services (MSEL; demo services shown only if
Q-S5 allows), Approx. area + unit, Message, Preferred contact, privacy consent*. Hidden: honeypot,
timestamp (min 3 s), CSRF. Limits: 5 per IP per hour; message 2000 chars; ≤ 2 links.

### 2.4 Client (PG-14)
| Field | Type | Req. | Notes |
|---|---|---|---|
| Client type | SEL | Y | individual / company / trust / institution |
| Name | T 150 | Y | |
| Contact person | T 120 | If not individual | |
| Mobile / alternate | T 15 | Y / N | Duplicate warning |
| Email | T 150 | N | |
| Address, City, PIN | TA 300, T 80, T 6 | N | |
| State + state code | SEL | N (Y if GST used on this client) | Place of supply |
| GSTIN [FIN] | T 15 | N | ADM only; GSTIN format |
| Notes | TA | N | |

### 2.5 Project (PG-02, PG-05)
| Field | Type | Req. | Notes |
|---|---|---|---|
| Project code | AUTO | — | D-28 |
| Project name | T 150 | Y | |
| Client | SEL / search | Y | |
| Project type | SEL | Y | |
| Site address, City | TA 300, T 80 | N | |
| Plot / built-up area + unit | AREA + SEL | N | |
| Floors | N 0–50 | N | |
| Start / expected completion | D | N | completion ≥ start |
| Status | SEL | Y | `WORKFLOWS.md` A.3 |
| **Source type** | SEL Direct / Contractor | Y | CLIENT-DECISION; "Referral" value PENDING Q-C2; label visible to STF only if Q-C5 allows |
| **Contractor / referral partner** | SEL | When Contractor | Must be empty for Direct |
| **Billing method** [FIN] | SEL agreement / bills | Y (ADM; default from Settings) | Locked once a bill is issued |
| Services | MSEL | N | From accepted quotation |
| Team members | MSEL + role text | N | |
| Notes | TA | N | |

### 2.6 Site visit ◇
Visit date D*, stage SEL*, visited by SEL*, observations TA 4000, photos FILE (JPG/PNG/WebP),
chargeable CHK ◇ (only if Q-F5 confirmed; ADM only).

### 2.7 Project document
Category SEL* (financial categories ADM only), title T 150*, version T 20, date D, file FILE*
(types/size Q-D1), replaces SEL, notes TA.

### 2.8 Service category and item (PG-08)
- **Category:** name T 100*, slug AUTO, description TA, website title T 150, website description TA,
  show on website CHK, sort N, active CHK, **content origin** SEL (reference / demo / client-confirmed).
- **Item:** category SEL*, name T 150*, default description TA, default unit SEL*,
  **default rate M [FIN] (optional; ADM only)**, show on website CHK, sort, active, content origin.
- Delete = soft delete (ADM); existing quotations and portfolio items keep the item.

### 2.9 Quotation builder (one revision) [FIN] (PG-04)
| Section | Fields | Notes |
|---|---|---|
| Header | Quotation no. (AUTO on first send), revision (AUTO), date D*, valid until D ◇, enquiry/project RO, client RO/SEL, subject T 200*, site location T 200, intro TA | |
| Area | Area, basis SEL*, unit SEL* | Required if any area line; basis Q-Q3 |
| Scope | Sections and items from the service master (demo allowed), inclusion marker, reorder | Scope-only drafting by STF ◇ (Q-U4) |
| Fee lines | Type SEL (area / area-category / fixed / item / custom), description, category, qty, unit, area, **rate (ADM-editable; no pre-fill unless a default exists)**, amount AUTO | ≥ 1 line; A.5 order |
| Discount ◇ | Type, value | ≤ subtotal; approval Q-F4 |
| **Apply GST** | CHK (shown only when the studio is GST-registered; default from settings, **off**) | Tax lines name / SAC / rate; place of supply from client state |
| Rounding | SEL none / ₹1 / ₹10 | |
| Payment schedule ◇ | Stage, %, amount, trigger | Must total 100% before sending (WF-11); basis Q-F2 |
| Text blocks ◇ | Terms, exclusions, bank details, acceptance block, amount in words | All off by default |
| Totals | Subtotal, discount, taxable, tax, rounding, grand total, words | RO, server-calculated |

### 2.10 Fee agreement, variation, stages [FIN]
- **Agreement:** project RO, source revision RO/none, date D*, **Apply GST** CHK, taxable M*, tax lines,
  total AUTO; manual reason TA* when no quotation.
- **Variation:** date D*, **Apply GST** CHK, taxable amount (signed M ≠ 0)*, tax lines, total AUTO,
  reason TA*, linked revision SEL.
- **Stage:** name T 100*, % or amount*, trigger, due date; must total 100% / agreed total before final (WF-11).

### 2.11 Bill [FIN] (PG-05)
- Header: bill type RO (tax invoice only if GST-registered), project* (bills-method projects only),
  agreement SEL (optional — ad-hoc bill allowed), stage SEL (optional), bill date D*, due date D.
- Lines: as quotation fee lines + "from site visit" ◇ and "from reimbursable expense" ◇ pickers.
- **Apply GST** CHK, rounding, notes.
- Cancel: reason TA* (blocked if allocations exist).
- **Credit note:** amount M* ≤ bill grand total − earlier credit notes − write-offs (WF-08); excess over
  the open amount becomes credit; reason TA*; tax follows the bill.

### 2.12 Payment [FIN] (PG-06)
| Field | Type | Req. | Notes |
|---|---|---|---|
| Receipt no. | AUTO | — | D-28 |
| Payment date | D | Y | After lock date unless ADM override with reason |
| Client / project | SEL | Y | Project limited to the client's projects (pre-project advance only if Q-F12) |
| Amount | M > 0 | Y | **Any amount accepted — no minimum, no "must equal due" rule** |
| Mode | SEL | Y | Q-F7 |
| Reference / UTR / cheque | T 60 | For non-cash | |
| Bank, notes | T 80, TA | N | |
| Allocation grid | Open targets of the project's billing method: bills (bills method) or stages/agreement (agreement method); one target per row | N | Total ≤ amount; remainder shown as **"Advance / credit"** |
| Reversal | Reason SEL* + note TA*, date D* | — | ADM |

### 2.13 Refund ◇ / write-off ◇ / credit transfer ◇ [FIN]
Date D*, project* (transfer: from and to project of the same client), amount M* (refund ≤ credit;
write-off ≤ outstanding), mode SEL (refund), reference, reason TA*; approved by AUTO (ADM).

### 2.14 Expense [FIN]
Date D*, category SEL*, project SEL (blank = overhead), paid to T 120*, amount M*, mode SEL*,
reference T 60, attachment FILE (private, financial), reimbursable CHK ◇, notes TA.

### 2.15 Portfolio item (PG-09)
| Field | Type | Req. | Notes |
|---|---|---|---|
| Title / slug | T 150 / T 160 | Y | Slug unique; old slugs redirect 301 |
| Category | SEL | Y | |
| Location | T 80 | N | City level only |
| Completion year | N 4 | N | |
| Area + unit, show area | AREA, CHK | N | Off by default |
| Services | MSEL | N | |
| Short / long description | TA 300 / rich text | Y / N | Drafted from Instagram & references; formal tone |
| **Content review status** | SEL draft / pending client review / approved | Y | Must be approved to publish |
| Featured (home page) | CHK | N | |
| **Highlighted (major project)** | CHK | N | CLIENT-DECISION |
| **Display priority** | N | N | Ordering (`WORKFLOWS.md` Part D) |
| SEO title / description | T 70 / T 160 | N | |
| Linked internal project | SEL | N | |
| **Client consent** | CHK + note + optional file | Required before publishing | Q-W5 |
| Images | FILE (several); per image alt text T 150*, caption, gallery CHK, order, cover ★ | ≥ 1 + cover to publish | Originals private; web copies on publish |
| Unpublish / remove reason | TA | On unpublish/remove | |

### 2.16 Follow-up
Linked record RO, due DT*, assigned SEL*, note TA*; outcome TA* when done. Linked to a bill, payment
or commission → ADM only.

### 2.17 User
Full name*, username* (unique), email*, mobile, role SEL* (ADM / STF / SITE), active. Temporary
password, change at first login. Password ≥ 10 chars, ≠ username (D-16).

### 2.18 Settings (PG-03, PG-12)
| Section | Fields |
|---|---|
| Studio | Name, tagline, address (spelling Q-W3), **phone 1, phone 2**, **WhatsApp number** (Q-W4), email, Instagram URL, office hours, map URL |
| Letterhead | Logo + visiting-card layout [CLIENT-DECISION]; invocation "श्री" optional (Q-Q2); Instagram QR on/off; signature name/designation (Q-Q10); footer |
| Numbering | Format and reset per sequence (`WORKFLOWS.md` B.11) |
| Finance [FIN] | Default billing method, rounding, FY start month, lock date, default validity (blank), default terms (blank) |
| GST [FIN] | Registered (default **No**), GSTIN, state code, default SAC, default tax lines, apply GST by default (**off**) — dormant until Q-F3 |
| Features [FIN] | Switches for every ◇ feature; `show_demo_services_publicly` (off, Q-S5); `staff_quotation_scope_drafting` (off, Q-U4); `staff_expense_claims` (off, Q-U4) |
| Website | Content blocks (hero, intro, About, services intro, contact, SEO defaults) — each with review status |
| Security | Idle/absolute timeout, password length, lockout |

### 2.19 Partner (contractor / referral) (PG-01)
| Field | Type | Req. | Notes |
|---|---|---|---|
| Partner type | SEL (`partner_type`) | Y | contractor / referral / other |
| Name | T 120 | Y | |
| Firm name | T 150 | N | |
| Mobile / alternate | T 15 | Y / N | Duplicate warning |
| Email, address, city | T 150, TA 300, T 80 | N | |
| Bank details [FIN] | TA (encrypted) | N | ADM only; masked in lists |
| PAN [FIN] | T 10 (encrypted) | Only if Q-C4 requires | ADM only |
| Default commission suggestion [FIN] | SEL type + value | N | Never applied automatically |
| Active, notes | CHK, TA | — | Cannot deactivate with outstanding commission |

### 2.20 Project commission [FIN]
| Field | Type | Req. | Notes |
|---|---|---|---|
| Project / partner | RO | — | Contractor-source projects only |
| Commission applicable | SEL Yes / No | Y (explicit; never defaulted to Yes) | No → status "Not applicable" |
| Commission type | SEL Percentage / Fixed | If applicable | |
| Rate % / fixed amount | PCT / M | If applicable | Exactly one, matching the type |
| Base | SEL (agreed fee excl. GST / amounts received / other) | If percentage | PENDING Q-C3 |
| Base amount | M (snapshot) | AUTO / ADM | |
| Commission amount | AUTO | — | Base × rate (paisa) or fixed |
| Status | RO + actions | — | Draft / Pending approval / Approved / Rejected / Cancelled / Not applicable |
| Approval remark | TA | On approve/reject/cancel | |
| Remarks | TA | N | |
| Paid / outstanding | AUTO | — | `WORKFLOWS.md` C.4 |

### 2.21 Commission payment [FIN]
Payment no. AUTO; date D*; amount M* (partial allowed; ≤ outstanding); mode SEL*; reference T 60;
TDS amount M (only if Q-C4); proof FILE (private, financial); notes TA. Reversal: reason SEL* + note TA*.

### 2.22 Commission adjustment [FIN]
Date D*, amount (signed M ≠ 0)*, reason TA*; approved by AUTO (ADM).
