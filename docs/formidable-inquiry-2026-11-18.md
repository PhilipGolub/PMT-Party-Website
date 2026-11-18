# Formidable event inquiry integration

Date: November 18, 2026. Target: https://oxygen.pmtparty.com only.
Branch: `codex/staging-editorial-refinement`.

## Result and ownership

The existing Oxygen inquiry page now contains a functioning five-step Formidable
form. The refined homepage, shared components, original event form, customer
records, payment settings, and production were preserved.

| Object | ID / key | State |
| --- | --- | --- |
| Existing homepage | 4640 | WordPress draft; unchanged in this milestone |
| Existing inquiry page | 4662 / `event-form` | WordPress draft; genuine form embedded |
| Original Event Form | 3 / `event-form` | Preserved; no original entries read |
| Staging working form | 13 / `pmt-event-inquiry-staging` | Renderable; administrators only |
| Form style | 4685 / `ykipmw` | PMT Editorial Inquiry — Staging |
| Confirmation action | 4684 | On-submit message only |
| Synthetic test image | 4687 | One-pixel PNG, no client information |

Authenticated previews:

- [Homepage draft](https://oxygen.pmtparty.com/?page_id=4640&preview=true)
- [Working inquiry draft](https://oxygen.pmtparty.com/?page_id=4662&preview=true)

The public `/event-form/` destination is not published. The homepage's seven
inquiry links resolve to the authenticated staging preview, including navigation,
hero, portfolio, custom creations, final CTA, and footer. No production inquiry
URL remains in the rendered previews inspected.

## Verified connection and management path

Fresh native discovery returned 352 WordPress abilities, including 51 Formidable
abilities. Site identity was verified again as `https://oxygen.pmtparty.com`.
Runtime: WordPress 7.1.4, Oxygen 6.2.2, PHP 8.5.12, Formidable Forms 7.0,
Formidable Pro 7.0.1, Conversational Forms 1.3, and Visual Views 5.13.

The installed official Formidable MCP skill was used with the working native
WordPress abilities. No additional credential file or helper connection was
needed. All Formidable writes used dedicated native abilities. Oxygen writes
used its documented element schema and native editing tools.

The available catalog has no dedicated form-duplication ability. A safe working
copy was therefore created with supported `create-form` and `create-field`
abilities, copying 22 active source fields and then restructuring the copy.
The unused draft checkbox and old submit field were excluded; the new form uses
Formidable's native submit button. Original actions and historical entries were
not copied. No direct database writes, PHP writes, plugin changes, or resets were
performed.

The original form's `list-fields` call failed output validation because legacy
associative choices do not satisfy its declared array schema. A read-only,
site-guarded call to the public `FrmField::get_all_for_form()` API retrieved only
whitelisted field configuration. No entries were included. Read-only rendering
and installed-plugin source inspection also confirmed version-specific options.
The final working form reads successfully through native `list-fields`.

## Field structure and preserved questions

Form 13 has 62 native field records: four page breaks, six explanatory HTML
fields, 50 input fields, one review summary, and one CAPTCHA. The type inventory
is: HTML 6, select 3, text 7, radio 10, date 1, time 4, break 4, checkbox 4,
number 6, textarea 10, URL 1, file 1, name 1, email 1, phone 1, summary 1,
CAPTCHA 1. There are 33 conditional fields and no foreign-form conditional IDs.

| Stage | Native fields and key IDs |
| --- | --- |
| 1 — About your event | Event type 163, guest count 164, other event 182, date certainty 183, conditional date 178, venue 165, city 184, start/end times 185–186 |
| 2 — Services | Services 167; backdrops 170; signage/seating chart 168; balloons 169; floral details 171–172; centerpiece/table/chair counts 177/174/176; runners 175; product quantities/sizes/wording 189; rental/coordination/custom requests 190/191/173; installation requirement 192 |
| 3 — Inspiration and budget | Colors 166, theme 195, inspiration link 196, images 197, décor budget 198 |
| 4 — Venue and installation | Setting 202, setup times 203–204, collection 205, loading/access 206, stairs/elevator 207, width/depth/height 208–210, measurement certainty 211, obstructions 212, mounting restrictions 213, approval status/details 214–215, acknowledgement 216 |
| 5 — Contact and review | Native name 160, contact preference 161, email 159, conditional phone 162, notes 179, privacy acknowledgement 219, summary 220, CAPTCHA 180 |

Page-break IDs are 187, 193, 199, and 217. Native progress titles are Your event,
Services, Inspiration, Venue, and Contact. Back buttons and summary Edit controls
use Formidable's own navigation. The responsive progress control collapses
intermediate stages into an expandable ellipsis.

The original event choices and relevant décor questions were retained or
clarified. Color selection became an open text answer; floral, balloon, backdrop,
seating, rental, product, and coordination details appear when relevant services
are selected. Venue questions appear for installation requested or undecided,
and are hidden for products-only collection. The products-only fourth step
explains that installation details are unnecessary.

Dates distinguish confirmed, tentative, and unset plans. Dropdowns begin with
empty prompts instead of silently selecting an event, guest range, or budget.
The budget explicitly covers décor/styling/custom creations, not the total event,
and includes “I'm not sure yet.” Venue fields distinguish confirmed measurements
from estimates and require restrictions, approval status, and acknowledgement
when installation applies. Unknown measurements need not be invented.

## Actions, privacy, and staging restrictions

Original form 3 retains actions 3150 (email), 3152 (on-submit), and 3237
(Google Sheets). Those actions were inspected without copying destinations into
Git or changing them.

Working form 13 has only action 4684, an on-submit confirmation:

> Your test inquiry has been saved.
> This is a staging test. No business inquiry, email notification, payment or
> Google Sheets update has been initiated.

There are no email, webhook, spreadsheet, registration, or payment actions on
the working form. Entry storage is enabled. AJAX submission, native validation,
honeypot protection, and the inherited CAPTCHA are enabled. No test email or
payment was initiated. Outbound delivery logs were not independently audited.

Formidable's internal status is `published`, because its draft status will not
render the genuine form. This does **not** publish the WordPress page.
`logged_in=1` and `logged_in_role=[administrator]` restrict the form during testing.

Uploads allow JPG/JPEG, PNG, and WebP only, at most five files of 5 MB each.
Image resizing is set to a 2000-pixel width. Attach-to-email is disabled.
`protect_files`, `noindex_files`, and administrator-only protected-file roles are
enabled. The synthetic file's protected download returned an image with HTTP 200
for the authenticated administrator and HTTP 403 without authentication.
No client uploads or private records were used.

## Native Oxygen embedding and styling

Page 4662 uses `OxygenElements\\Shortcode`, element 142, with:

```text
[formidable id="pmt-event-inquiry-staging" title="0" description="0"]
```

The native custom Structure label is **Inquiry — Form Embed**. Its parent is
**Inquiry — Formidable Form Container**, element 137. The existing notice,
element 136, now states that this is an administrator staging test using
synthetic information with business notifications disabled.

All 43 authored inquiry nodes retain descriptive `meta.friendlyName` labels.
The final saved tree and Oxygen preview were reread successfully. Homepage 4640
and reusable components 4642, 4645, and 4648 were not modified in this milestone.
Active home-page setting remains 0, header IDs [4618], and footer IDs empty.

Formidable style 4685 uses the established Cormorant Garamond / DM Sans system,
paper `#f7f3ed`, white `#fffdf9`, charcoal `#24211f`, muted `#625a53`, wine
`#7c2635`, and border `#d8cfc4`. Inputs are 48 pixels high with 16-pixel text;
field spacing is 24 pixels. Related short answers use native half/third rows.
Small form-scoped custom rules handle editorial headings, active-step contrast,
choice spacing, and stacked review tables on mobile. No new sitewide styles
or unmanaged form-processing code were introduced.

## Verification results

| Check | Result |
| --- | --- |
| Source preservation | Original form/actions remain; no historical submissions accessed |
| Native structure | 62 fields, five pages, 33 conditional fields; all conditional references local |
| Native server rendering | All five page variants render; genuine form appears in Oxygen preview |
| API negative validation | Missing event type rejected; missing required installation restrictions/acknowledgement rejected |
| API valid products-only path | Synthetic entry 43 saved; hidden venue requirements did not block it |
| API valid installation path | Synthetic entry 44 saved and read back by known ID |
| Browser products-only flow | All five steps completed; confirmation displayed; entry 45 and image persisted |
| Browser installation flow | Mobile five-step flow completed; confirmation displayed; entry 46 persisted with dimensions 12/6/9 feet and estimated status |
| Browser conditional behavior | Event-date, service-specific details, installation questions, and preferred-contact phone field toggle correctly |
| Browser validation | Missing required fields, invalid email, privacy consent, and installation requirements blocked progression; focus moved to first invalid field |
| Upload handling | TXT rejected; 6 MB PNG rejected; 68-byte synthetic PNG accepted and saved |
| Protected download | Authenticated 200 image; anonymous 403 |
| Review and navigation | Prior answers displayed, Back/forward works, venue values visible, empty review cards hidden |
| Responsive inquiry | Inspected at 1440×1000, 820×1180, and 390×844; no horizontal document overflow |
| Mobile accessibility smoke test | Keyboard activated navigation disclosure and radio/checkbox controls; native error states and labelled inputs observed |
| Homepage preservation smoke test | Desktop/mobile render; loaded images valid; seven inquiry links point to staging; mobile inquiry link reaches real form |
| Page publication | Both 4640 and 4662 verified as WordPress drafts |

Only known synthetic entries 43/44 and exact synthetic searches within the new
form 13 were read. Entries 43–46 and the synthetic image remain on staging for
review; no existing data was deleted. Browser artifacts are ignored by Git.

Normal form page loads and the final installation submission showed zero console
errors. Six warnings came from the existing Hostinger AI widget: deprecated
SVGLoader calls and zero-size WebGL framebuffer warnings. One upload-rejection
removal interaction generated a request to `/[object%20Event]` returning 404;
the accepted upload and subsequent submission still succeeded. This appears to
be a plugin-side interaction to investigate, not a corrected issue.

## Remaining requirements before publication

1. Verify sitewide staging access protection. A challenge or draft-only preview
   is not sufficient evidence of comprehensive staging protection.
2. Obtain approval to discourage search-engine indexing: the inspected
   `blog_public` setting currently allows indexing. This setting was not changed.
3. Decide the intended staging tester access model before changing the current
   administrator-only form restriction. Review privacy wording and retention.
4. Recheck actions, protected upload delivery, and CAPTCHA with the intended
   tester role. Six-file limit, alternate-role access, all image formats, full
   screen-reader testing, and automated accessibility audits were not exercised.
5. Confirm the final design and obtain explicit publication approval. Then verify
   `/event-form/` and replace draft-preview links with its actual staging URL.
6. Configure any future business notifications separately, using approved
   recipients and controlled tests. No live workflow is authorized by this work.

The Oxygen visual editor was not reopened/saved during this Formidable milestone.
Persisted native labels and frontend rendering are verified; visual-editor save
compatibility and the 14-property Oxygen Doctor warning remain separate,
unresolved checks described in the November 17 record. No OxyMade class was
deleted or repaired speculatively.

## Operational notes and rollback

- `update-form` can change status if omitted; provide it explicitly and read back
  restrictions. The internal published form must remain administrator-only until
  the intended tester access is approved.
- The composite Name default must remain a schema-compatible empty string.
  A composite object default caused a native `list-fields` output-schema error
  during development and was corrected without replacing the native Name field.
- The style sanitizer removed a leading `#` from custom CSS. Scoped selectors
  start `div#frm_form_13_container` to preserve the intended selector. The site
  root font size is 10 pixels; heading sizes use explicit pixel bounds.
- Git stores this implementation record and development safeguards, not Oxygen
  layouts, Formidable configuration exports, entries, or uploads. No backup is
  implied. Capture an approved private configuration backup before promotion.
- A reversible suspension can remove the new shortcode from draft 4662 and set
  form 13 to its internal draft state through native tools. Preserve source form
  3 and synthetic evidence; do not delete forms, entries, or upload records as an
  automatic rollback. A Git revert cannot undo these WordPress changes.
