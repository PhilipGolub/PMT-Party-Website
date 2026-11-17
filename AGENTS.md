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
