---
title: Temporary overrides in node_modules
summary: Direct changes to installed package files are temporary local development and testing overrides that yarn install or npm install can overwrite.
sources:
  - how-to/cp-dist-workflow/README.md
kind: concept
createdAt: "2026-11-11T10:54:51.231Z"
updatedAt: "2026-11-11T10:54:51.231Z"
tags:
  - dependency-management
  - node-modules
  - local-testing
aliases:
  - temporary-overrides-in-nodemodules
  - TOIN
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Temporary overrides in node_modules

Dočasné přepsání souborů v `node_modules` umožňuje použít lokálně sestavený npm balíček v jiném projektu bez publikování na npm. Popsaný postup kopíruje složku `dist` přímo do instalovaného balíčku a nevyžaduje `npm link` ani `npm pack`. ^[how-to/cp-dist-workflow/README.md:1-9]

## Postup

Nejprve proveď změny ve zdrojovém balíčku a sestav jej pomocí `yarn build`. Potom odstraň starou složku `dist` v cílovém projektu a nahraď ji novým sestavením. Tento postup předpokládá, že balíček ukládá výstup sestavení do `dist`; souvisí s [[Local package testing by copying dist]]. ^[how-to/cp-dist-workflow/README.md:13-28, how-to/cp-dist-workflow/README.md:64-64]

```bash
# Run in the source package
yarn build

# Replace placeholders with the actual paths
rm -rf <target-project>/node_modules/<package-name>/dist
cp -R <source-package>/dist <target-project>/node_modules/<package-name>/
```

V cílovém projektu poté restartuj vývojový server. U Next.js uvedený postup zahrnuje smazání `.next`, protože cache modulů může zabránit projevení změn. Podrobněji viz [[Next.js cache invalidation after local package changes]]. ^[how-to/cp-dist-workflow/README.md:30-35, how-to/cp-dist-workflow/README.md:54-56]

```bash
# Run in the target Next.js project
rm -rf .next
yarn dev
```

## Omezení

Úpravy v `node_modules` jsou dočasné: po spuštění `yarn install` nebo `npm install` se přepíší zpět. Tento způsob přepsání je určen pouze pro lokální vývoj a testování. ^[how-to/cp-dist-workflow/README.md:60-64]

## Sources

- [cp-dist-workflow — lokální propojení npm balíčku](how-to/cp-dist-workflow/README.md)
