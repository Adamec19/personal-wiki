---
title: Next.js cache invalidation after local package changes
summary: The workflow deletes .next and restarts the development server so cached modules do not prevent copied package changes from appearing.
sources:
  - how-to/cp-dist-workflow/README.md
kind: concept
createdAt: "2026-11-11T10:54:47.035Z"
updatedAt: "2026-11-11T10:54:47.035Z"
tags:
  - nextjs
  - caching
  - local-development
aliases:
  - nextjs-cache-invalidation-after-local-package-changes
  - NCIALPC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Next.js cache invalidation after local package changes

Při [[Lokální testování npm balíčku kopírováním dist|lokálním testování balíčku kopírováním `dist`]] do `node_modules` nemusí Next.js změny ihned zobrazit, protože cachuje moduly. Po nahrazení balíčku je proto součástí postupu smazání adresáře `.next` a opětovné spuštění vývojového serveru. ^[how-to/cp-dist-workflow/README.md:25-35, how-to/cp-dist-workflow/README.md:54-56]

## Postup

Nejprve upravte a vybuilděte zdrojový balíček. Poté smažte jeho starou složku `dist` v `node_modules` cílového projektu a nahraďte ji nově vytvořenou složkou `dist`. ^[how-to/cp-dist-workflow/README.md:13-28]

V kořenovém adresáři cílového projektu smažte `.next` a znovu spusťte vývojový server. Odstranění cache zajistí, aby zobrazení změn nebránily dříve cachované moduly. ^[how-to/cp-dist-workflow/README.md:30-35, how-to/cp-dist-workflow/README.md:54-56]

```bash
rm -rf .next && yarn dev
```

## Omezení

Tento postup slouží pouze pro lokální vývoj a testování balíčků, které vytvářejí výstup ve složce `dist`. Úpravy v `node_modules` jsou dočasné: další `yarn install` nebo `npm install` je přepíše. ^[how-to/cp-dist-workflow/README.md:60-64]

## Sources

- [cp-dist-workflow — lokální propojení npm balíčku](how-to/cp-dist-workflow/README.md)
