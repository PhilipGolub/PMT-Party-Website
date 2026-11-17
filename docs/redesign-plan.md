# Public website redesign plan

## Objective and current evidence

Build a modern, premium event décor website in native Oxygen components while
preserving PMT's strongest existing branding, content, and useful functionality.
The client portal is a later phase, not the first implementation target.

No current-site content or visual audit has been completed: direct read-only
requests were blocked by this environment's proxy. Do not treat any proposed
page, service, testimonial, visual treatment, or customer claim as an observed
fact. Oxygen version and installed component capabilities also need verification.

## Phase 1 — Audit and preservation

Use read-only access to the live site. Do not submit live inquiry forms or trigger
emails, bookings, payments, or analytics experiments. Inventory:

- URLs, navigation, page purpose, service descriptions, calls to action, and forms.
- Logos, colors, typography, tone, distinctive visual treatments, and photography.
- Gallery structure, event categories, testimonials, trust signals, and contact data.
- Inquiry fields, conditional logic, accessibility, validation, confirmations, spam
  handling, routing, and notification/integration behavior through approved access.
- Titles, descriptions, canonical URLs, indexability, structured data, redirects,
  accessibility, mobile behavior, and performance using available read-only evidence.

For each page/feature, record `keep`, `refine`, `merge`, or `retire`, with rationale.
Use a content inventory with URL, purpose, owner, rights/approval status, current
behavior, proposed destination, and SEO/redirect considerations. No customer
submissions or private operational material belongs in the inventory committed to Git.
Preserve valuable URLs where practical; plan redirects before changing them.

## Phase 2 — Visual identity and reusable system

Confirm approved logo variants, color roles, typography licenses, photography
rights, tone, and target audiences. Develop semantic design tokens for color,
type, spacing, container width, radius, motion, and interaction states. Choose
values after review; no palette or font is approved by this document.

Plan native Oxygen components for header/navigation, footer, hero, service cards,
editorial content sections, gallery/project previews, proof/testimonial sections,
and inquiry calls to action. Include responsive behavior and accessible states.
Avoid custom code where a maintainable native element satisfies the requirement.

Keep an approved asset register with source, owner/license, public-use permission,
approved variant, and optimization notes. Commit only approved public brand assets
to `brand/approved/` when supplied. Do not commit private client/event photography,
unlicensed fonts, or personal metadata. Treat client publication consent explicitly.

## Phase 3 — Sitemap and content plan

Create a comprehensive sitemap from the actual audit and business priorities.
The following is a discussion scaffold, not a verified or approved final sitemap:

| Area | Pages to assess |
| --- | --- |
| Brand introduction | Home; About PMT |
| Offering | Services overview and relevant individual service pages |
| Inspiration | Portfolio/gallery overview and selected event/project stories |
| Audience needs | Event-type landing pages only where content and services justify them |
| Decision support | Process; FAQ; approved testimonials if available |
| Conversion | Event inquiry; contact information; confirmation experience |
| Governance | Privacy; accessibility information; applicable legal pages |

For each proposed page, define audience, intent, content owner, primary action,
native components, assets, SEO requirements, and links to related pages. Validate
page labels against actual offerings. Reserve portal/store navigation decisions
for their later phases rather than implying those services already exist.

## Phase 4 — Compare homepage directions

Prepare two or three clearly distinct directions after the audit. Possible
starting hypotheses, subject to available approved photography and brand review:

1. **Editorial elegance:** restrained typography, generous spacing, a strong event
   image, curated portfolio storytelling, and a considered inquiry invitation.
2. **Immersive celebration:** richer color and large photography, expressive event
   moments, a browsable portfolio, and prominent paths to relevant services.
3. **Modern concierge:** a clear service-led introduction, event-type discovery,
   process and trust evidence, and a direct, reassuring inquiry journey.

Each direction should show desktop and mobile compositions, typography/color
choices, navigation, hierarchy, portfolio treatment, and conversion flow. Include
accessibility and performance tradeoffs. These are design briefs, not completed
mockups or approved concepts. Select one before any Oxygen implementation.

## Phases 5–6 — Native Oxygen implementation and expansion

After explicit staging-write approval, implement the selected direction using
native Oxygen elements, shared tokens, and reusable components. Establish the
header, footer, homepage, and representative content patterns first. Review them
before expanding across the approved sitemap. Track database-managed layout
changes separately from Git-managed source changes; see [ownership](oxygen-and-git.md).

Acceptance should cover approved content/rights, responsive layouts, semantic
structure, keyboard navigation, focus, contrast, reduced motion, image alternatives,
image sizing, loading behavior, metadata, links, and native component reuse. Use
WCAG 2.2 AA as the design/testing target; do not claim conformance without evidence.
Agree performance budgets from measured baselines and test representative pages.

## Phase 7 — Existing inquiry form redesign

Audit the current form before deciding whether it can be reused, exported, or
rebuilt on staging. Verify Formidable availability and supported features first.
Preserve required business fields and routing while improving labels, grouping,
conditional questions, error handling, privacy notices, mobile use, and accessibility.

Test staging submissions with synthetic data and a controlled email recipient.
Verify validation, spam controls, storage, confirmations, notification routing,
and any existing integrations. Do not test by sending inquiries to live staff
workflows. Client accounts and portal access must not be created from unverified
submission emails. New inquiry automation requires separate implementation scope.

## Later phases

Only after the public foundation is accepted: implement client identity/membership,
event dashboard, version-specific design approvals, PandaDoc/PayPal integrations,
and optional commerce as separately approved slices. See [architecture](architecture.md).
Public-site publication and production changes always require separate approval.
