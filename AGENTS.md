# PMT Party Services Group — Development Instructions

## Mission and sequence

Build a modern, premium event décor website for PMT Party Services Group Corp.
Prioritize the public website: current-site audit, brand and design system,
sitemap, two or three homepage directions, selected native Oxygen components,
sitewide rollout, and inquiry form redesign. Plan the client portal now but defer
its implementation until the public website foundation is approved.

## Environments and authorization

- Production: `https://www.pmtparty.com` (including `pmtparty.com`). Never change
  production without explicit authorization for the particular action.
- Staging: `https://oxygen.pmtparty.com`. Confirm the target before site actions.
- Obtain explicit approval before deployments, plugin installation/activation,
  WordPress settings changes, layout/database writes or imports, and external
  actions such as sending contracts, emails to clients, or initiating payments.
- GitHub access does not imply WordPress access, a working MCP connection, or
  deployment authority. A merge must not implicitly deploy or activate code.
- Read-only inventory is permitted. Prefer documented connector tools; do not
  guess connector endpoints, authentication schemes, capabilities, or versions.
- Use the existing checkout. Do not create worktrees unless requested. Inspect
  existing files, refs, and changes before editing; preserve user work. Do not
  reset, force-push, overwrite unknown files, or publish unreviewed changes.

## Architecture and ownership

- Prefer native Oxygen elements, templates, and reusable components for layouts.
- Keep custom business rules in maintainable, namespaced WordPress plugins.
  Do not put business logic in Oxygen code blocks or unmanaged snippet plugins.
- Git owns custom source, tests, documentation, and approved brand assets.
  WordPress owns Oxygen layouts, content, settings, and operational data.
- Layout promotion is separate from code deployment. Confirm the installed
  Oxygen version's supported export/import workflow before relying on exports.
- Do not modify WordPress core, Oxygen, or other third-party plugin files.
- Keep integrations behind adapters with graceful handling of missing dependencies.
  Defer portal, approvals, PandaDoc, PayPal, and WooCommerce implementation.
- Verify actual PHP, WordPress, Oxygen, and plugin versions before selecting APIs
  or committing runtime requirements. Do not invent a working development stack.

## Confidentiality and assets

- Never commit credentials, API secrets, application passwords, license keys,
  private keys, customer information, private designs/contracts, or database backups.
- Keep runtime uploads, caches, logs, commercial plugin packages, and WordPress
  installations outside tracked source. An ignore rule is not a security boundary.
- Use synthetic fixtures and approved secure configuration. Never request secret
  values in chat or print credential files or process environments.
- Copy production data only under an explicitly approved sanitization process.
- Commit brand assets only after confirming ownership/license and approval.
  Client/event photography also needs appropriate publication rights. Strip
  sensitive metadata. Store private operational files outside Git.

## Implementation standards for later phases

### Oxygen Structure panel naming

- Give every authored element and reusable component instance a native custom
  Structure label in the format `Section — Element Purpose`, for example
  `Hero — Main Headline`, `Services — Wedding Card`, and `Inquiry — Form Embed`.
- Name repeated items distinctly by service, project, step, or function. Name
  containers as clearly as their contents; avoid CSS class names as labels.
- Oxygen 6.2.2 MCP exposes the editor-only field `meta.friendlyName`. Recheck
  the installed element schema before using it. Use `edit-post` to change only
  that field for a naming pass; never invent unsupported properties.
- Preserve CSS classes and selector IDs, HTML IDs, content, hierarchy, component
  references, and behavior during naming. Apply the same convention to new
  pages, shared components, and Formidable page wrappers.
- Coordinate with open editor sessions before MCP writes. Ask the editor owner
  to save and close tabs, reread the current tree, and avoid overwriting newer
  work. Reopen the editor after changes rather than saving a stale session.
- Verify persisted labels by rereading the saved tree; compare before/after
  structure and preview markup for naming-only changes. Also verify labels in
  the reopened visual editor when browser access permits. Clearly distinguish
  server persistence from visual-editor verification.
- Keep real Formidable fields and processing in Formidable. Name Oxygen form
  containers and embeds clearly without creating a second form system.

### Formidable staging development

- Discover native Formidable abilities through the verified PMT staging MCP
  connection before using other management routes. Use the official Formidable
  skill and current ability schemas; do not invent a duplicate/import ability.
- Preserve source form 3, its actions, and historical entries. Work on form 13
  (`pmt-event-inquiry-staging`) in existing Oxygen inquiry draft 4662; do not
  create another inquiry page or duplicate the completed homepage work.
- Form 13 is administrator-only and has a confirmation action without email,
  spreadsheet, webhook, or payment actions. Recheck actions before every test.
  Use synthetic information only. Read test entries by known ID or exact
  synthetic search within form 13; never list unrelated customer submissions.
- Keep field processing, validation, conditional logic, uploads, progress, and
  review inside Formidable. Use the labeled native Oxygen Shortcode element
  for embedding, and Formidable's scoped style for form appearance.
- Send explicit form status on updates and verify access restrictions afterward.
  Formidable's renderable internal `published` status does not authorize
  publication of WordPress pages 4640 or 4662.
