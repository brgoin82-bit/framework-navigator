# Framework Navigator 0.1.0

A free independent reference library for cybersecurity, governance, risk, privacy, cloud, AI, application security, supply chains, operations and data-center resources. It deliberately follows the NIST Navigator layout, including the repaired dark high-contrast and custom-accent controls.

## Coverage—not a claim of every framework ever

The initial catalog contains **117 resource families, 44 publishers and 16 subject areas**, assembled October 13, 2026. It includes NIST, ISO/IEC, CIS, CISA, OWASP, MITRE, CSA, ISACA, AICPA, PCI SSC, SCF, Open FAIR, government/regional resources, and data-center standards. The source is the editable `data/frameworks.tsv`, not a universal authoritative registry. Every source row is represented in the generated catalog; that count does not prove worldwide completeness.

This is not every proprietary/sector-specific framework, historical edition, language variant, individual control or publication. Standards families may combine parts or related documents; the card explicitly notes such cases. Some links open an official family directory rather than an individual document. The identifier and edition note explain what to locate there. Full standard text is not copied or redistributed.

Resource type distinguishes **Framework**, **Standard**, **Control catalog**, **Guidance**, **Maturity model**, **Assurance program**, **Knowledge base** and **Risk model**. SOC 2 is an attestation program, not a government certification. ATT&CK/CWE are knowledge resources, not interchangeable with a compliance-control framework. A regional label does not establish legal applicability.

Edition notes identify checked anchor versions where available and otherwise explicitly direct the reader to verify the publisher. A catalog assembly date is not a statement that every publisher's latest edition was independently verified that day. Source links/availability can change. The app is discovery support, not legal, engineering, certification or compliance advice.

## Free operation and sharing

No paid API, AI calls, subscription, analytics, account database or runtime dependency is required. All application scripts run in the browser; the preview and catalog builder use Node's standard library. Publisher documents, training, certification and assessments may cost separately; access badges are indicative and are not price guarantees. The app never buys or subscribes to anything.

