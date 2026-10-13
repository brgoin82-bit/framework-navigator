# Catalog curation contract

The source of truth is `data/frameworks.tsv`. Header:

```text
id|title|publisher|type|areas|access|region|url|summary|edition
```

One resource family per line; exactly ten fields. Areas and regions use comma-separated values. Preserve publisher names and identifiers; do not claim an edition is current when that has not been checked. Descriptions are short original discovery aids, not copied normative control text. Do not put private research, credentials or personal information in this file.

Allowed types/access/categories and source hosts are explicit in `dist/search-core.mjs`. Adding an unknown host requires a reviewed allowlist change, not a bypass. Prefer the exact official resource page; when only an official family/publisher directory is used, say so in the edition note. Never replace an inaccessible paid standard with an unauthorized copy.

After editing, run `node scripts/build-catalog.mjs`, then `node --test --test-concurrency=1 tests/*.test.mjs`. Review the diff and verify the changed source's title, edition, availability and licensing. Deploy the verified static artifact through the project's configured host. Keep prior source commits and deployment versions for rollback. Do not force-push or overwrite unrelated work.

The initial 117 rows build into exactly 117 JSON records with 44 publisher labels and 16 populated areas. This verifies import completeness **relative to this file**, not completeness of all worldwide frameworks. Region labels describe context, not mandatory law. Access badges describe reading material, not the entire cost of certification, assessment or implementation. Source editions require continuing owner review.

The app has no live publisher ingestion or scheduled discovery. Refresh rereads the hosted catalog only. Do not turn an HTTP-success/link check or a regenerated assembly date into an assertion that a framework's legal scope or latest edition was reviewed.
