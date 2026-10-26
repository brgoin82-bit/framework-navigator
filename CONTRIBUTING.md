# Contributing

Read [the documentation index](docs/INDEX.md) before changing behavior. Use a descriptive branch such as `codex/describe-the-change` from current `main`; keep each change focused and open a pull request for review. Do not include unrelated local work.

## Local verification

Use Windows PowerShell in the repository with Node.js 22.13+ on PATH.

```powershell
node --test --test-concurrency=1 tests/*.test.mjs
```

For intentional catalog edits, follow [CATALOG.md](docs/CATALOG.md), run `node scripts/build-catalog.mjs`, then rerun the tests and review the generated diff.

Check keyboard search/suggestions, combined filters, pagination, refresh, appearance and failure feedback when changing the interface. Add focused regression coverage for behavior changes. Preserve the existing validators, network bounds, safe URL policies and source attribution.

Update the affected guides, changelog and [version metadata](docs/VERSIONING.md) for a release. Do not publish credentials, personal research, local paths, runtime caches or hosting configuration. Review the staged diff and exact remote/branch before pushing. Do not add paid services, runners or credit-consuming automation without the owner's explicit cost approval.

The application source and contributions use the existing [MIT license](LICENSE). Do not copy proprietary standard text into the catalog. Report suspected security issues as described in [SECURITY.md](SECURITY.md).