The owner approved public read-only sharing on October 13, 2026. Open [Framework Navigator](https://framework-navigator.brgoin82.chatgpt.site/) without signing in; classmates can search, filter, read, copy and follow official links. There are no visitor write endpoints or administrative edits in the app. A public link may be forwarded. Source changes still require repository-owner/collaborator permissions; public visibility does not grant push access.

Public source and documentation: [brgoin82-bit/framework-navigator](https://github.com/brgoin82-bit/framework-navigator). This repository is a clean initial source export, excluding hosting identity, credentials, local runtime files and private source history. The hosted Site is managed separately: a GitHub push alone does not redeploy it. After owner edits, run the builder and tests, then publish the validated `dist` folder using the configured static host or Sites deployment workflow. Preserve the prior deployment for rollback.

## Setup on Windows

Requires Node 22.13+ and a modern browser. No npm install is needed. PowerShell, current directory this project:

```powershell
& 'C:\Program Files\nodejs\node.exe' scripts/build-catalog.mjs
& 'C:\Program Files\nodejs\node.exe' --test --test-concurrency=1 tests/*.test.mjs
& 'C:\Program Files\nodejs\node.exe' scripts/serve.mjs 5182
```

Open http://127.0.0.1:5182 . This temporary preview is loopback-only and does not alter SignalWatch or NIST Navigator. Share the hosted URL, not localhost. The entire `dist` directory can be served by a static host or homelab web server; enforce appropriate HTTPS/access/header configuration there. The local preview is not an Internet-facing production server.

## Use

Type a name, abbreviation, subject or partial word. Suggestions appear underneath; use mouse, Up/Down/Enter, or Escape to dismiss. Examples: `grc`, `ISO27001`, `SOC2`, `credit cards`, `cloud`, `data center`. Small letter typos are supported. Numeric standard identifiers are not fuzzy-substituted; prefixes remain supported. This is heuristic matching, not an unrestricted natural-language AI system.

Choose a sidebar subject and optionally combine Publisher, Resource type, Access and Region filters. Counts on the sidebar/dropdowns describe the whole library; the results total reflects current filters. Reset clears all filters. Results paginate 20 at a time without a hidden first-page-only cap. A related-results message means only some search words matched.

Open the official source and check current edition, terms and applicability. Expand **Edition, scope & access notes** for the catalog's limitations. **About & coverage** explains the distinction between types and the maintenance model. **Copy share link** copies the hosted address; on localhost it warns that the address is local.

**Dark high contrast** toggles themes. **Accent** opens the same smooth in-app panel as NIST Navigator: named presets, Hue/Saturation/Lightness sliders and validated hex input, with a live applied-color preview. Mouse and keyboard changes work. Paints are coalesced to animation frames and storage is written only on commit/Done/theme changes. Contrast correction targets 4.5:1 against defined main surfaces; black/white filled-button text is selected by contrast. The preference key `framework-navigator-appearance` is separate from NIST Navigator.

## Catalog maintenance and refresh

Edit `data/frameworks.tsv`, preserving the header and ten pipe-separated fields. No field may contain a literal pipe. Use a unique lowercase ID, an allowed resource type/access tag/subject, a primary-publisher HTTPS URL, a brief original summary and an honest edition note. Change allowed destinations or classifications only through reviewed source changes.

Run the builder, then tests. The builder bounds file size, validates every record, rejects duplicates/unreviewed links, writes a uniquely named temporary file, reads it back, and replaces the generated catalog only after validation. Original TSV remains editable and unchanged by the builder. `meta.sourceSha256` fingerprints that local source; it is not a publisher signature or assurance that the metadata is current.

**Refresh catalog** reloads the latest hosted JSON, preserves active search/filter values, and returns to page 1. It does not discover new resources, download publisher standards, or update editions automatically. There is no unattended monthly framework-research process in this version. No AI heartbeat or other recurring credit-consuming task was created. Unlike the NIST bulk source, these publishers have no single common monthly catalog feed. An honest automated update would need separately verified publisher-specific data paths.

Republish the validated static artifact after owner changes; local changes alone do not update a hosted Site. A failed browser refresh retains the prior search engine/results. A missing or invalid initial catalog displays a visible failure—not a healthy empty library.

## Architecture

Buildless static HTML/CSS/ES modules with separate presentation, pure matching/validation, curated data and owner-side generation. Approximately 117 metadata records are small enough for bounded browser-local matching without a shared search backend.

```text
data/frameworks.tsv          Editable primary-publisher reference metadata
scripts/build-catalog.mjs    Validated atomic catalog generation
scripts/serve.mjs            Loopback fixed-file preview
dist/catalog.json           Generated public or access-controlled metadata
dist/search-core.mjs        Validation, facets, matching, synonyms and pagination
dist/catalog-loader.mjs     Bounded same-origin read-only acquisition
dist/app.mjs                Search, suggestions, filters, cards, refresh and sharing
dist/appearance.mjs/.css    Independent theme/color controls and preferences
tests/                     Catalog/search/security/appearance regression checks
```

## Security Controls

- Same-origin read-only JSON fetches, 15-second timeout, 2 MB limit, no credentials or redirects. There is no arbitrary-destination fetch or public writer.
- Required fields, length/count bounds, unique IDs, resource classifications, known subject groups and official HTTPS destination allowlists are validated before use.
- Text renders through DOM `textContent`/nodes; source URLs reject script schemes, credentials, unexpected ports and spoofed hosts. New-window links use `noopener noreferrer`.
- Meta CSP restricts scripts/styles/data to the app origin. `_headers` supplies additional headers on supporting hosts; production header enforcement is host-dependent, not assumed.
- Preview binds 127.0.0.1, checks Host/Origin, permits GET/HEAD only, and serves fixed files—not source, credentials, Git metadata or `.runtime` state.
- No personal/student/card data, search history, AI prompts or saved queries are stored. Only validated theme/color preferences live in the visitor's browser; corrupt or denied storage cannot prevent startup. Host/source providers still see ordinary connection metadata.
- No added third-party runtime packages, install scripts or paid service credentials. Hosting authorization stays with the platform; repository credentials are never included in client assets.

## Threat model and Known Security Limitations

Trust boundaries are owner-edited metadata into the builder, published JSON into the browser, and owner hosting access into deployment. Validation and text-only rendering reduce malicious markup/URL and incomplete-catalog risks. They do not eliminate compromised owner/publisher accounts, misleading source metadata, browser extensions, provider outages or stale editions. A trusted source domain is not proof that every linked resource is current or applicable. Hosted access policy is separate from app code.

No complete penetration test, formal compliance certification, full screen-reader test, long-duration load or every-browser/OS verification is claimed. Appearance tests validate defined color surfaces, not every assistive-technology interaction. Local generation is recoverable from TSV and Git/deployment history; same-disk copies are not independent disaster-recovery backups.

## Tests and review status

**30 sequential tests passed** on October 13, 2026 (~0.3 seconds), covering full TSV-to-JSON row counts, all subjects, search/prefix/typos/abbreviations/numbers, suggestions, combined facets, cost filters, classification, full pagination, sorting, empty/related results, malicious-looking input, link/schema rejection, bounded refresh errors, loopback file/Host/Origin controls, independent appearance storage and rapid-input coalescing. Browser testing caught numeric fuzzy substitution; it was fixed and regression-tested before release.

Actual local browser checks covered joined-number search, keyboard subject suggestions, PCI publisher/type/free filters, filter-preserving refresh, page navigation, the coverage dialog, and dark/purple appearance. Full reference-link availability and every publisher's live edition were not exhaustively checked. See [verification notes](docs/TESTING.md) and [source/editing guide](docs/CATALOG.md).

- Last Security Review Date: October 13, 2026.
- Last Architecture Review Date: October 13, 2026.
- Standards/Guidance Reviewed: NIST CSF/RMF/AI resources; ISO family/management-standard listings; OWASP project listings; CIS/CSA/MITRE resources; official Sites hosting guidance; prior verified color-control implementation.
- Dependencies Reviewed: none added; standard browser/Node APIs only.
- Known Vulnerabilities Found: none identified in this bounded implementation review; no exhaustive security scan performed.
- Remediation Status: numeric identifier matching corrected before release; inherited color-picker repair retained.
- Residual Risks: coverage/currency gaps, link changes, upstream/owner/host compromise and availability as above.
- Next Recommended Review: before new publisher destinations, data imports, authentication or hosting changes.

Primary starting sources include [NIST](https://www.nist.gov/cyberframework), [ISO families](https://committee.iso.org/standard/iso-iec-27000-family), [OWASP](https://owasp.org/projects), [CSA CCM](https://cloudsecurityalliance.org/artifacts/cloud-controls-matrix-v4-1), [SCF](https://securecontrolsframework.com/free-content), [Open FAIR](https://www.opengroup.org/open-fair), [PCI SSC](https://www.pcisecuritystandards.org/document_library/), and the individual official references in the source catalog. This app is not endorsed by those publishers.
