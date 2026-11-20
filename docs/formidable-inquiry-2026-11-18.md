# Formidable event inquiry integration

Date: November 18, 2026. Target: https://oxygen.pmtparty.com only.
Branch: `codex/staging-editorial-refinement`.

This is a chronological implementation record. The latest
[delivery and pickup refinement](#delivery-and-pickup-refinement)
records the current 89-field configuration and synthetic test entries 70–74.
Earlier sections describe the configuration and checks at those milestones.

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

## Conditional-experience refinement

Implemented November 18, 2026, New York time; final checks completed November 19
UTC. The user authorized logic and content refinements while explicitly
preserving the successful visual design. All writes in this pass targeted
Formidable form 13 through native abilities. No new form or inquiry page was
created. Read-only inspection of installed Formidable code verified page-break
and Summary behavior where the generic field-options schema lacked detail.

### Preserved design and existing work

Before/after native reads verified:

- Style 4685 is exactly unchanged, including typography, colors, dimensions,
  spacing, responsive rules, and custom CSS.
- Oxygen trees 4640, 4662, 4642, 4645, and 4648 are exactly unchanged. Structure
  labels, the real form embed, shared components, and homepage remain intact.
- Original form 3 is unchanged. No original submissions were accessed.
- Form 13 options and action 4684 are unchanged. Administrator-only access,
  protected upload settings, CAPTCHA, entry storage, confirmation, and absence
  of outbound actions are preserved.
- Upload field 197, CAPTCHA 180, privacy acknowledgement 219, venue
  acknowledgement 216, and native submit 221 are exactly unchanged.
- Existing installation fields 202–216, including their required flags and
  conditional rules, are exactly unchanged.
- Both WordPress pages remain drafts. No public access, business notifications,
  payment actions, plugin changes, or live integrations were enabled.

Native submit field 221 was present in the freshly read baseline, having been
added since the initial integration. It remains last at order 471. This pass
added 15 field records to that 63-record baseline, for **78 total records**.
The record count includes explanatory HTML, page breaks, summary, CAPTCHA, and
submit; it is not the number of questions shown to every customer.

### Routing and changed existing fields

| Fields | Change |
| --- | --- |
| 163 | Renamed to Event or order type; added Standalone custom-product order, including products intended for an event |
| 164, 183, 165, 185, 186 | Hide guest count, event-date certainty, venue name, and event times for standalone orders; hidden answers are excluded by native logic |
| 178 | Existing conditional event-date field retained unchanged; date certainty still controls it |
| 184 | Event or fulfillment city / area, with delivery-area guidance |
| 167 | Retained all services and added Decals and labels and Other personalized products; supports combined selections |
| 189 | Reused as shared wording/names/personalization; item-specific wording belongs with each product's specifications |
| 190, 191, 173 | Moved after product questions within the existing Services stage; content and conditions retained |
| 192 | Still required for every request; clarified that setup includes custom products; No label now reads “No — no on-site setup needed,” preserving its original stored value |
| 199 | Native conditional page break shows Venue only for 192 = Yes or Not sure yet; button caption is Continue so it also makes sense when Venue is skipped |
| 198 | Budget label/help explicitly cover requested décor and custom products, distinct from total event budget |
| 181, 188, 194, 200, 218 | Updated explanatory copy; removed fixed heading ordinals because the native progress control now correctly counts four or five stages |
| 220 | Native Summary retained; clearer guidance explains review-group order, Edit controls, tentative dates, deadlines, estimates, access and restrictions |

The form retains five stages when installation is requested or undecided.
Selecting No on field 192 reduces it to four stages by skipping Venue, including
during Back navigation. Product fulfillment stays within the Services stage;
there is no extra step. Mixed requests retain the same product and installation
rules, and “Not sure yet” conservatively keeps venue questions.

### Added native fields

| ID / key | Purpose and conditional rule |
| --- | --- |
| 222 / `pmt-product-heading` | Product-specification explanation when any product service is selected |
| 223 / `pmt-product-quantity` | Banners: quantity, finished size with units, and item-specific wording; only Custom banners |
| 224 / `pmt-product-size` | Signage/seating-chart quantity, size and item-specific wording; only Seating charts and signage |
| 225 / `pmt-product-size-units` | Signage units, including Need guidance; only Seating charts and signage |
| 226 / `pmt-apparel-sizes` | Garment type, sizes, quantities and placement; only Personalized apparel |
| 227 / `pmt-product-material` | Optional shared material, finish or intended-use preferences; any product service |
| 228 / `pmt-artwork-status` | Required artwork availability with print-ready, reference/logo, and design-guidance choices; any product service |
| 229 / `pmt-product-deadline-status` | Required confirmed/tentative/unknown product-deadline status; any product service |
| 230 / `pmt-product-fulfillment` | Required collection request, delivery request subject to availability, or Need guidance; any product service |
| 231 / `pmt-venue-access-status` | Required confirmed/partly confirmed/unconfirmed access and load-in status; installation Yes or Not sure |
| 232 / `pmt-budget-heading` | Budget explanation within existing Inspiration stage |
| 233 / `pmt-product-needed-date` | Required completion date only for confirmed or tentative product deadlines; separate from the event date |
| 234 / `pmt-invitation-specs` | Invitation/stationery quantity, size/format, envelopes, wording and finish if known; only Invitations and stationery |
| 235 / `pmt-decal-specs` | Decal/label quantity, size with units, surface and wording if known; only Decals and labels |
| 236 / `pmt-other-product-specs` | Other product, quantity, dimensions/units and wording if known; only Other personalized products |

Specifications are optional and accept estimates or “Need guidance.” Related
details share a small number of fields instead of repeating a long technical
questionnaire for each product. Category-specific answers have their own native
conditions so removing one product does not leave its specifications attached
to another. Shared preferences deliberately apply across remaining products and
are hidden/cleared when no product service remains.

No shipping availability is claimed. Delivery is a request requiring review,
with the city/area collected for assessment. Addresses, carrier selection and
promised fulfillment arrangements are deferred until PMT confirms availability.

### Native Summary capabilities and limitation

The existing Summary continues to group answers into native page review cards,
with native Edit navigation and the unchanged responsive presentation. Labels
now explicitly distinguish product categories, deadline certainty, event-date
certainty, access status, measurement certainty and mounting restrictions.

The installed Summary offers `include_extras: ["html"]`, but enabling it and
rereading the saved setting did not display the HTML section headings in the
actual browser review. That experiment was reverted. Native Edit button text is
hard-coded by this installed implementation; there is no exposed per-group label
setting. Thus custom group headings and renamed Edit buttons are **not** claimed
as implemented. Clearer review guidance and field labels were added instead.
No unmanaged JavaScript, plugin-file edits, custom review renderer, new styling,
or artificial hidden fields were introduced to work around the limitation.

### Functional test results

All data was synthetic. Only exact test searches within form 13 were read.

| Entry / test | Verified result |
| --- | --- |
| 47 — products only | Standalone order hid event-only questions; invitations and decals persisted; native Venue skip produced four stages; tentative May 1, 2027 completion deadline and delivery request stored |
| 47 — changed categories | Entered banner and apparel answers, then deselected them; both were absent from review and empty in the saved entry |
| 47 — navigation | Summary Edit returned to Services and retained relevant answers; Back from Contact returned to Inspiration without stopping at Venue |
| 48 — full installation | Five stages; unknown event date accepted; estimated 16 × 8 × 12-foot dimensions, unconfirmed access, load-in notes and mounting restrictions stored |
| 48 — removed all products | Added then removed a product service; product specifications, shared material preferences, artwork status and fulfillment answers did not remain in review or storage |
| 49 — mixed mobile request | Décor plus banners, signage, apparel and other products; tentative June 12 event date remained distinct from confirmed June 10 product deadline; venue questions retained for installation Not sure |
| 49 — confirmed venue information | Confirmed access and measurements stored with 10 × 5 × 8-foot dimensions and freestanding-only mounting restrictions |
| 50 — changed installation/deadline | Filled installation answers and a known product date, then changed to No installation and Need guidance/no date; old date, height, access, restrictions and venue acknowledgement were absent from review and empty in storage |
| 50 — changed product | Removed apparel and selected other products; old apparel answer was cleared, new product specification retained |
| Required product validation | Blank artwork availability, deadline status, fulfillment and setup intent blocked progression; a confirmed/tentative deadline required its date |
| Required installation validation | Setting, access status, measurement certainty, mounting restrictions, approval status and acknowledgement blocked progression when missing |
| Contact validation | Invalid email and missing privacy consent blocked submission; correcting them permitted confirmation and entry storage |
| Date controls | Native calendar selected and persisted event/product dates through keyboard and pointer interactions |
| Responsive | Desktop 1440×1000, tablet 820×1180 and mobile 390×844 checked; no horizontal document overflow; mobile review stacking and keyboard-operated controls retained |
| Console | Completed flows had no JavaScript console errors; existing Hostinger widget warnings remain unrelated to the form changes |

All four completed browser tests displayed the existing staging confirmation.
No outbound action was added. The form is still administrator-only. Synthetic
entries 47–50 remain for review; no entries or uploads were deleted.

Upload/security settings were compared exactly against the tested baseline;
unchanged file type/size limits and protected-download behavior were not
needlessly retested. The initial integration's positive/negative upload tests
and anonymous-download check remain the recorded evidence. Full screen-reader
certification, alternate-role access, and the Oxygen Doctor/editor recovery
investigation remain outside this logic-only pass.

### Release state

This refinement remains on the existing development branch. Both WordPress
pages are unpublished, and the original publication gates still apply. No
production access or changes occurred. The new configuration is in WordPress;
this Git record is not an Oxygen or Formidable backup/export.

## Final inquiry UX refinements — November 19, 2026

Implemented the owner's requested finishing pass on form **13**, its dedicated
style **4685**, and Oxygen inquiry draft **4662**. The approved visual direction,
native Summary/Edit controls, and conditional four-/five-stage flow remain.
No writes targeted source form 3, homepage 4640, shared components, production,
payment settings, public notification actions, or staging access restrictions.

### Configuration capture and rollback

Before modifying choices, captured the current 78 fields, form settings, sole
confirmation action, dedicated style, and inquiry element tree. Local files are
in the Git-ignored `private/` directory and contain configuration only, without
entries, credentials, or customer records:

- `form13-final-ux-before-20261118.json` — original configuration snapshot.
- `form13-final-ux-rollback-20261118.json` — targeted native field updates,
  Oxygen text/label operations, and original style settings for restoration.
- `form13-final-ux-after-20261119.json` — saved configuration after refinement.

The before snapshot's SHA-256 is
`A2D283E3AF733448B786E913F271B90D47C89ECEC0289E23F813A5AF84F339BD`.
JSON round-trip, target IDs, and rollback field/style values were verified
against the snapshot. These are local configuration captures, not an official
Formidable XML export, complete WordPress backup, or Git-backed recovery system.
No live rollback was applied during testing.

To roll back, first coordinate open editor sessions and reread current state.
Apply the saved targeted field updates through `formidable-forms/update-field`,
restore style 4685 through `update-style`, and apply the saved operations through
Oxygen `edit-post` on 4662. Do not overwrite later owner edits. Reread and preview
after restoration. No entry migration, deletion, or page publication is needed.

### Changes

| Target | Implemented refinement |
| --- | --- |
| Field 163 | Standalone custom-product order is the first actual choice; Bridal Shower added; other occasions grouped in a more useful sequence. All pre-existing choice values retained. Placeholder now says event or order type. |
| Field 198 | Replaced the broad Under $1,000 choice for new inquiries with Under $250, $250–$499, and $500–$999. Higher ranges and I'm not sure yet retain their values. Help distinguishes product/combined décor budgets from overall event spending and states that ranges are not quotes or installation minimums. |
| Fields 167 / 191 | Customer-facing wording now says Décor coordination and Décor coordination support. The service still stores `Event planning or coordination`, preserving the existing conditional match. |
| Field 184 | Replaced postcode/collection terminology with ZIP code and pickup/delivery area. No new address requirement. |
| Field 230 | Pickup requested is the display label; stored `Pickup / collection requested` remains unchanged. |
| Field 205 | Décor breakdown or pickup window, with matching date guidance. Validation and installation conditions remain unchanged. |
| Style 4685 | Labels/base text 15→16px; helper text 13→14px; field spacing 24→28px. Error borders use wine `#7c2635`, input text charcoal `#24211f`, and a subtle `#fffaf8` error background. Existing error message colors and accessible markup retained. |
| Upload presentation | Scoped rules make the native dropzone fill the form width, with 144px minimum message height on desktop and 132px on mobile. Helpers use 1.6 line height and 6px top separation. Upload handling and limits are unchanged. |
| Oxygen 4662 | Form headline now reads “Let’s start with your event or custom creation.” Introductory copy welcomes both audiences. Static overview says “Four steps. Five for installation,” marks Venue as IF / if needed, and Contact as stage 4–5. |

No condition or action references budget field 198. The old broad budget value
was not reassigned to a narrower meaning, and no historical entry was rewritten.
An older saved `Under $1,000` answer remains historical data; it is no longer a
selectable choice for a new inquiry. Entry editing remains disabled as before.

The Oxygen pass updated existing text controls and renamed the overview's
Structure label to `Inquiry — Conditional Stage Overview`. All **43** authored
elements retain descriptive labels. Rereading the tree verified unchanged node
types, child ordering, classes, HTML attributes, and shared component references.
The native Shortcode embed remains unchanged. Oxygen preview confirmed the form
and revised text render. The visual builder itself was not reopened in this pass.

### Validation and functional results

Native field requirements, conditional rules, date/time defaults, field order,
privacy consent, Summary configuration, and upload settings were compared with
the captured baseline and remain unchanged. Submit field 221 remains last.
There was no demonstrated need to change validation logic.

| Test | Result |
| --- | --- |
| Stage-local errors | Empty first-stage required fields showed only first-stage errors. Blank budget showed its error on Inspiration; Back to Services showed no budget error. |
| Venue errors and Back | Missing setting, access confirmation, measurement certainty, restrictions, approval and acknowledgement blocked advancement. Back to Inspiration did not display those later-stage errors. |
| Contact errors and Edit | Blank name, contact preference, email and consent blocked submission. Summary Edit to the first stage did not carry those contact errors onto it. |
| Error accessibility | First invalid input received focus; `aria-invalid=true` and `aria-describedby` pointed to its error. Wine error border was confirmed in computed browser styling. Full screen-reader certification was not performed. |
| Entry 51 — products only | Invitation order, pickup request and Under $250 persisted. Four stages, no installation questions, native confirmation, and normal stored entry verified. |
| Entry 52 — event installation | Bridal Shower, unknown event date, décor coordination, $2,500–$4,999, estimated 12×6×10-foot space, unconfirmed access and pending approval persisted. Five-stage flow and installation requirements verified. |
| Entry 53 — mixed / mobile | Sweet 16 with tentative June 12, 2027 date, décor and banner request, delivery request and installation Not sure retained the venue stage. Partly confirmed access/measurements and restrictions persisted. |
| Smaller ranges and Edit | $500–$999 was accepted and shown in mixed review. Native Edit returned to Inspiration; changing to $250–$499 retained venue answers and appeared in review and saved entry 53. |
| Stale answers | Apparel specifications were filled, then apparel deselected in the mixed request. They disappeared from review and were empty in entry 53. |
| Optional times | Untouched event start/end and setup access/deadline all stored as empty strings in entry 52. Native AM selectors do not create a time without hour/minute values. No artificial defaults added. |
| Responsive | Actual browser inspection at 1440×1000, 768×1024 and 390×844; no horizontal document overflow. Native mobile Summary stacking and Edit controls retained. |
| Upload proportions | Native dropzone measured approximately 739×147px on desktop and 277×134px on mobile; visual checks confirmed readable instructions and preserved editorial styling. |
| Console | No JavaScript errors in completed flows. Existing authenticated Hostinger widget warnings remained. |

Only synthetic inquiries and exact test-entry searches were used. Entries
**51–53** remain available for administrator review; no records were deleted.
The existing confirmation appeared after each submission. Actions were rechecked:
**4684**, the save-and-confirm action, is still the sole action. No email,
spreadsheet, webhook, payment or other outbound action was added or enabled.

### Visitor visibility and remaining limits

Anonymous browser checks found no WordPress admin bar or Hostinger Agent UI on
the returned WordPress 404 page for the unpublished inquiry. The staging root
returned a 403 browser challenge. The authenticated preview does show those
administrator tools. A complete ordinary-visitor rendering of this inquiry
cannot be tested while it remains a draft restricted to administrators; access
restrictions were not relaxed to obtain that test.

Upload type/size restrictions, protected-file configuration and privacy consent
were unchanged; the previously recorded upload/security tests remain applicable.
No new upload was needed for this presentation-only pass. The Oxygen Doctor
investigation was not reopened, and successful previewing is not a new claim of
visual-editor recovery.

Final connection check: `https://oxygen.pmtparty.com`, WordPress **7.1.5**,
Oxygen **6.2.2**, PHP **8.5.12**. Both pages **4640** and **4662** remain **drafts**.
Form 13 remains administrator-only with protected uploads. The existing
publication gates and separate approval requirement still apply. Preview:
`https://oxygen.pmtparty.com/?page_id=4662&preview=true`.

## Welcoming Venue & Setup assessment — November 19, 2026

Implemented on staging form **13** and inquiry draft **4662**. The venue stage
now opens with a short preliminary assessment and a native conditional choice
to share more details. No separate follow-up form, page, custom accordion,
JavaScript routing, or CSS change was introduced. Dedicated style **4685** was
compared exactly before/after and is unchanged.

### Capture and restoration

Before field changes, captured all 78 existing fields, form settings, action,
style and Oxygen inquiry tree in the local Git-ignored file
`private/form13-venue-before-20261119.json`. SHA-256:
`EBAD4920026D4E2F11BD4F1566FAA39459B3DC71941D02CBEE05CAE36DB04251`.
The completed configuration is in `private/form13-venue-after-20261119.json`.
These files contain configuration only, without entries or credentials.

The final restoration payload is
`private/form13-venue-rollback-ready-20261119.json`; use it instead of the earlier
preliminary rollback file. It restores the 21 changed existing field records,
the progress-title option and four Oxygen text edits through native abilities.
It retains new fields 237–239 and their data: the rollback makes them optional
and hides them with documented native all-match conditions requiring field 192
to equal both its mutually exclusive Yes and No choices. It does not delete
fields or entries. Original values and target IDs were checked against the
snapshot. Coordinate editor sessions and reconcile any later owner edits before
applying this rollback; no live rollback was needed during verification.

### Event categories and stored values

Field 163 now offers separate **Bar Mitzvah** and **Bat Mitzvah**, plus
**B'nai Mitzvah / Joint Mitzvah**, **School or Community Event**,
**Gala or Fundraiser**, and **Grand Opening / Brand Event**. There are 26 actual
choices, including Standalone custom-product order and Other. Existing useful
occasions were retained. **Quinceañera** is corrected as a display label while
its existing stored value remains `Quinceanera`.

Audited every field dependency on 163 and the sole form action. Conditions use
only Standalone custom-product order and Other; neither value changed. Field
182's Other description and all those conditions remain exactly unchanged.
The retired combined mitzvah choice was not relabeled as one particular event
or migrated: historical `Bar Mitzvah or Bat Mitzvah` answers retain their original
meaning. New inquiries use the distinct choices. No historical entries were
updated, exported or removed.

### Preliminary questions and optional details

The native page break 199 still depends on setup intent 192: Yes and Not sure
retain the venue stage; No skips it. The progress title, stage introduction and
Oxygen overview now say **Venue & Setup**. Initial guidance welcomes uncertainty
and explains that measurements, loading and venue requirements are confirmed
later, before finalizing the setup plan.

| Field | Requirement and behavior |
| --- | --- |
| 202 — indoor/outdoor setting | Still required for a venue inquiry: Indoors, Outdoors, Both or I'm not sure yet. The unsure label keeps the existing `Not confirmed` stored value. |
| 237 — `pmt-setup-complexity` | New required question: straightforward ground-level setup, unusual conditions, or I'm not sure yet. Guidance flags high ceilings, overhead décor, attachments, stairs/access and venue rules. |
| 239 — `pmt-setup-risk-indicators` | New required checklist only when 237 indicates unusual conditions. Captures high/elevated décor; hanging/wall/ceiling attachments; stairs/elevators/loading/access; venue restrictions/limited setup time; outdoor surfaces/weather; or other requirements to discuss. |
| 214 — venue approval | Still required in the preliminary assessment, moved ahead of detailed questions. Friendly confirmed/pending/unsure labels retain all existing stored values. A customer's venue approval answer does not mean PMT has inspected or approved the installation. |
| 238 — `pmt-venue-details-optin` | New optional radio, titled “Have more venue details to share? (Optional)”. Only Yes reveals the technical questions. Blank or Not right now / I'm not sure keeps them hidden. |
| 201 — optional guidance | Reused the existing non-input HTML note as guidance for the revealed details. Its former products-only note was on a page that products-only requests skip. No collected answer was removed. |
| 203–210, 212, 215 | Existing setup/access times, breakdown window, loading, route, width/depth/height, measurement notes and detailed approvals retain their IDs and remain optional inside the revealed group. Numeric bounds, units and time defaults remain unchanged. |
| 231 — access confirmation | **Changed from required to optional**, shown only in the additional-details group. |
| 213 — mounting/restriction details | **Changed from required to optional**, shown only in that group. Required preliminary risk questions still flag known mounting or venue restrictions. |
| 211 — measurement certainty | **Changed from unconditional venue requirement to conditional requirement**: appears and is required when any width, depth or height is greater than zero. Blank measurements need no certainty answer. This preserves the distinction between estimates and confirmed measurements when numbers are supplied. |
| 216 — preliminary acknowledgment | Remains required: “I understand venue details and approvals need to be confirmed before PMT finalizes the setup plan.” Uses this new statement as its stored value rather than saving the former stronger wording under a shorter label. Existing acknowledgments are not rewritten. |

All existing technical field IDs are retained. Technical questions are revealed
through native Formidable field conditions, not an unmanaged collapsible block.
There are now **81** field records. Native submit field 221 remains last.

The acknowledgment helper states that the inquiry does not replace venue checks
or responsibilities agreed during planning and contracting. No contract or
separate responsibility terms were edited. PMT's planning gate remains:
confirm accurate dimensions, mounting methods, loading/access, required equipment
and venue approvals before finalizing an installation plan. This inquiry gathers
early indicators; it does not automate or certify that later approval process.
Unknown or missing technical details must be followed up, not treated as approval.

### Closing copy and Oxygen preservation

Contact-stage copy warmly welcomes the request and explains that an inquiry
does not guarantee availability, pricing or a booking. Summary guidance now
invites a quick check of the relevant groups without implying that every venue
detail must already be known. The native Summary renderer, Edit navigation,
privacy consent, upload restrictions, CAPTCHA and anti-spam settings are unchanged.
Notification and confirmation actions were not edited.

On Oxygen 4662, only text in elements 104, 115, 127 and 128 changed: the overview
and venue guidance match the preliminary setup assessment. Native custom labels,
classes, hierarchy, embed and component references remain intact. Saved trees
for homepage 4640 and header/footer components 4642/4648 compared identical.
Original form 3's settings also compared identical; no writes targeted it.

### Verification

Only synthetic data and exact test searches in form 13 were used. Before each
submission scenario, rechecked that 4684 remained the sole save-and-confirm
action, with no email, webhook, spreadsheet or payment action.

| Entry / test | Verified outcome |
| --- | --- |
| 54 — full setup / Bar Mitzvah | Opted into details; estimated 12×6×10-foot space, loading and mounting notes saved with pending venue approval. |
| 55 — simple ground-level / Bat Mitzvah | Technical details and risk checklist stayed hidden; no measurements or loading confirmation were required. Saved successfully. |
| 56 — complex / joint mitzvah | High/elevated décor, hanging attachments, stairs/loading/access and venue restriction flags saved with approval pending, without demanding measurements. |
| 57 — unknown / school or community | Unsure setting, risks, approval and installation intent accepted; five stages retained and optional technical questions hidden. Earlier Other description was cleared when the category changed. |
| 58 — products only | Four-stage flow; Venue skipped during forward and Back navigation; new risk fields, venue acknowledgment and technical fields empty in storage. |
| 59 — mixed / gala / mobile | Décor and banner request retained venue assessment. Summary Edit returned to Venue. Switching optional details off and changing unusual setup to straightforward cleared old dimensions, certainty, loading, mounting, access-confirmation and risk-checklist answers in review and saved entry. Product details and pending approval remained. |
| Required validation | Empty setting, setup-risk status, approval and acknowledgment blocked advancement. Yes to unusual conditions required at least one risk selection. Entering dimensions required measurement certainty. |
| Numeric validation | Height -1 failed native browser range validation against the retained 0.1 minimum and kept the user on Venue. Clearing it permitted advancement; no certainty answer was required for blank dimensions. |
| Optional-details choice | Selecting Yes while leaving every technical answer blank was accepted; no hidden technical requirement prevented the inquiry. |
| Categories | Grand Opening / Brand Event worked through review. Quinceañera selected with stored value `Quinceanera`; all 26 choices present and Other's conditional description worked. |
| Review / confirmation | Native Summary displayed relevant preliminary answers and any supplied technical details; all six submissions reached the unchanged staging confirmation and normal saved-entry status. |
| Responsive | Desktop 1440×1000, tablet 768×1024 and mobile 390×844 checked. Mobile label/helper wrapping and controls visually inspected; no horizontal overflow. No style changes needed. |
| Browser | No JavaScript console errors in completed flows. Existing authenticated Hostinger widget warnings/overlay remain unrelated. |

Entries **54–59** remain for administrator review. No entries or uploads were
deleted. An additional validation-only walkthrough was not submitted.
The earlier known synthetic entry 52 was checked by ID and still contains its
original acknowledgment statement; the new wording did not rewrite that answer.

Afterward, exact comparisons confirmed unchanged style 4685, action 4684,
upload 197, privacy consent 219, CAPTCHA 180, page-break routing 199, setup intent
192, Other description 182 and submit 221. Only the form-level progress title
changed; administrator access, protected uploads and anti-spam remain intact.
Oxygen's native preview rendered the real form and updated overview. Both pages
**4640** and **4662** remain **drafts**. Production was not accessed or modified.
Guest rendering of the unpublished form and visual-editor recovery were not
claimed as tested by this pass. This Git record does not back up the runtime
configuration; the private captures above are separate local artifacts.

## Event-category ordering follow-up

Date: November 19, 2026. Completed before the services refinement, in response
to the owner's additional event-category instructions. Only field 163's choices
changed. Its configuration and native rollback payload were captured in ignored
`private/form13-categories-before-20261119.json` before the edit.

The first five choices are Wedding, Engagement, Bridal Shower, Sweet 16 and
Quinceañera. Standalone custom-product order is sixth and Corporate Event seventh,
followed by Grand Opening / Brand Event, Gala or Fundraiser and Conference.
Baby Shower was already present and remains. Added Baptism, Gender Reveal,
Retirement Celebration and Family Reunion, for **30 actual choices** in total.
Baptism, Christening, Communion and Confirmation precede Bar Mitzvah, Bat Mitzvah
and B'nai Mitzvah / Joint Mitzvah, as requested. Other remains last.

All preexisting choice values from the venue milestone were preserved, including
`Quinceanera` behind the corrected display label. Dependency inspection found
conditions on Standalone custom-product order and Other; both values and their
rules stayed unchanged. Native readback and Chrome checks confirmed ordering,
new options, Other's description and standalone-event question hiding. No
historical entries were changed. This ordering is included in the services
baseline below and was not altered by that refinement.

## Services and custom pieces refinement

Date: November 19, 2026. Target verified again as `https://oxygen.pmtparty.com`:
WordPress 7.1.5, Oxygen 6.2.2, PHP 8.5.13. All writes used native Formidable
abilities or documented Oxygen element properties. No plugin, server, production,
payment, notification or access-setting changes were made.

### Capture and rollback

Before changes, captured form 13, its 81 fields, confirmation action, style 4685
and inquiry tree in ignored `private/form13-services-before-20261119.json`.
SHA-256: `63ECB3C20AF22A789AE47952D44950DA0FCF7A2D23A774BE815B6FBC0C89ED94`.
Prepared `private/form13-services-rollback-20261119.json` with supported targeted
updates for the 21 modified existing fields and the four Oxygen elements.
Every rollback property was compared against the baseline and matched.

Rollback retains new field IDs 240–245, makes them optional and hides them with
native conditions; it does not delete fields or entries. Reverting field 168's
checkbox type to its old radio type would need review of any newer multi-choice
entries before editing those entries. No historical answer migration is part of
rollback. Re-read the current state and preserve newer work before applying it.
Rollback was validated as a payload, not executed against the completed form.

After verification, captured `private/form13-services-after-20261119.json`.
SHA-256: `BB5A6E0781932E61CAC7B9538C07D260D95BF7244B6C06D23804016A63F22179`.
These are private local configuration captures, not entries, database dumps or
Git-backed runtime backups. All four named private files are ignored by Git.

### Fields and conditions

Six new native optional fields were added. No existing field was deleted. There
are **87 field records**, including layout/HTML/page-break fields, and native
submit 221 remains last. The current visual style 4685 was not changed.

| Field | Purpose and conditions |
| --- | --- |
| 240 — `pmt-rental-pieces` | Optional rental checklist for Rentals: artificial floral centerpieces, cherry blossom trees, candelabras, mirror displays/easels, arches/backdrop structures, drapery/display equipment, marquee numbers, audio guest book, specialty pieces and Other/Need recommendations. Examples are subject to availability and estimate confirmation. |
| 241 — `pmt-balloon-styles` | Optional checkbox for Balloons: garland, arch, columns, clusters/centerpieces, backdrop/larger installation, Other/Need recommendations. |
| 242 — `pmt-decor-focus` | Optional table styling/linens/runners, chair décor, or other décor choice. Appears for event décor, florals, artificial floral rental selections or candelabras. |
| 243 — `pmt-banner-formats` | Optional multi-choice formats: large printed backdrop, retractable standing banner, X-stand, standard vinyl/fabric banner, Other/Not sure. Appears for Custom Banners **or** a printed backdrop in 170. Supporting 8×8 ft, 31.5×80 in and 30×69 in dimensions are examples, not required sizes or guarantees. |
| 244 — `pmt-display-equipment` | Optional Yes / I have my own / Not sure question for signage, banners or backdrops. Explains client-owned graphics and returnable PMT-owned rental equipment, subject to the agreed estimate. No mandatory ownership decision. |
| 245 — `pmt-event-website-brief` | One optional description for the new Event websites & digital RSVP service: occasion, desired guest experience and timing. Scope, features and pricing require discussion; no fixed package, online payment or integration promises. |

Existing fields were improved and reused:

- Service checklist **167** keeps all existing stored values and adds the website
  option. Its helper explains that floral/backdrop rental requests do not need
  a second Rentals selection. This is a flexible estimate inquiry, not a catalog
  or reservation system.
- Floral fields **171/172/177** retain material choices and approximate quantity.
  They show once for the Florals service **or** artificial floral centerpieces in
  240. Guidance explains artificial rentals, fresh arrangements to keep, possible
  fresh-flower cost differences, unusual requests and separate price/availability
  confirmation. No Rent/Buy field was added.
- Balloon colors/details **169** remain; its helper accepts an optional known
  garland length or installation size. No technical measurements are required.
- Backdrop preferences **170** keep their choices. Printed backdrops share **243**
  and the existing banner quantity/size/wording field **223**, avoiding a duplicate
  banner questionnaire. Shared product fields **222/227/189/228/229/230** now also
  recognize that printed-backdrop selection. Artwork, deadline certainty, actual
  deadline **233**, fulfillment and setup intent otherwise retain their validation
  and stored choices.
- Signage **168** became a native optional checkbox. It offers printed guest
  charts, framed charts, mirrors, welcome signs, memorial/photo displays, table
  numbers, bar signs, directional signs and custom guidance. Old stored values
  `Framed chart on an easel`, `Mirror with names in vinyl` and
  `Other / please advise` are preserved behind clearer labels. Existing **224**
  collects optional quantities, sizes and wording; **225** keeps the units.
  A framed 24×36-inch chart is described as an example, not a fixed product.
- Rental details **190** moved beside 240 and stays an optional quantity/additional
  request area. Helpers discourage repeating florals, backdrops or signage already
  requested elsewhere. No separate rental quantities are required for floral work.
- Table count **174** now depends on table styling, florals, artificial floral
  rentals or candelabras, not broad décor alone. Its helper allows skipping it if
  the centerpiece quantity already covers the request. Chair count **176** appears
  only for Chair décor in 242. Optional runners **175** appear for table styling.
  None of these quantities became mandatory.
- Budget heading **232** and helper **198** now cover all requested services and
  products, including digital work if selected, rather than the entire event
  budget. The range values are unchanged. The final label is **Budget range**:
  the initially longer wording crowded the native mobile Edit button, so it was
  shortened and visually rechecked without changing CSS.

### What happens next and preserved objects

Reused Oxygen 4662's existing support group **126** and text elements **123–125**
for **What happens next?** The copy explains inquiry review, clarification,
itemized custom products/rentals/décor/delivery/installation/breakdown and fees,
estimate revisions, the later PandaDoc agreement after scope/price approval,
and booking/payment arrangements under that agreement. It expressly says the
inquiry does not guarantee availability, reserve inventory, fix a price or book.
This is explanatory copy only; no PandaDoc, contract or payment action was added.

Only those four nodes' content/custom names changed. Exact tree comparison,
after excluding the intended text/name edits, confirmed identical hierarchy,
classes, settings, IDs and references. All authored nodes retain descriptive
Structure labels; Oxygen's root document node is not an authored element.
The native Shortcode embed **142** remains unchanged. Saved trees for homepage
**4640** and components **4642/4648** are identical to the baseline.

Original form **3** was never written; its settings compared identical. Form 13's
form-level settings, action 4684 and style 4685 also compared exactly unchanged.
The approved first-stage questions, Venue & Setup fields and routing, installation
intent, required/optional venue safeguards, privacy 219, upload 197, CAPTCHA 180,
native Summary 220 and submit 221 compared unchanged. Both WordPress pages remain
**drafts**; form 13 remains administrator-only with entry editing disabled.

### Functional and responsive verification

Rechecked the sole confirmation action before every submission scenario. Used
synthetic browser inquiries and exact email searches restricted to form 13;
no unrelated submissions were listed. Entries **60–69** all reached the existing
staging confirmation and normal saved status 0, not draft or spam.

| Entry / scenario | Verified result |
| --- | --- |
| 60 — artificial florals | Material and eight centerpieces saved without requiring Rentals; five-stage setup flow worked. No irrelevant chair quantity. |
| 61 — fresh florals | Fresh selection, ten centerpieces and floral preferences saved; no forced purchase/rental decision. |
| 62 — balloon garland | Garland choice, colors and optional approximate length appeared in Summary and storage; unrelated table questions stayed hidden. |
| 63 — large printed backdrop | Selecting printed backdrop without Custom Banners exposed shared banner/production questions; 8×8 request saved. Missing artwork/deadline answers blocked advancement on Services. |
| 64 — retractable and X-stand | Both formats, example dimensions and display-equipment request saved in a products-only four-stage flow. |
| 65 — framed seating chart | 24×36 dimensions, inches and display equipment saved; raw choice retained `Framed chart on an easel`. |
| 66 — mirror and display rental | Mirror signage and mirror/easel rental saved together; raw signage choice retained `Mirror with names in vinyl`. |
| 67 — rental equipment | Blossom trees, arch, marquee and audio guest book saved with optional quantities. Unrelated table/chair counts stayed hidden. |
| 68 — event website | Brief and website service saved without physical-product requirements. A previously selected/removed banner and display-equipment answer were empty in storage. |
| 69 — mixed / mobile / changed answers | Rental artificial florals reused the existing floral questions. Native Summary Edit returned to Services. Removing florals, printed banner, balloons, website and table/chair focus cleared 12 obsolete field answers in Summary and storage. Signage, drapery, audio guest book, shared artwork and display-equipment answers remained. Back to Venue and forward to Contact retained the approval answer. |

Desktop **1440×1000**, tablet **768×1024**, and mobile **390×844** were checked
for overflow and inspected visually, including new choices, wrapping, helper text,
the estimate guidance and native review. No horizontal overflow; no stylesheet
change was needed. A final non-submitted walkthrough verified the shortened
mobile Budget range label clears the Edit button. The browser was returned to
the opening authenticated draft preview afterward.

Oxygen's native preview rendered the genuine form and workflow copy. Console
inspection found one Google iframe **report-only** Content Security Policy
message, with no blocking action, plus existing authenticated Hostinger warnings.
These did not prevent the ten submissions. The administrator bar and Agent widget
remain visible in the administrator test session; no access restrictions were
relaxed to test a public visitor. No critical form JavaScript failure was observed.

### Limits and next-release considerations

- Native conditions clear answers when a category becomes hidden. Shared free-text
  specifications are intentionally retained while that category still applies;
  they are not automatically rewritten if one banner/sign format is replaced
  within the same category. Customers should review that text using Summary/Edit.
- Inventory examples do not establish stock, rental reservations or final pricing.
  PMT still confirms equipment ownership/returns, scope and fees in its estimate
  and agreement. Initial venue unknowns still require later planning follow-up.
- Upload/privacy and anti-spam settings compared unchanged; this pass did not
  repeat the earlier file-security tests or reopen the Oxygen visual editor.
  Saved native labels and frontend rendering were verified through supported tools.
- Public rendering, release notification recipients, staging/indexing protection
  and publication approval remain release gates. No page was published, and no
  outbound notification, payment or live integration was enabled.

## Delivery and pickup refinement

Date: November 19, 2026. Target verified again as `https://oxygen.pmtparty.com`
on WordPress 7.1.5, Oxygen 6.2.2 and PHP 8.5.13. Scope: form 13's fulfillment
question and native conditional grouping. Oxygen page 4662 continues to embed
the same form; no Oxygen layout write was needed.

### Saved configuration and wording

Captured the current form, fields, actions, style and page trees before editing:
`private/form13-fulfillment-before-20261119.json` (ignored), SHA-256
`1CE4F6E61F668A8BD5031860C928BA1E0454304303DCFF4EF69C3AC88BD3F0A5`.
The original payload and completed rollback reference are in
`private/form13-fulfillment-rollback-20261119.json` and
`private/form13-fulfillment-rollback-ready-20261119.json`.
Rollback restores field 230's saved properties and moves it outside the section;
the new native layout markers can remain hidden rather than being deleted.
All rollback values were checked against the captured field, with `in_section: 0`
explicitly restoring its former ungrouped state. No rollback was executed.

Field **230** now asks exactly:

> How would you prefer to receive your custom products?

| Display order and label | Preserved stored value |
| --- | --- |
| 1. Delivery by PMT | `Delivery requested — please confirm availability` |
| 2. Pickup by arrangement | `Pickup / collection requested` |
| 3. I'm not sure — please advise | `Need guidance` |

The default remains empty. Its native description appears beneath the options:

> We'll confirm the available arrangements and any related costs in your personalized estimate.

No field depended on 230 before the change. The sole confirmation action had no
fulfillment-dependent condition. No stored choice value or historical entry was
migrated, and no shipping or other fulfillment option was introduced.

### Native conditions and placement

Field 230 moved from order 160 to **192**, immediately after setup field **192**
(which remains at order 190). Two non-input Formidable layout records provide
native grouping: plain, non-repeating section **246** at order 191 and end marker
**247** at order 193. These are not new questions or a new form. The total is now
**89 field records**; native submit 221 remains last.

The section is shown only when setup 192 equals its existing
`No — products only / collection` value. Field 230 retains its existing OR rules
for the six physical-product services or printed-backdrop selection in 170.
This combines product relevance and no on-site setup without JavaScript, a
calculated helper, or a dependency on answering the artwork question first.
The existing required flag on 230 is unchanged and applies only when visible.
No new required question was added.

Yes, Not sure yet or blank setup hides the section and clears fulfillment. No
setup with no relevant physical product also hides and clears 230. The setup
field itself, its choices and the Venue page-break routing are unchanged:
No retains four stages; Yes and Not sure retain five. Uncertain installation
needs are left for PMT's follow-up rather than forcing a delivery/pickup choice.

Section 246 has a descriptive administrator label but no visible heading.
Its native Custom HTML template omits only the default heading line: Formidable's
Label Position None hid the words but initially retained a 35-pixel heading
spacer. Removing that unused line left a zero-height section when the product
question is hidden. The standard section container and native child rendering
remain, with no custom CSS or JavaScript. Field 230's template, typography,
classes, spacing and responsive style remain unchanged.

### Verification and preservation

Before every submitted scenario, verified that 4684 remained the only action,
with the unchanged staging save-and-confirm message. Used synthetic data only
and exact test searches within form 13. All five entries saved with normal
status 0 and reached the existing confirmation.

| Entry / test | Result |
| --- | --- |
| 70 — Delivery by PMT | Delivery first, no radio preselected, exact helper below options. Blank visible fulfillment blocked advancement on Services. Summary used the new label; entry retained the original delivery value. |
| 71 — Pickup by arrangement / mobile | Correct label and legacy pickup value saved. Native Summary Edit restored the selected choice. Back from Contact reached Inspiration and skipped Venue in the four-stage path. |
| 72 — Please advise / printed backdrop | Printed backdrop exposed fulfillment without requiring Custom Banners as a second service. Summary used the new guidance label; stored value remained `Need guidance`. |
| 73 — Mixed installation / changed setup | Delivery selected under No disappeared under Yes. Returning to No showed all choices blank. A subsequent pickup choice cleared under Not sure. Final Yes flow completed five stages; Summary and saved entry contained no fulfillment answer. Summary Edit also kept fulfillment hidden for installation. |
| 74 — Physical products removed | Removing Custom Banners while keeping an event website request hid fulfillment despite No setup. Four-stage flow submitted without requiring it, and old delivery values were empty in storage. |

After the section-spacing correction, rechecked reveal/hide/clear behavior and
confirmed zero height when no product question applies. Desktop **1440×1000**
and mobile **390×844** screenshots showed the exact wording, clear options and
helper wrapping with no horizontal overflow or preselection. The browser was
returned to the opening authenticated draft preview. This pass did not repeat
unrelated upload/security tests or operate the Oxygen visual editor.

Exact native comparisons showed **230 was the only existing field changed**.
Setup 192, Venue & Setup, event/service questions, Summary, privacy/upload and
anti-spam fields remain unchanged. Form-level settings, style 4685, action 4684
and original form 3's settings compared identical. Trees for inquiry 4662,
homepage 4640 and components 4642/4648 compared identical. Both pages remain
**drafts** and form 13 remains administrator-only. Production, payment settings,
notification actions and staging restrictions were not modified.

The final ignored capture is `private/form13-fulfillment-after-20261119.json`,
SHA-256 `00A7F787E7904361396FF95DE0D2EC7A2FEBEC7322CA6B027E2C3A23606EEF03`.
Git records the work and checks, not the runtime configuration or submissions.
No functional failure remains from this refinement. Guest/public validation
still awaits the existing publication and access-protection release gates.
