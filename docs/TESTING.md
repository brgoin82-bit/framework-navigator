# Verification record — 0.1.0

October 13, 2026 · Windows · Node 24.21.0

30 automated tests passed, zero failed/skipped/cancelled, in approximately 0.3 seconds. Run sequentially with `node --test --test-concurrency=1 tests/*.test.mjs` from the project.

The source build matched all 117 TSV rows to 117 unique validated records. All 16 subjects have results; 44 publisher labels are present. Tests cover matching and exact numeric identifiers, typo/prefix/synonym behavior, suggestions, combined subject/publisher/type/access/region filters, cost/type distinctions, six-page completeness without duplicates, clamped pages, stable sorting, no-results and related-result messages, unsafe URLs, invalid schema/duplicates, failed/corrupt HTTP responses, same-origin credential-free refresh, local traversal/Host/Origin/write rejection, and appearance preferences/contrast/coalescing.

Browser checks observed:

- Initial load: 117 resources, 44 publishers; all filter controls populated.
- `ISO27001` initially returned nearby numeric standards because generic typo matching included numbers. Fixed before release; the actual UI and regression test then returned only ISO/IEC 27001.
- Keyboard autocomplete selected Risk management and returned 12 resources.
- Publisher PCI SSC + Standard + Free resource returned five resources. Refresh preserved the publisher/filter selection and result count.
- Next navigated to page 2 of 6.
- The coverage dialog showed the real curation limitation.
- Dark mode and Violet preset visibly changed the rendered layout/accent; the repaired in-app picker is reused with a separate preference key.
- A narrow in-app-browser view showed responsive header, horizontally scrollable subject choices and usable search controls.

Not verified: every publisher's latest edition, every reference URL's continued availability, all historical or proprietary frameworks, every browser/OS, full screen-reader operation, prolonged load, disk-full/power-loss simulation or a complete penetration test. Unit contrast checks cover defined surfaces, not formal accessibility certification. No deep scanner, extra agent or recurring AI process ran.
