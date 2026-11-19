# PMT Party Services Group Corp.

Foundation for the public website redesign and future custom WordPress development.

| System | Role |
| --- | --- |
| `https://www.pmtparty.com` / `https://pmtparty.com` | Live website; no changes without explicit approval |
| `https://oxygen.pmtparty.com` | Staging website and intended Oxygen design environment |
| `PhilipGolub/PMT-Party-Website` | Custom source, documentation, tests when introduced, and approved brand assets |

GitHub and WordPress are separate systems. This repository does not deploy itself
and does not contain the WordPress database or a working local WordPress install.

## Current staging state — November 19, 2026

Authenticated Oxygen development now uses `https://oxygen.pmtparty.com`.
Homepage draft **4640** has native components and descriptive Structure labels.
Event inquiry draft **4662** now embeds genuine Formidable form **13**, an
administrator-only working copy of the original event form **3**. Its five-step
flow, conditional questions, validation, uploads, confirmations, and synthetic
entry storage have been tested through native abilities and authenticated Chrome.
Conditional refinement now skips installation for requests without on-site setup,
adds product-specific specifications and deadlines, and clears irrelevant answers
when selections change. Four additional browser test inquiries verified the
products-only, installation, mixed, and change-of-mind paths.
The final inquiry UX pass adds smaller product-budget ranges, Bridal Shower,
clearer New York terminology, a conditional stage overview, and restrained
readability improvements. Three more synthetic browser submissions verified
products, installation and mixed mobile inquiries, stage-local validation,
Back/Edit navigation, and blank optional times.
Venue & Setup now starts with a short preliminary assessment. Existing technical
fields sit behind an optional details choice, while setup risks and venue approval
remain explicit. Six further synthetic inquiries verified full, simple, elevated,
unknown, products-only and mixed requests, including clearing hidden details.
Services & custom pieces now includes optional balloon and banner formats,
recognizable signage and rental choices, relevant table/chair questions, and a
short event website/RSVP brief. Floral rental guidance and the itemized-estimate
workflow are clearer. Ten more browser submissions verified the service paths,
native Summary/Edit navigation and clearing removed-service answers. The current
form has 87 field records; its approved visual style remains unchanged.
The original form and its actions remain unchanged; the copy has no outbound
notification, spreadsheet, webhook, or payment actions.

See the [initial homepage milestone](docs/homepage-editorial-milestone.md) and
[refinement and investigation record](docs/staging-refinement-2026-11-17.md), and
[Formidable integration and verification](docs/formidable-inquiry-2026-11-18.md)
for verified versions, preview links, changes, and outstanding tests.
The Oxygen Doctor warning remains under investigation. Nothing has been
published as a WordPress page, activated sitewide, or deployed to production.
Formidable's internal form status is published so it can render, with access
restricted to administrators. Sitewide staging protection, search-indexing
restrictions, release checks, and explicit approval are still required before
publishing either page.

## Initial discovery snapshot — historical

- Git read access was verified against the repository's configured HTTPS origin.
- At initial inspection the server advertised an unborn default `HEAD` targeting
  `refs/heads/main`: the remote had no commits, branches, or tags.
- A non-mutating push preflight to `codex/initialize-foundation` succeeded using
  a disposable empty commit in a temporary bare repository. A subsequent ref
  query confirmed no remote refs were created by that preflight. This alone does
  not prove that all future branch rules or writes will be accepted; consult Git
  history and remote refs for the subsequent documentation initialization.
- GitHub REST metadata inspection returned `Forbidden`. Git access does not
  establish API access; the default branch was verified through Git instead.
- The local checkout was empty on entry, on unborn branch `work`. This
  initialization adds documentation and configuration only, with no application,
  dependency installation, automated deployment, or runnable tests.
- Direct read-only requests to the live site, staging root, and staging REST
  index failed with `Tunnel connection failed: 403 Forbidden` at the network
  proxy. This does not establish a website outage or WordPress authentication error.
- The tagged PMT WordPress app exposed no callable tools in this session.
  WordPress, Oxygen, Formidable, other plugins, and MCP capabilities are unverified.
  Oxygen 6 is the target; the earlier requested 6.2 version is not an observed fact.
- A network configuration draft now adds `pmtparty.com`, `www.pmtparty.com`, and
  `oxygen.pmtparty.com`, preserving package-manager presets. Saving the draft does
  not apply it to this runtime or establish an MCP connection. Review/save and
  publish through environment settings as required by the environment UI.

## Priority and scope

1. Audit the current public website and preserve its strongest brand, content,
   navigation, SEO value, and useful functionality.
2. Establish a refined visual identity and reusable design system.
3. Approve a comprehensive sitemap and content plan.
4. Compare two or three distinct homepage directions and select one.
5. Implement the selected direction in native Oxygen components on staging,
   after approval for those changes.
6. Extend the approved system through the public website.
7. Redesign the existing event inquiry form using Formidable where appropriate,
   preserving required submission and notification behavior.
8. Implement the client portal later. Plan its architecture now; defer design
   approvals, PandaDoc/PayPal automation, and optional WooCommerce functionality.

## Documentation

- [Permanent development instructions](AGENTS.md)
- [Development workflow and setup prerequisites](docs/development.md)
- [Public website redesign plan](docs/redesign-plan.md)
- [Architecture and deferred business functionality](docs/architecture.md)
- [Oxygen/database and Git/source ownership](docs/oxygen-and-git.md)
- [Oxygen and MCP connection verification](docs/oxygen-connection.md)
- [Deployment, layout promotion, and rollback](docs/deployment-and-rollback.md)

## Source structure as implementation begins

Introduce `plugins/pmt-platform/` for modular business functionality only when
its implementation is approved. Use `tests/` for meaningful tests and synthetic
fixtures; `brand/approved/` for approved, licensed assets; and `oxygen/exports/`
only for reviewed, sanitized exports supported by the installed Oxygen version.
An optional WooCommerce adapter may later live in `plugins/pmt-commerce/`.
No empty application modules or commercial plugin packages are needed now.

## Review and next action

Review source changes before committing or publishing them. The foundation is
documentation and configuration only; Git history records its commit. Recheck
remote refs before pushing, because the remote can change while work is in
progress. Do not reset or force-push if existing work appears.
See the connection guide for the prerequisites to a read-only staging inventory,
then begin the public-site audit and design exploration. No site deployment,
WordPress setting change, or automatic GitHub-to-WordPress connection is configured.
