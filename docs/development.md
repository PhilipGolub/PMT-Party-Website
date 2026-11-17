# Development workflow

## Current foundation

This is a documentation/configuration-only repository initialization. There is no
application server, plugin implementation, dependency manifest, lockfile, CI
pipeline, or application test suite yet. Do not invent installation or test
commands. No PHP, WordPress, or Oxygen runtime version has been verified.

Read [AGENTS.md](../AGENTS.md) first. Use the existing checkout; do not create a
worktree unless explicitly requested. Keep runtime WordPress files outside the
tracked source directories. Do not install plugins or modify staging to test
documentation changes.

## Safe Git workflow

1. Inspect `git status --short --branch`, local refs, and current user changes.
2. Verify the configured origin identity without printing embedded credentials.
3. Use `GIT_TERMINAL_PROMPT=0 git ls-remote --symref origin` to test Git read
   access. An unset token or CLI login prompt alone does not prove missing Git
   access; reuse platform authentication and never extract proxy credentials.
4. If a nonempty default branch exists, fetch and inspect its tree and history
   before proposing changes. Preserve local work; do not reset it to the remote.
5. Use a focused branch and reviewed changes. For this initially empty remote,
   `main` was verified as the server's unborn default branch; the local checkout
   is on `work`. Do not silently assume those branch names are interchangeable.
6. Before the initial remote update, recheck refs and preserve any work created
   since inspection. Avoid force-pushes. A dry run is a preflight, not a release.
7. When the first commit/default branch exists, use short-lived branches and pull
   requests. Configure protection/CODEOWNERS separately with approved maintainers.
   A merge does not authorize a WordPress deployment.

## Documentation checks now

- Review all additions and the diff for factual accuracy, spelling, and consistency.
- Verify relative Markdown links, UTF-8 encoding, final newlines, and whitespace.
- Verify `.gitignore` excludes representative credentials, backups, dependencies,
  and runtime files while allowing custom plugin source and safe example files.
- Review actual file contents for sensitive data; ignore rules cannot detect
  secrets in otherwise valid source files or remove already tracked secrets.
- Report document checks separately from application, integration, or UI tests.

## Before public-site work

Complete the [connection checklist](oxygen-connection.md), then inventory:

- WordPress, PHP, database, Oxygen, and connector versions; active/inactive plugins;
  required licenses and the supported compatibility matrix.
- Hosting access, backup/restore facilities, staging isolation, permitted deployment
  paths, HTTPS/access restrictions, and scheduled-job support.
- Oxygen's native reusable components, global styles, supported export/import
  behavior, and how custom plugin rendering can integrate through documented APIs.
- Existing inquiry form fields, validation, storage, notifications, spam protection,
  confirmations, and other integrations, using sanitized examples only.

Record observed versions and commands without license keys, personal data, or
credentials. Select/pin local tools only after this inventory. A future local
WordPress environment should use synthetic data and legally obtained plugins;
never commit WordPress runtime files, premium packages, or database snapshots.

## When custom source is approved

Choose the lowest supported PHP/WordPress versions from the verified matrix.
Introduce Composer and Node tooling only where needed, with lockfiles and frozen
installation commands. Test source against that matrix. Add CI before relying on
automated checks, and add a deployment workflow only after its separate approval.

For plugins, use PHP lint, WordPress coding standards, appropriate static analysis,
unit/integration tests, and focused end-to-end tests. For Oxygen work, review
native component reuse, responsive behavior, keyboard/focus, contrast, content,
forms, SEO, and performance. See [the redesign plan](redesign-plan.md).

Use sandbox credentials, synthetic users, and controlled outbound email. Store
secrets through approved secure settings; examples must contain placeholders only.
Report setup problems separately from confirmed application defects.
