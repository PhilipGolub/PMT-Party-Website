# Technical architecture proposal

## Scope and current evidence

The first delivery is the public PMT Party Services Group website redesign.
Use native Oxygen elements, templates, reusable components, and shared design
tokens wherever they meet the approved design. The portal is a later phase.
This document proposes future boundaries; it does not describe deployed software.

The repository began empty. WordPress, PHP, Oxygen, Formidable, and hosting
versions and capabilities still need read-only verification. No custom plugin,
database schema, integration credentials, or running test stack is established.
See [the redesign plan](redesign-plan.md) and [connection verification](oxygen-connection.md).

## Public website first

1. Audit public content and navigation without changing production.
2. Confirm approved brand assets, audience, conversion goals, and sitemap.
3. Review homepage directions and select the design system before sitewide work.
4. Build approved native Oxygen components on staging; verify accessibility,
   responsive behavior, performance, and the inquiry journey.
5. Redesign the inquiry form after field requirements and routing are agreed.

Keep presentation in Oxygen and business rules in plugin services. Do not put
contracts, payment logic, permissions, or customer workflows in layout code blocks.
Custom rendering should call documented WordPress/Oxygen extension points only
after the installed versions and compatibility have been confirmed.

## Deferred application boundaries

Start with one namespaced, modular PMT application plugin when implementation is
authorized. Keep domain services independent of Oxygen and vendor APIs. Split
deployable plugins only when separate activation or release cycles justify it.

| Module | Responsibility | Boundary |
| --- | --- | --- |
| Core | Client/event relationships, capabilities, domain services | No vendor-specific API calls |
| Portal | Authenticated views, event membership, document access | Calls domain services; never trusts browser IDs |
| Inquiry adapter | Formidable hooks, validation, field mapping, routing | Translates vendor entries into PMT records |
| Design approvals | Immutable versions, review requests, decisions | Each decision identifies one exact version |
| Contract adapter | PandaDoc creation/status/reconciliation | External document identifiers and verified events |
| Payment adapter | PayPal order/payment references and reconciliation | Server-confirmed financial state |
| Commerce adapter | Optional WooCommerce interoperability | WooCommerce owns store orders if adopted |

Use documented interfaces and dependency checks so an unavailable optional plugin
does not break public pages. Do not add placeholder modules or dependencies now.

## Domain model and workflow

- **Identity:** WordPress users authenticate; explicit client/event membership and
  capabilities authorize access. Support multiple events and collaborators.
- **Inquiry:** a validated submission references its Formidable entry. Qualifying
  a lead into a client/event is an explicit staff action, not an email-based grant
  of portal access. Define retention and the authoritative record for each field.
- **Event/project:** a private business record connects clients, designs,
  contracts, and payment references. Authorization applies to every related object.
- **Design:** versions are immutable. Approval requests and decisions record the
  version, actor, time, and outcome. A revision requires a new approval request.
- **Contract and payment:** keep their states independent of design approval.
  An approved design does not prove a signed contract or captured payment.

Choose private custom post types versus custom tables through an architecture
decision before implementation. Consider query needs, volume, relational
constraints, immutable history, and migration cost; do not assume a schema now.

## Integration and background work

Treat provider-verified facts as authoritative for external contract and payment
status. Verify callbacks using each provider's current supported mechanism;
persist event identifiers, deduplicate delivery, and make side effects idempotent.
Plan bounded retries, failure visibility, and reconciliation for missed events.
Confirm a host-supported scheduler before relying on unattended jobs; WordPress
cron triggered only by site traffic may be insufficient.

PayPal confirmation must validate the expected amount, currency, recipient, and
internal order association server-side. Browser redirects cannot confirm payment.
Do not collect payment credentials in PMT forms. If WooCommerce is later approved,
avoid a parallel PMT payment path for the same store order. Confirm product, tax,
shipping, and fulfillment requirements before choosing the commerce scope.

## Security, privacy, and validation

Require object-level authorization on portal queries, REST routes, actions, and
files. Nonces protect against CSRF but do not grant access. Validate input, escape
output, prepare queries, rate-limit exposed forms, and minimize collected data.
Private designs/contracts require authenticated delivery or expiring storage URLs;
ordinary public media URLs are insufficient. Define retention, deletion, and
audit access before storing real client records. Keep logs free of secrets and PII.

Staging uses synthetic clients, sandbox providers, and controlled email. Never
commit customer data, private designs, secrets, or backups. Future tests must cover
client isolation, exact-version approvals, inquiry mapping, callback verification,
duplicates/retries, and payment reconciliation, plus public-site accessibility.

Implementation and releases require separate approval. See [source ownership](oxygen-and-git.md),
[development](development.md), and [deployment/rollback](deployment-and-rollback.md).
