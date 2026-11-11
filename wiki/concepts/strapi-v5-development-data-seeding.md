---
title: Strapi v5 Development Data Seeding
summary: seedDevData.js populates a clean local Strapi v5 database with sample categories, tags, posts, pages, and a locally uploaded placeholder image.
sources:
  - how-to/restore-db/README.md
kind: concept
createdAt: "2026-11-11T11:01:38.382Z"
updatedAt: "2026-11-11T11:01:38.382Z"
tags:
  - strapi
  - development
  - data-seeding
aliases:
  - strapi-v5-development-data-seeding
  - SVDDS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Strapi v5 Development Data Seeding

Skript `seedDevData.js` naplní čistou lokální databázi Strapi v5 ukázkovými vývojovými daty. Hodí se zejména tehdy, když starý SQL dump obsahuje nevalidní data a Strapi v5 s ním nenastartuje. Místo [[Restoring a Strapi SQL database dump|obnovy SQL zálohy]] vytvoří čerstvá validní data. ^[how-to/restore-db/README.md:75-79]

## Vytvářená data

Seed zahrnuje tři kategorie blogových příspěvků, dvě kategorie stránek, čtyři tagy a dvě kategorie release notes. Dále vytvoří placeholder obrázek ve formátu PNG o rozměrech 600 × 400 pixelů v `public/uploads`, pět blogových příspěvků a čtyři stránky. Příspěvky a stránky vznikají nejprve jako draft a poté se publikují, čímž vzniknou dvojice draft a publikovaná verze podle [[Strapi v5 Draft and Publish Seeding|Draft & Publish ve Strapi v5]]. ^[how-to/restore-db/README.md:81-84]

Data se vytvářejí přes [[Seeding Through the Strapi Documents API|Strapi Documents API]]. Procházejí tak validacemi a lifecycle mechanismy; `generatedUrl` se generuje správně a kontroly duplicit zůstávají funkční. ^[how-to/restore-db/README.md:86-86]

## Chování při opakovaném spuštění

Skript je nedestruktivní: nic nemaže. Podporuje [[Idempotent and Non-Destructive Seeding|idempotentní seedování]], protože existující záznamy při opakovaném spuštění přeskočí podle shody slug nebo title. V development režimu ukládá upload lokálně a nic nenahrává do cloudu. ^[how-to/restore-db/README.md:88-92]

## Konfigurace a požadavky

Proměnná `STRAPI_APP_DIR` určuje cestu ke Strapi projektu; výchozí hodnota je `~/work/direct/projects/direct.cz-cms/strapi`. Připojení k databázi skript načítá z `DATABASE_URL` v projektovém `.env`. Závislosti `@strapi/strapi` a `dotenv` používá z projektového `node_modules`, takže musí být předem nainstalované pomocí `yarn install`. ^[how-to/restore-db/README.md:94-100]

Pro spuštění je potřeba Node.js, Docker s běžícím kontejnerem `postgres_strapi` a databáze s vytvořeným schématem. Schéma musí být připravené alespoň jedním spuštěním `yarn develop`. ^[how-to/restore-db/README.md:133-138]

## Spuštění

Běh PostgreSQL kontejneru lze ověřit příkazem `docker ps`. Seedovací skript lze následně spustit z libovolného adresáře následujícím příkazem. ^[how-to/restore-db/README.md:102-112]

```bash
node /Users/martin.adamec/work/how-to/restore-db/seedDevData.js
```

Jinou cestu ke Strapi projektu lze předat prostřednictvím `STRAPI_APP_DIR`. ^[how-to/restore-db/README.md:114-117]

```bash
STRAPI_APP_DIR=/jina/cesta/strapi node seedDevData.js
```

## Čistý start databáze

Workflow pro [[Clean Database Initialization for Strapi v5|čistou inicializaci Strapi v5]] začíná smazáním a opětovným vytvořením databáze. Tento krok odstraní její stávající obsah. Následuje spuštění Strapi, které vytvoří schéma a provede migrace, a nakonec spuštění seedu. Mazání databáze je samostatný přípravný krok; samotný seed nic nemaže. ^[how-to/restore-db/README.md:90-91, how-to/restore-db/README.md:119-130]

```bash
# 1. Recreate the database
docker exec postgres_strapi psql -U postgres -c "DROP DATABASE postgres_strapi WITH (FORCE);"
docker exec postgres_strapi psql -U postgres -c "CREATE DATABASE postgres_strapi;"

# 2. Create the schema and run migrations
cd ~/work/direct/projects/direct.cz-cms/strapi && yarn develop

# 3. Seed development data
node /Users/martin.adamec/work/how-to/restore-db/seedDevData.js
```

## Sources

- [how-to/restore-db/README.md](how-to/restore-db/README.md)
