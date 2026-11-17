# Staging refinement and Oxygen Doctor investigation

Date: November 17, 2026. Target: https://oxygen.pmtparty.com only.

## Current implementation

| Object | ID | Status |
| --- | --- | --- |
| Premium editorial homepage | 4640 | Unpublished draft |
| Event inquiry page, slug `event-form` | 4662 | Unpublished draft; layout prepared, real form pending |
| Navigation component | 4642 | Used by both drafts; no sitewide condition |
| Event inquiry CTA component | 4645 | Used by homepage |
| Footer component | 4648 | Used by both drafts; no sitewide condition |

Authenticated previews:
- [Homepage](https://oxygen.pmtparty.com/?page_id=4640&preview=true)
- [Event inquiry layout](https://oxygen.pmtparty.com/?page_id=4662&preview=true)

These are administrator draft previews, not public inquiry endpoints.
The future `/event-form/` slug is assigned but is not published or verified
as a public form URL. Publication requires the requested protection, indexing,
notification checks, and explicit approval.

## Changes completed through native Oxygen tools

- Applied native `meta.friendlyName` labels in the format
  `Section — Element Purpose` to every authored element.
- The initial naming-only pass covered 176 existing nodes. Before/after preview
  HTML and CSS were identical for the homepage and all three components.
  Tree differences were limited to the friendly-name field and its new parent
  metadata object where none existed.
- After additions/refinement, all 232 nodes have labels: homepage 138,
  navigation 23, CTA 6, footer 23, inquiry page 42. Repeated service, stage,
  caption, and mobile navigation elements have distinct names.
- Clarified the hero: “Event décor. Made personal.” Supporting copy names
  event styling, décor, and custom creations.
- Added service photography for weddings, Sweet 16s, baby showers, and corporate
  events. Replaced the repeated yacht portfolio image with a custom engagement
  backdrop. Replaced the custom-creations monogram concept with a real
  rose-cut invitation sleeve photograph.
- Removed customer-visible internal design and placeholder explanations.
  The unverified testimonial placeholder is now a practical planning-notes
  section, with no attributed quote, rating, or invented endorsement.
- Expanded navigation to Home, About, Services, Our Work, Custom Creations,
  Event Inquiry, and Contact. Added a native `details` / `summary` mobile menu.
  It uses browser-native disclosure behavior, without unmanaged JavaScript.
- Connected all inquiry links to the authenticated staging inquiry preview.
  No production `event-form` link remains in the page/component previews.
- Built the inquiry introduction, five-stage overview, supporting guidance,
  form container, and shared navigation/footer as native Oxygen elements.
  The page explicitly states that this staging preview is not accepting submissions.
  It contains no mock form fields and no unverified Formidable embed.
- Added 20 scoped classes and one nested focus rule in the
  `PMT Editorial Refinements` collection. Existing OxyMade selectors and
  variables were not changed.
- Added permanent Structure naming and session-coordination guidance to AGENTS.md.

The existing Cormorant Garamond / DM Sans system remains, with warm paper
`#f7f3ed`, soft white `#fffdf9`, charcoal `#24211f`, muted text `#625a53`,
wine `#7c2635`, brass `#88734e`, and line `#d8cfc4`. Existing fluid section
spacing is 64–128px and gutters 24–88px. New layout gaps use 12/16/20/24/32/40/64px.
Responsive rules use registered breakpoints 1119/1023/767/479px.
No new entrance animations were added.

## Photography

Reused existing staging media; no stock or generated event photography:

| Attachment | Use |
| --- | --- |
| 4244 | Existing yacht hero retained |
| 4395 | Existing candlelight portfolio image retained |
| Existing Gabrielle.jpg image | Wedding portfolio image retained |
| 3379 | Wedding reception service card |
| 4216 | Sweet 16 styling service card |
| 4136 | Baby shower décor service card |
| 4140 | Corporate event service card |
| 4138 | Custom backdrop portfolio image |
| 3911 | Rose-cut invitation sleeve showcase |

Source images were visually inspected. The current corporate image includes
existing promotional text; a clean original is preferable in a later crop review.
The invitation production-table photograph was inspected but not used.
No media files or customer data are committed to Git.

Add distinct birthday images, a clean corporate-event photograph, broader custom
product images (apparel, decals, seating charts, signage), and approved testimonial
text with source/attribution. Confirm publication rights before public release.

## Oxygen Doctor: investigation, not a verified repair

The owner reports that the editor recovers after about a minute and remains usable.
The recovery-test reply confirmed that all editor tabs were closed, but left
the recurrence and styling-result options in brackets. Those results are unknown.

Authenticated selector inspection found:
- Seven classes `hero`, `h1`–`h6` in OxyMade Headings.
- Each stores two typography values as strings:
  `font_size: "var(--h1)"` (matching its name) and `line_height: "1.2"`.
- Seven same-named classes in OxyMade Typography have empty properties and
  distinct selector IDs.
- The seven populated definitions therefore contain 14 property values. This
  is a stronger candidate for the reported count than duplicate names alone,
  but has not been matched against Oxygen Doctor's actual rejected paths.
- None of the homepage or three shared components directly references those
  14 OxyMade selector IDs.
- Rereads after the owner's reported save/reopen still show the same stored
  values. The final selector result is unchanged from the investigation baseline.

[OxyMade's 1.5.0 changelog](https://oxymade.com/changelog/) documents a related
heading font-size fix from plain strings to variable placeholders. Version 1.5.0
is installed here. Persisted older definitions are a hypothesis, not an
established cause. Do not delete duplicate names, run a bulk styling repair,
resync typography, or overwrite these selectors without tracing Doctor's
specific paths and preserving affected designs.

No global class deletion, OxyMade disabling, PHP change, reset, database
manipulation, or cache purge was performed. The warning is **still under
investigation**; its recurrence and styling impact are not verified.

## Verified runtime

- WordPress 7.1.4; Oxygen 6.2.2; PHP 8.5.12.
- OxyMade 1.5.0.
- Formidable Forms 7.0; Formidable Forms Pro 7.0.1;
  Conversational Forms 1.3; Visual Views 5.13.
- Breakdance Elements / Forms / WooCommerce for Oxygen each 1.1.0.
- WooCommerce 11.3.0; WP Fastest Cache 1.5.5 and Premium 1.7.6.

[Current Oxygen requirements](https://oxygenbuilder.com/documentation/troubleshooting/hosting-server-requirements/)
tie PHP support to WordPress compatibility.
[WordPress's server handbook](https://make.wordpress.org/hosting/handbook/server-environment/)
lists PHP 8.5 as supported for WordPress 6.9 and later.
[Oxygen 6.2 release notes](https://oxygenbuilder.com/oxygen-6-2-is-now-available/)
also document PHP 8.4/8.5 deprecation fixes. These sources do not establish
compatibility of every installed add-on or prove the absence of runtime errors.
No server logs or browser diagnostics were available to establish a PHP fault.

## Formidable: access and remaining implementation

The generic authenticated MCP discovery exposes no Formidable abilities.
The staging page search found no existing `event-form` page; this does not
establish whether the previous form itself exists in Formidable.

[Formidable's official MCP guide](https://formidableforms.com/knowledgebase/connect-formidable-forms-to-your-ai-agent-with-mcp/)
says version 7.0 includes the server and ability registration, controlled under
Formidable → Global Settings → MCP. This setting was not changed.

The earlier read-only review of the production form found contact information,
event type, guest count, venue, colors, requested services, conditional décor
details, event date, additional notes, and spam controls. No production form
submission was made. The later instruction prohibits further production access.

Still required through authorized staging admin access:
1. Find the existing form; record its ID and field IDs without reading entries.
2. Inspect actions, recipients, integrations, confirmation, and upload rules.
3. Duplicate the form, preserving the original and excluding historical entries.
4. Disable live actions on the copy and establish controlled synthetic testing.
5. Build the requested five stages: event; services; inspiration/decor budget;
   venue/installation; contact/review. Preserve applicable original questions,
   add estimates-versus-confirmed venue information, and bypass installation
   questions for print-only requests.
6. Embed the genuine form in Oxygen's native Shortcode element after verifying
   its form ID. Name it “Inquiry — Form Embed”.
7. Test conditional logic, required fields, navigation, private uploads,
   confirmation, entry storage, and controlled notifications.
8. Check staging access and indexing protections before requesting publication.
9. After approval/publication, replace preview inquiry URLs with the verified
   staging `/event-form/` URL.

No form ID is established, no form was duplicated, no notifications were changed,
and no synthetic submission was made in this pass. The form is not functional yet.

## Verification and limitations

Passed through official Oxygen tools:
- Both pages remain drafts; five other draft pages remain present.
- Full native element trees reread successfully and all labels persist.
- Shared component references render.
- Both page previews render; each has one H1, image alt attributes, no duplicate
  image sources, and no missing same-page fragment targets.
- Production inquiry links and internal placeholder notes are absent.
- Registered responsive breakpoints persist in the new selectors.
- CSS import returned no warnings; CSS file inventory reports an updated
  selectors-cache version.
- Active home page setting remains 0, header IDs [4618], and footer IDs empty.
  No new sitewide template conditions were activated.

Not verified:
- Actual visual-editor reopening, selecting elements, saving, and Doctor recovery.
- Desktop/tablet/mobile screenshots, keyboard/touch behavior, visual spacing,
  cropping, or interactive mobile-menu operation.
- Browser console/network errors, PHP logs, or CSS HTTP/cache delivery.
- Formidable functionality or notification safety.

The user requested Playwright MCP exclusively for browser work and manual
authentication. At the final tool-registry check, this conversation did not
expose any Playwright browser navigation/snapshot/tab tools, despite the
owner reporting them in local CLI. No direct Playwright navigation call could
therefore be made; there is no Playwright connection error to report.
Do not use another browser integration or handle credentials as a workaround.
Resume in the session exposing Playwright, open staging admin visibly, and
allow the owner to authenticate manually.

## Change ownership and next milestone

These Git documents record changes; they are not Oxygen exports, WordPress
backups, or Formidable configuration backups. Prototype files are ignored.
Use native Oxygen revision/recovery facilities or an approved private backup
for layout rollback; a Git revert does not undo WordPress changes.

Next milestone: establish Playwright admin access, complete the safe Formidable
copy, verify actual editor recovery and labels, review responsive screenshots,
then request staging publication only when submission safety is demonstrated.
