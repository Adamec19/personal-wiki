---
title: Strapi v5 Draft and Publish Seeding
summary: Sample blog posts and pages are created as drafts and then published to produce Strapi v5 draft and published counterparts.
sources:
  - how-to/restore-db/README.md
kind: concept
createdAt: "2026-11-11T11:01:42.350Z"
updatedAt: "2026-11-11T11:01:42.350Z"
tags:
  - strapi
  - content-publishing
  - data-seeding
aliases:
  - strapi-v5-draft-and-publish-seeding
  - Publish Seeding and Strapi v5 Draft
  - SVDAPS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Strapi v5 Draft and Publish Seeding

Ve Strapi v5 vytváří skript `seedDevData.js` ukázkový obsah nejprve jako draft a následně jej publikuje. Pro 5 blogových příspěvků a 4 stránky tak vznikají draftové a publikované protějšky odpovídající mechanismu draft & publish ve v5. ^[how-to/restore-db/README.md:79-84]

## Vytváření obsahu

Skript používá [[Seeding Through the Strapi Documents API|Strapi Documents API]]. Vytvářená data proto procházejí validacemi a lifecycles; správně se generuje `generatedUrl` a fungují kontroly duplicit. ^[how-to/restore-db/README.md:86-86]

Vedle příspěvků a stránek vytváří také 3 kategorie blogových příspěvků, 2 kategorie stránek, 4 tagy, 2 kategorie release notes a jeden placeholder obrázek ve formátu PNG o rozměrech 600 × 400 pixelů. Obrázek se nahrává do `public/uploads`. ^[how-to/restore-db/README.md:81-84]

## Příprava a spuštění

Seedování je určeno pro čistou lokální databázi. Hodí se například tehdy, když starý SQL dump obsahuje nevalidní data a Strapi v5 s ním nenastartuje. Databáze už musí mít schéma vytvořené alespoň jedním spuštěním `yarn develop`; tento postup souvisí s [[Clean Database Initialization for Strapi v5]]. ^[how-to/restore-db/README.md:79-79, how-to/restore-db/README.md:133-138]

Před spuštěním musí běžet PostgreSQL kontejner `postgres_strapi` a musí být dostupný Node.js i Strapi projekt s nainstalovanými závislostmi. Skript čte připojení `DATABASE_URL` z projektového `.env` a načítá `@strapi/strapi` a `dotenv` z projektového `node_modules`. ^[how-to/restore-db/README.md:100-100, how-to/restore-db/README.md:133-138]

Skript lze spustit odkudkoliv následujícím příkazem. ^[how-to/restore-db/README.md:109-112]

```bash
node /Users/martin.adamec/work/how-to/restore-db/seedDevData.js
```

Cestu k jinému Strapi projektu lze zadat proměnnou `STRAPI_APP_DIR`. ^[how-to/restore-db/README.md:114-117]

```bash
STRAPI_APP_DIR=/jina/cesta/strapi node seedDevData.js
```

## Opakované spuštění

Skript nic nemaže a při opakovaném spuštění přeskakuje existující záznamy podle shody `slug` nebo `title`. Jde tedy o [[Idempotent and Non-Destructive Seeding|idempotentní a nedestruktivní seedování]]. Upload v development módu probíhá lokálně a nic se nenahrává do cloudu. ^[how-to/restore-db/README.md:88-92]

## Sources

- [how-to/restore-db/README.md](how-to/restore-db/README.md)
