---
title: Local package testing by copying dist
summary: Build a package locally, remove its installed dist directory, and copy the new dist into the consuming project's node_modules to test without publishing, npm link, or npm pack; this requires a package that builds into dist.
sources:
  - how-to/cp-dist-workflow/README.md
kind: concept
createdAt: "2026-11-11T10:54:45.330Z"
updatedAt: "2026-11-11T10:54:45.330Z"
tags:
  - local-development
  - npm-packages
  - build-artifacts
aliases:
  - local-package-testing-by-copying-dist
  - LPTBCD
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Local package testing by copying dist

Copying a locally built package’s `dist` directory into another project’s `node_modules` allows testing changes without publishing to npm. This workflow uses direct file copying and requires neither `npm link` nor `npm pack`. ^[how-to/cp-dist-workflow/README.md:1-9]

## Workflow

First, make changes in the source package and build it. The source example uses `yarn build` in the package directory. ^[how-to/cp-dist-workflow/README.md:13-18]

```bash
cd <source-package>
yarn build
```

Delete the installed package’s old `dist` directory, then copy the newly built directory into the installed package’s root. ^[how-to/cp-dist-workflow/README.md:39-46]

```bash
rm -rf <target-project>/node_modules/<package-name>/dist
cp -R <source-package>/dist <target-project>/node_modules/<package-name>/
```

For a Next.js target project, switch to its directory, remove `.next`, and restart the development server. Next.js caches modules, so changes may not appear without clearing that directory; see [[Next.js cache invalidation after local package changes]]. ^[how-to/cp-dist-workflow/README.md:30-35, how-to/cp-dist-workflow/README.md:54-56]

```bash
cd <target-project>
rm -rf .next
yarn dev
```

## Limitations

This workflow is intended for local development and testing and requires a package that builds into a `dist` directory. The copied files are [[Temporary overrides in node_modules|temporary overrides in node_modules]]: running `yarn install` or `npm install` overwrites the changes. ^[how-to/cp-dist-workflow/README.md:60-64]

## Sources

- [cp-dist-workflow — lokální propojení npm balíčku](how-to/cp-dist-workflow/README.md)
