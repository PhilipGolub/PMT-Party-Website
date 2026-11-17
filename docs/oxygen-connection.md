# Oxygen and WordPress connection verification

## Verified access state — November 17, 2026

| Check | Result |
| --- | --- |
| Git origin read | Passed; empty remote and unborn default `main` verified |
| Git push preflight | Passed in dry-run mode only; no remote branch created |
| GitHub REST metadata | `Forbidden`; not needed for the verified Git default-branch result |
| Live site GET | Proxy tunnel rejected with HTTP 403 |
| Staging root GET | Proxy tunnel rejected with HTTP 403 |
| Staging `/wp-json/` GET | Proxy tunnel rejected with HTTP 403 |
| PMT WordPress app tools | No callable tools exposed in this session |
| WordPress/PHP/Oxygen/plugin versions | Unverified |
| Oxygen Agent Connector transport/auth/tools | Unverified |

The website requests failed before a site response could be inspected. They do
not establish a site outage, a missing plugin, or bad WordPress credentials. The
app tag is not proof of an authenticated MCP connection. No guessed MCP endpoint
was called and no WordPress settings were changed.

## Required configuration and information

1. **Make the actual app connection available.** In the client's app/connector
   configuration, verify that PMT Party Services Group (WordPress) is enabled,
   authenticated for staging, and exposes tools to this conversation. The precise
   reconnect flow depends on that app; no app-specific instructions were exposed.
2. **Identify the server.** Confirm the exact Oxygen Agent Connector plugin name,
   vendor, version, installation/activation state, and official documentation.
   Obtain its actual endpoint, supported transport, client compatibility, and
   authentication scheme. Do not infer these from the WordPress REST URL.
3. **Use approved staging authentication.** Reuse an existing usable binding first.
   If missing, configure a dedicated staging identity with the least permissions
   supported by the connector. Enter credentials only in secure app/environment
   settings. Use application passwords only if explicitly supported. Do not grant
   production access, expose personal credentials, or request secrets in chat.
4. **Permit the required network routes.** The current cloud policy has package
   manager presets and no custom domains. For direct public-site auditing add
   `www.pmtparty.com` and `pmtparty.com`; for direct staging inspection add
   `oxygen.pmtparty.com`, preserving existing rules and presets. GitHub REST checks
   additionally need `api.github.com` if that workflow is desired. The saved draft
   below covers website hosts only and has not been applied to this runtime. Hosted app connections
   may use a separate route and need their own reachability checks. Add any
   connector-vendor destination only after its documentation identifies it.
5. **Respect site protections.** Confirm valid HTTPS and any staging access-control
   or firewall requirements. Arrange narrowly scoped access rather than disabling
   security globally. Retry read-only checks after meaningful configuration changes.

If the connector is not installed, activation or installation is a separate
WordPress change requiring approval. Public HTML alone cannot reliably establish
exact WordPress/Oxygen versions, plugin availability, or connector permissions.

### Saved network draft

A subsequent configuration draft adds `pmtparty.com`, `www.pmtparty.com`, and
`oxygen.pmtparty.com`, preserving package-manager presets. The table and direct
request failures above describe the running instance, where these destinations
remain blocked. The draft save does not apply runtime changes or publish the
environment. Review and save in environment settings, then publish as required.
Retry the public/staging read-only requests afterward. App tool exposure and
authentication must still be resolved separately; network access alone is not
a verified Oxygen/MCP connection.

## Read-only acceptance sequence

Once documented connector tools are available:

- List their capabilities and distinguish inventory/read tools from write tools.
- Read the site identity and canonical URL; require `oxygen.pmtparty.com`. Stop
  if the target is production or cannot be established.
- Read exact WordPress, PHP, Oxygen, and connector versions and relevant
  compatibility/license status without collecting license keys.
- Read active/inactive plugin inventory, especially Formidable, WooCommerce,
  integration plugins, security/caching tools, and backup facilities.
- Inspect available Oxygen templates/components and native reuse/export mechanisms.
  Avoid customer entries, documents, payment records, and other private content.
- Record tool names, date, verified versions, limitations, and evidence summaries
  without credentials, sensitive content, or raw diagnostic dumps.

Success means authenticated read-only inventory from the confirmed staging site.
It does not authorize write tools or prove that a GitHub deployment connection
exists. Plugin, settings, layout, and database changes require their own approval.
