# Versioning and releases

Current documentation release: **0.1.1**. Previous application version: **0.1.0**, source commit `3303f22`. The October 26, 2026 patch packages documentation and version metadata; it does not introduce new app features.

## Policy

Use MAJOR.MINOR.PATCH and annotated Git tags named `vMAJOR.MINOR.PATCH`. These 0.x releases remain in initial development. Use a patch for compatible fixes or a packaged documentation update, a minor for features, and explicitly document incompatible changes. Decide and document the stable compatibility contract before 1.0.0.

- Update `package.json`, README title, changelog and current release notes together.
- Keep historical release/test dates intact. Never call old evidence a new test run.
- Run the sequential tests and record the environment, result and limits before tagging.
- Review source, version files, links and secrets, commit the reviewed changes, then create an annotated tag on that commit. Never move a published tag.
- Push the intended branch and explicit new tag without force. A Git tag identifies source; a GitHub Release adds a release page and notes. Only describe a GitHub Release as published after verifying it.
- A source tag does not deploy the hosted website. Keep website deployment and source release status separate.

## Catalog versions

The source TSV fingerprint and assembly timestamp in `dist/catalog.json` identify the curated snapshot. Assembly is not a live edition review. Review catalog-only changes separately from application features and document meaningful coverage changes.

## Recovery

Use a separate checkout of the previous verified tag/commit for comparison. Prefer a new revert commit for an already-published mistake. Restore the frontend through the existing hosting deployment history. Do not force-push, retag or silently replace a release archive.

References reviewed October 26, 2026: [Semantic Versioning](https://semver.org/) and [GitHub releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases).