- Verify browser submission and entry storage as well as API validation. Test
  protected file access without authentication using synthetic uploads only.
  Do not treat accepted settings as proof of working privacy or notifications.
- See `docs/formidable-inquiry-2026-11-18.md` for IDs, schema limitations, test
  results, and publication gates. Git documentation is not a configuration backup.
- Preserve the approved form style 4685 during logic improvements. Use native
  conditional fields and page breaks; do not add custom JavaScript to route
  inquiries or reconstruct the native Summary field.
- Form 13's venue page break 199 depends on installation field 192. Both Yes
  and Not sure keep the installation questions; No skips the page. Preserve
  fields 202–216 and the added access-confirmation field 231.
- The initial Venue & Setup assessment requires setting 202, setup-risk status
  237, approval status 214 and preliminary acknowledgment 216. Risk checklist
  239 is required only for unusual conditions. Setting, risk status and approval
  allow unsure answers; unknowns need later follow-up, not assumed approval.
- Optional choice 238 reveals retained technical fields. Access confirmation
  231 and mounting details 213 are optional at inquiry time. Measurement
  certainty 211 is required only when a positive dimension is provided. Keep
  numeric limits and field IDs; test clearing all related answers when details
  or risks are hidden. Confirm venue facts and approvals during planning before
  finalizing installation; inquiry answers do not replace contractual duties.
- Product specifications are conditional by selected service. Shared product
  preferences apply across remaining products; product-specific wording belongs
  in that product's specifications. Test both changing categories and removing
  every product, plus clearing a deadline and hiding a previously answered venue
  page. Verify the final saved synthetic entry, not only hidden browser controls.
- The owner added native submit field 221. Keep it last; do not assume this form
  still uses only the form-level fallback submit button.
- Services refinement uses optional native fields 240–245 for rental examples,
  balloon styles, table/chair focus, banner formats, display equipment and the
  event website/RSVP brief. These collect estimate information, not orders or
  availability guarantees. Do not introduce mandatory Rent/Buy decisions.
- Floral fields 171/172/177 are shared by the Florals service and the artificial
  floral rental choice in 240. Printed-backdrop choice 170 uses the same banner
  and shared production questions as Custom Banners. Preserve these OR rules;
  neither path requires selecting a second top-level service.
- Signage field 168 is now a checkbox with its original stored values retained.
  Table count 174 is conditional on table styling, florals or relevant rentals;
  chair count 176 requires chair décor in 242. Runners 175 require table styling.
  Quantities remain optional. Shared specification text is not rewritten when
  a format changes within a still-selected category; customers review it with
  native Summary/Edit. Hidden categories must clear their saved answers.
- Inquiry-page estimate guidance describes manual scope review, estimate
  revisions and the later PandaDoc agreement. It does not authorize contract,
  payment or inventory integrations, nor promise a booking or final price.
- Fulfillment field 230 follows setup intent 192. Native non-repeating section
  246 (closed by 247) shows only for the existing No setup value; 230 retains
  the product-service/printed-backdrop OR conditions inside it. Yes, Not sure,
  blank setup or no relevant products must not demand a fulfillment choice.
  Keep Delivery/Pickup/Please advise labels separate from their legacy values,
  with no default selection. The section has no visible heading or heading
  spacer; its native Custom HTML omits only the heading line. Test clearing
  fulfillment on setup/service changes and the native Summary/Edit controls.

### Application implementation

- Use PHP namespaces under `PMT` and `pmt_` prefixes for public identifiers.
- Follow WordPress coding standards, documented APIs, and the verified runtime
  compatibility matrix. Pin dependencies and preserve lockfiles when introduced.
- Validate input, escape output, and prepare database queries. Require capabilities
  and object-level authorization on protected routes, actions, queries, and files.
  Nonces do not replace authentication or authorization.
- Protect private documents through authenticated delivery or expiring storage URLs.
- Verify provider callbacks, deduplicate events, make financial actions idempotent,
  and reconcile external state. Redact personal information and secrets from logs.
- Prefer accessible semantic markup and reusable design tokens. Verify responsive
  behavior, keyboard access, focus, contrast, and reduced-motion behavior.

## Validation and release discipline

- During documentation initialization, validate links, formatting, ignore rules,
  and the diff. Do not create application modules or fake tests for appearances.
- When implementation exists, run meaningful relevant lint, static analysis, and
  tests. Prioritize client isolation, version-specific approvals, inquiry mapping,
  integration verification, and public-site accessibility and smoke checks.
- Report passed, failed, skipped, and unrun checks accurately. Distinguish verified
  facts from proposals and inaccessible systems.
- Use sandbox integrations, synthetic clients, and controlled email on staging.
- Release reviewed, versioned artifacts. Record the target, commit, readiness
  checks, migrations, backup reference, and rollback procedure before deployment.
- Prefer backward-compatible migrations. Code rollback is not database rollback.
- Production promotion requires separate approval after staging acceptance.

## Project references

Start with `README.md`, `docs/development.md`, `docs/redesign-plan.md`, and
`docs/architecture.md`. Use `docs/oxygen-connection.md` for connection verification,
`docs/oxygen-and-git.md` for ownership, and `docs/deployment-and-rollback.md` for
release planning. User instructions for the current task take precedence.
