# Architecture and security

Documentation review · October 26, 2026 · application behavior unchanged

The app uses static HTML, CSS and ES modules. Browser-local search avoids a shared search backend and visitor accounts.

Data flow: owner-edited `data/frameworks.tsv` → `scripts/build-catalog.mjs` → validated `dist/catalog.json` → bounded same-origin loader → search engine → DOM result cards → official publisher links.

| Component | Responsibility |
| --- | --- |
| `data/frameworks.tsv` | Editable curated metadata, ten pipe-separated fields |
| `scripts/build-catalog.mjs` | Source size/schema validation, SHA-256, temporary-file verification and replacement |
| `dist/search-core.mjs` | Schema and URL validation, classifications, matching, suggestions and pagination |
| `dist/catalog-loader.mjs` | Bounded read-only catalog acquisition |
| `dist/app.mjs` | Search controls, results, refresh and sharing |
| `dist/appearance.mjs` / `appearance.css` | Theme and accent selection with separate browser preference key |
| `scripts/serve.mjs` | Fixed-file loopback preview with Host/Origin/method checks |

Owner-edited source, hosted JSON, browser storage and the hosting account are separate trust boundaries. Catalog text uses DOM text nodes; official HTTPS destination allowlists reject unsafe schemes, credentials, spoofed hosts and unexpected ports. Source metadata is validated before rendering. No public write endpoint or client credential is present.

Catalog loading has a 2 MB limit, 15-second timeout and no credentials or redirects. The preview serves only approved files, rejects traversal and write requests, and supplies CSP and other response headers. Production header enforcement depends on the host. These controls do not establish formal certification or exhaustive security.

Only validated appearance preferences are saved locally. No query history, account database, AI prompts or telemetry service is implemented. Hosting providers and publisher sites still receive normal HTTP connection metadata.

Residual risks include stale or inaccurate metadata, compromised owner/publisher/host accounts, outages and browser extensions. Source hashes identify local input bytes; they are not publisher signatures. Full publisher edition/link review, screen-reader testing, all-browser testing and penetration testing were not repeated for this documentation release.

See [SECURITY.md](../SECURITY.md), [TESTING.md](TESTING.md) and [OPERATIONS.md](OPERATIONS.md).
