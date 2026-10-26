# Operations and recovery

Documentation release 0.1.1 · October 26, 2026

## Run the existing snapshot

On Windows, use PowerShell in the cloned repository. Node.js 22.13 or later must be on PATH. There are no npm dependencies to install.

```powershell
node --test --test-concurrency=1 tests/*.test.mjs
node scripts/serve.mjs 5182
```

Open http://127.0.0.1:5182/. Stop your preview with Ctrl+C. The helper binds loopback and serves a fixed list of public assets; use a production static host for sharing.

## Maintain and publish

Edit `data/frameworks.tsv` according to [CATALOG.md](CATALOG.md), run `node scripts/build-catalog.mjs`, then rerun the tests. The builder changes the assembly timestamp and fingerprints the exact source bytes. Review the source and generated catalog diff before committing; a new assembly timestamp does not mean every publisher edition was checked.

Publish the complete `dist/` directory using the existing hosting arrangement. GitHub source updates do not themselves redeploy the hosted frontend. `_headers` works only on hosts that support that format; verify the deployed response headers separately. No new hosting purchase or deployment is required by this documentation update.

The browser Refresh button loads same-origin `catalog.json`. It does not run the builder. This app has no automatic publisher ingestion or scheduled monthly research.

## Recovery

Keep the source TSV and Git history. Review an earlier known-good commit in a separate checkout before restoring. Prefer a new revert commit for a published mistake; never rewrite shared history or move an existing release tag. Redeploy the prior verified static artifact if the frontend is broken. A same-disk checkout is not an independent backup.

| Problem | Action |
| --- | --- |
| Missing/invalid catalog | Inspect the builder error, repair the TSV, rebuild and run tests. Do not bypass validation. |
| Refresh failed | Check host availability. Loaded results remain usable; retry later. |
| Port already used | Choose another port from 1024–65535, such as `node scripts/serve.mjs 5183`. |
| No results | Reset filters, then search an abbreviation or shorter phrase. |
| Publisher link changed | Verify the official replacement, update the TSV and regenerate. |
| Preferences fail to save | Browser storage may be blocked; the app can still run. |

There is no application database, visitor account store or server-side search log. Only appearance preferences persist in browser storage. Static hosts and linked publishers can receive ordinary connection metadata.
