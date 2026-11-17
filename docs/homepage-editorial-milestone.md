# Premium editorial homepage — staging milestone

## Authorized scope and acceptance

On November 17, 2026, the owner authorized a new unpublished page titled
**PMT Homepage — Premium Editorial Luxury Draft** on https://oxygen.pmtparty.com.
Build editable native Oxygen elements with responsive desktop, tablet, and phone
styles, reusable components, real existing public photography, and an inquiry CTA.
Preserve all existing drafts, the front-page setting, and header/footer conditions.
No production writes, plugin/settings changes, notifications, or payment actions.

## Before-change evidence

- Official Oxygen `site-info` confirmed staging, WordPress 7.1.4, Oxygen 6.2.2,
  PHP 8.5.12, and CSS prefix `ppsg-`.
- Front-page ID: 0; active header IDs: 4618; active footer IDs: none.
- Existing page drafts: 4616, 4619, 4622, 4624, 4626. Leave untouched.
- Header 4618 currently has no Oxygen content, according to `preview-post`.
- Modern Normalize is disabled. Preserve this sitewide setting; explicitly set
  margins on the new design's own classes instead of adding a global tag reset.
- Read AGENTS.md, README, development, architecture, redesign, ownership, and
  connection documentation; earlier connection notes are historical.
- Read official Oxygen instructions and building-sites, design-first-build,
  building-templates, patterns, and navbar guidance.

## Public-site audit

Read-only GET of https://www.pmtparty.com succeeded through the approved network
route. The web browsing tool could not fetch it. Review covered rendered source,
copy, navigation, image references, and selected photographs; no form submitted.

Keep: PMT logo, Staten Island/NYC positioning, event planning and décor, balloon
and floral work, custom apparel/signage/invitations, actual event photographs,
consultation and estimate process, public event-form route, social/legal links.
Refine: very long overlapping menus, many `#` destinations, competing service
labels, small repeated images, dense process copy, and image alternatives.
Defer: portal, account, commerce, contracts, deposits, payment-provider workflows.
Do not repeat the unverified review-count claim or invent testimonial quotations.

Photography selected only from existing public PMT homepage/gallery references;
no new publication-rights claim is made. Obtain asset-specific rights confirmation
before eventual publication. Keep photos in WordPress, outside tracked source.

## Intended design

Photography-led editorial luxury: warm ivory, dark ink, deep red derived from the
existing red brand direction, muted brass rules, Cormorant Garamond display type,
and DM Sans text. Shared classes and uniquely named variables affect only the new
draft/components. Navigation and footer are component concepts with no display
conditions. Inquiry links lead to the existing public inquiry page; no new form
or outbound automation is introduced.

Build input is kept in ignored `.oxygen-prototype/` for iteration. These are
prototype inputs, not an Oxygen export or a database backup.

## Result and verification

- Created page **4640**, title as requested, status **draft**, built with Oxygen.
  Preview: https://oxygen.pmtparty.com/?page_id=4640&preview=true (sign-in required).
  Builder: https://oxygen.pmtparty.com/?oxygen=builder&id=4640.
- Created reusable Components **4642** (navigation), **4645** (event inquiry),
  **4648** (footer), and inserted them only into page 4640. No template created.
  The inquiry component exposes headline, introduction, button label, and URL
  for per-instance editing. Preview canvas is 1440px with an ivory background.
- Native Containers, Text with semantic heading/paragraph tags, Images, Text
  Links, and Component instances form the layout. No HTML/PHP code block,
  third-party layout import, custom script, live form, or business logic added.
- Eight sections: hero, introduction, services, portfolio, custom creations,
  process, clearly marked testimonial placeholder, and event inquiry. Navigation
  wraps on phones so every section remains reachable without a scripted menu.
- Created 74 unique draft-scoped class selectors and 11 uniquely named variables
  in the `PMT Editorial Draft` collections. All import calls returned no warnings.
  No existing selectors or variables replaced. Fonts load through Oxygen's
  supported font mechanism (confirmed by `get-post-css-files`).
- Typography: Cormorant Garamond headings; DM Sans body/navigation. Hero type
  54–88px, section headings 40–64px, body 16px, supporting text 14px.
- Palette: paper #f7f3ed, warm white #fffdf9, ink #24211f, muted text #625a53,
  deep red #7c2635, brass #88734e, rules #d8cfc4. Spacing uses 24/32/40/48/64px
  intervals, fluid section padding 64–128px, and gutters 24–88px.
- Reused the public logo (attachment 4345), Atlantis Yacht floral/table décor
  (4244), black/gold candlelit celebration (4395), and the existing public
  `Gabrielle.jpg` wedding portrait. The latter's live alt text incorrectly
  describes a centerpiece; the new draft describes the actual staircase portrait.
  Images remain on staging. The hero/logo load eagerly; gallery images load lazily.
- Source process was condensed into vision, details/estimate, personalization,
  and setup. Pricing, deposit rules, provider names, and review-count claims were
  deliberately not introduced into this design draft.

### Passed checks

- `get-post-tree` confirmed editable native elements and three Component instances.
- `preview-post` with CSS and header/footer resolution confirmed all eight sections,
  one H1, correct content, all three components, no duplicate IDs, and no missing
  internal anchor targets. The existing active header resolves empty; no footer
  template applies. The draft's own navigation/footer render through components.
- Generated stylesheet and stored selector properties confirmed responsive grid
  changes at official 1119/1023/767/479px breakpoints, including stacked mobile
  hero/services/portfolio and one-column narrow-phone process/footer layouts.
- Selected staging photography URLs returned HTTP 200. Media-library hero and
  gallery images include native responsive source sets and descriptive alt text.
- Visible keyboard focus is specified for links/buttons and a skip link exists.
  Calculated contrast: ink/paper 14.48:1, muted/paper 6.12:1, white/red 9.46:1,
  light text/ink 9.83:1, light eyebrow/red 5.70:1. No WCAG conformance claim is
  made. No motion-dependent content or entrance effects.
- Final `site-info`: home page ID remains 0, header IDs remain [4618], footer IDs
  remain empty, Modern Normalize remains disabled. All five prior drafts remain.
- No production or other-site write tool, form submission, notification action,
  payment action, plugin activation, or site-setting mutation was called.

### Remaining review and next iteration

- Pixel-level desktop/tablet/phone screenshots and interactive keyboard/device QA
  were not run. Official Oxygen preview verifies markup and stored responsive CSS,
  not browser-rendered appearance. Review crops and typography in the draft builder.
- Replace the typography-only custom-creations concept with approved photographs
  of invitations, signage, banners, apparel, and finished printed pieces.
- Add distinct birthday, baby-shower, and corporate-event photography; replace the
  repeated yacht image with another approved detail. Consider a wider hero crop.
- Supply a verified testimonial with source and approved attribution. Confirm
  asset-specific publication permissions before publication or production rollout.
- Review image `sizes` hints and file weights before launch. Oxygen currently
  emits broad default responsive sizes, including for the compact logo.
- Hover/focus feedback is deliberately static; optional entrance animation should
  wait for reduced-motion behavior to be verified in the frontend runtime.
- Inquiry CTA opens the existing public event form; a redesigned staging form,
  controlled notification tests, and inquiry routing remain a later milestone.
- Rollback for this isolated draft is to remove its component instances and
  trash the new draft/components through native tools after owner authorization.
  No production deployment or database migration occurred.
