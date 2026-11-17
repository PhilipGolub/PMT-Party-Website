# Deployment, layout promotion, and rollback

## Current policy

No deployment integration, auto-deploy hook, WordPress filesystem connection,
plugin activation, layout import, or database migration is configured here.
GitHub access and a merge do not establish or authorize any of these operations.
Production (`pmtparty.com` and `www.pmtparty.com`) is protected from changes without
explicit approval. Staging (`oxygen.pmtparty.com`) is the first implementation target.

## Prerequisites before the first deployment

- Verify staging identity, actual runtime/plugin compatibility, filesystem paths,
  hosting-supported deployment methods, and least-privilege access.
- Confirm staging is isolated from production databases, storage, email delivery,
  payment accounts, and document-sending workflows. Any setting changes need approval.
- Verify secure backup/restore facilities and define which data is protected and
  how recovery would affect data created after the backup. Keep backups outside Git.
- Agree the release scope, acceptance checks, migration requirements, maintenance
  implications, previous artifact, and rollback procedure before requesting approval.

## Custom code release workflow

1. Develop a focused change on a branch; review it against the compatibility matrix.
2. Run relevant CI once source/tooling exists: locked dependency installation, PHP
   lint, coding standards/static analysis, meaningful tests, and secret/dependency
   checks. Do not report a nonexistent pipeline as passing.
3. Build an immutable, versioned plugin ZIP from the reviewed commit. Include required
   production dependencies; exclude credentials, tests, local config, and runtime data.
   Record the checksum, version, source commit, and required runtime versions.
4. Obtain explicit approval for that artifact and staging actions. Initially prefer
   a manually reviewed installation. A later manual GitHub workflow should use a
   protected staging environment and approval gate if the account/plan supports it.
   Never introduce automatic deployment on merge by assumption.
5. Back up affected state securely and deploy only the approved plugin directory
   using a hosting-supported method with an intact/atomic replacement strategy.
   Do not copy the repository into the web root or overwrite all of `wp-content`.
6. Activate or migrate only as approved. Use backward-compatible, versioned, repeatable
   schema migrations; isolate destructive changes for separate review.
7. Verify the plugin version, errors, affected public pages, and relevant staging
   behavior. For future portal work include client isolation, private downloads,
   version-specific approvals, and verified sandbox callbacks as applicable.
8. Record the outcome and rollback readiness. Production promotion is a separate
   authorized release after staging acceptance, not an extension of this approval.

The hosting transport is intentionally undecided. Do not embed SSH/SFTP secrets,
API tokens, or application passwords in a workflow. Use approved secure bindings,
verified host identity/TLS, scoped access, and a host allowlist. Do not expose the
WordPress installation's writable paths or credentials unnecessarily.

## Oxygen layouts and configuration

Native Oxygen edits live in WordPress and follow their own approved change set.
Verify the installed version's supported export/import facilities and their scope
before relying on them. Record affected templates, components, global styles,
pages, dependencies, and expected regeneration/cache steps.

Use sanitized exports only when they can be safely reviewed without personal
data, secrets, or executable surprises. Keep secure backups outside Git. A code
artifact does not contain database-managed Oxygen layouts, Formidable settings,
or content; do not use a whole database overwrite as routine layout promotion.
Test any layout promotion procedure in a suitable approved isolated environment.

## Rollback and failure handling

- **Code:** stop the rollout and restore the known-compatible previous artifact;
  verify the restored version and affected behavior. For a first installation,
  plan safe deactivation/removal without deleting operational data.
- **Layouts/settings:** restore the specific prior change set through the verified
  supported mechanism. Regenerate derived assets/cache only as documented/approved.
- **Database:** older code must tolerate additive migrations. Do not automatically
  drop tables or restore an entire database; that can destroy intervening work.
  Obtain approval for a data recovery plan when required.
- **External effects:** reverting code does not unsend an email/document, reverse
  a payment, or remove an external record. Compensating actions need separate approval.

Release records should include target, approver, time, commit/artifact checksum,
configuration/layout change summary, secure backup reference, checks, errors,
and recovery outcome. Omit secrets, customer details, and raw private logs.
