---
title: Idempotent and Non-Destructive Seeding
summary: The seed script deletes nothing and skips existing records matched by slug or title when run repeatedly.
sources:
  - how-to/restore-db/README.md
kind: concept
createdAt: "2026-11-11T11:01:39.373Z"
updatedAt: "2026-11-11T11:01:39.373Z"
tags:
  - data-seeding
  - idempotency
aliases:
  - idempotent-and-non-destructive-seeding
  - Non-Destructive Seeding and Idempotent
  - IANS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Idempotent and Non-Destructive Seeding

Idempotentní a nedestruktivní seedování umožňuje doplnit vývojová data bez mazání existujících záznamů. Skript `seedDevData.js` pro Strapi v5 nic nemaže a při opakovaném spuštění přeskakuje existující záznamy podle shody `slug` nebo `title`. ^[how-to/restore-db/README.md:88-92]

## Účel a vytvářená data

Skript je určen k naplnění čisté lokální databáze ukázkovými daty, například když starý SQL dump obsahuje nevalidní data a Strapi v5 s ním nenastartuje. Vytváří kategorie, tagy, jeden placeholder obrázek, pět blogových příspěvků a čtyři stránky. Příspěvky a stránky nejprve vytváří jako drafty a následně publikuje; obrázek se v development režimu ukládá lokálně. ^[how-to/restore-db/README.md:79-92]

Záznamy vznikají prostřednictvím [[Seeding Through the Strapi Documents API|Strapi Documents API]], takže procházejí validacemi a lifecycles. Tím se zajišťuje správné generování `generatedUrl` a fungování kontrol duplicit. ^[how-to/restore-db/README.md:86-86]

## Hranice nedestruktivního chování

Nedestruktivní je samotný seedovací skript. Ukázkový postup pro [[Clean Database Initialization for Strapi v5|čistou inicializaci databáze]] před seedováním výslovně obsahuje odstranění a opětovné vytvoření databáze. Poté se spustí Strapi, které vytvoří schéma a provede migrace, a teprve následně se doplní data. Bezpečnost opakovaného seedování proto nelze vztahovat na celý tento postup. ^[how-to/restore-db/README.md:88-91, how-to/restore-db/README.md:119-131]

## Konfigurace a spuštění

Skript vyžaduje běžící PostgreSQL kontejner, Node.js a Strapi projekt s nainstalovanými závislostmi a již vytvořeným databázovým schématem. Připojení načítá z `DATABASE_URL` v projektovém `.env`; závislosti `@strapi/strapi` a `dotenv` používá z projektového `node_modules`. Cestu k projektu lze změnit proměnnou `STRAPI_APP_DIR`. ^[how-to/restore-db/README.md:94-100, how-to/restore-db/README.md:133-138]

Následující příkaz spustí seedování s explicitně nastavenou cestou ke Strapi projektu. ^[how-to/restore-db/README.md:114-117]

```bash
STRAPI_APP_DIR=/jina/cesta/strapi node seedDevData.js
```

## Sources

- [how-to/restore-db/README.md](how-to/restore-db/README.md)
