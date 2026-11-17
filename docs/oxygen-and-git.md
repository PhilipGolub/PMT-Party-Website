# Oxygen, WordPress, and Git ownership

## Two coordinated systems

GitHub is the source history for custom code and approved project materials.
WordPress stores site content, layouts, configuration, and operational data.
A Git commit or merge does not update WordPress. An Oxygen edit does not create
a Git commit. No automatic deployment connection is established or assumed.

`https://www.pmtparty.com` is production and must remain unchanged without
explicit authorization. `https://oxygen.pmtparty.com` is the staging target;
verify its identity before any approved write. Access alone is not write approval.

The installed Oxygen version and supported export/import capabilities still need
verification. Do not assume an older Oxygen workflow or internal database format
applies to Oxygen 6.2. Prefer documented native elements and reusable components.

## Ownership map

| Material | Primary home | Repository policy |
| --- | --- | --- |
| Native Oxygen layouts, templates, reusable components, design settings | WordPress database | Document changes; eligible sanitized exports only after verification |
| Page/post content and navigation | WordPress database | Content plans allowed; no database dumps |
| Custom PMT plugin PHP, JavaScript, CSS, and build inputs | Git | Review and release versioned source/artifacts |
| Plugin-owned business schema and migration code | Git | Review migrations; records remain outside Git |
| WordPress/plugin configuration and licensed packages | Runtime/approved secure storage | Document requirements; exclude secrets and commercial packages |
| Public approved brand assets | Approved asset directory in Git | Confirm rights, approval, and safe metadata first |
| Media uploads, customer files, contracts, inquiry data | Protected runtime storage | Never commit private operational files |
| Database/file backups and logs | Restricted backup/operations storage | Never commit backups, customer data, or sensitive logs |
| Architecture, tests, synthetic fixtures, release procedures | Git | Keep useful, current, and free of private data |

Custom source must not modify WordPress core, Oxygen, or other vendor files.
Do not use Oxygen code blocks or unmanaged snippet plugins as the home for
business rules. No custom theme or additional framework is proposed; verify the
actual runtime needs before selecting one. See [the architecture proposal](architecture.md).

## Layout change record and exports

Before approved layout work, record the staging target, relevant page/template
identifiers, intended behavior, and acceptance criteria without customer data.
Afterward, record the result and review evidence. Keep private operational
references in approved storage rather than copying their contents into Git.

Use layout exports in Git only if the installed Oxygen version supports a
documented export/import process and the export has been inspected and sanitized.
Check for embedded personal information, credentials, scripts, private URLs,
environment-specific IDs, media references, and licensing restrictions. An export
is not automatically safe because its format is JSON or another text format.

Do not hand-edit undocumented serialized database values or treat an export as
a complete backup. Test an approved import on staging with rollback preparation.
Confirm dependencies and ID/URL mapping; a copied layout may reference content,
media, or plugin features that are absent in the destination environment.

## Separate release paths

**Custom code:** a reviewed commit produces a versioned plugin artifact. Approved
deployment copies only the intended custom code. It must not overwrite uploads,
vendor plugins, runtime configuration, or the WordPress database.

**Layouts/content:** approved Oxygen/WordPress changes use the verified native
workflow. Promotion requires its own scope, review, backup, and acceptance checks.
Never restore an entire staging database onto production as a layout shortcut;
that can replace users, inquiries, settings, orders, or other operational records.

For coordinated changes, document which plugin version a layout requires and
sequence releases so missing optional functionality fails gracefully. Record code
version and layout review together without implying Git contains database state.

## Recovery and access

Retain prior code artifacts and approved private backup references before a
release. Code rollback and layout/database recovery are different operations.
Database migrations can make old code incompatible; prefer additive changes and
validate compatibility before deployment. No restore or rollback is authorized
merely by documenting it. See [deployment and rollback](deployment-and-rollback.md).

Use least-privilege access and approved secure configuration for hosting, GitHub,
WordPress, and the Oxygen connector. Never commit tokens, application passwords,
API keys, license keys, or credential-bearing URLs. Ignore rules reduce accidents
but do not authorize sensitive files or erase committed history.

Read [connector verification](oxygen-connection.md) before site tooling and
[development instructions](development.md) before future implementation.
