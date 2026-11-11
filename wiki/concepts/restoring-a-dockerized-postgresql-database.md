---
title: Restoring a Dockerized PostgreSQL Database
summary: restore_strapi.py copies a SQL backup into Docker, terminates connections, drops and recreates the database, imports the backup, and lists tables to check the result.
sources:
  - how-to/restore-db/README.md
kind: concept
createdAt: "2026-11-11T11:01:30.086Z"
updatedAt: "2026-11-11T11:01:30.086Z"
tags:
  - postgresql
  - docker
  - backup-restore
aliases:
  - restoring-a-dockerized-postgresql-database
  - RADPD
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Restoring a Dockerized PostgreSQL Database

[[obnova-postgresql-databáze-v-dockeru|Obnova PostgreSQL databáze v Dockeru]] pomocí skriptu `restore_strapi.py` nahraje celou zálohu ze souboru `.sql` do databáze v kontejneru. Slouží k návratu do staršího stavu, přípravě vývojového prostředí od nuly nebo obnovení databáze po chybné změně. ^[how-to/restore-db/README.md:12-19]

## Průběh obnovy

Skript zkopíruje zálohu z hostitelského počítače do kontejneru, ukončí všechna aktivní připojení k databázi a stávající databázi smaže příkazem `DROP DATABASE`. Následně vytvoří prázdnou databázi pomocí `CREATE DATABASE`, naimportuje zálohu a vypíše seznam tabulek pro ověření výsledku. **Obnova tedy odstraní současný obsah cílové databáze.** ^[how-to/restore-db/README.md:23-30]

## Požadavky a konfigurace

Před spuštěním musí běžet Docker i kontejner `postgres_strapi`, musí být nainstalovaný Python 3 a záložní `.sql` soubor musí existovat na cestě uvedené v `HOST_SQL_PATH`. ^[how-to/restore-db/README.md:66-71]

Na začátku souboru `restore_strapi.py` zkontroluj následující proměnné. Nejčastěji se mění cesta k záloze v `HOST_SQL_PATH`. ^[how-to/restore-db/README.md:34-43]

| Proměnná | Význam | Výchozí hodnota |
|---|---|---|
| `CONTAINER` | Název Docker kontejneru | `postgres_strapi` |
| `DB` | Název databáze | `postgres_strapi` |
| `USER` | PostgreSQL uživatel | `postgres` |
| `HOST_SQL_PATH` | Cesta k záložnímu `.sql` souboru | Nastavit podle umístění zálohy |

## Spuštění

Nejprve ověř běžící kontejner příkazem `docker ps` a poté spusť skript pomocí Pythonu 3. Zdroj uvádí následující příkazy. ^[how-to/restore-db/README.md:52-62]

```bash
docker ps
python3 /Users/martin.adamec/work/how-to/restore-db/restore_strapi.py
```

Po importu skript vypíše seznam tabulek jako kontrolu výsledku obnovy. ^[how-to/restore-db/README.md:29-30]

## Alternativa pro Strapi v5

Pokud starší SQL dump obsahuje nevalidní data a Strapi v5 s ním nenastartuje, lze místo obnovy připravit čistou databázi a naplnit ji ukázkovými daty pomocí `seedDevData.js`. Tento postup popisuje [[Strapi v5 Development Data Seeding]]; skript vytváří data přes [[Seeding Through the Strapi Documents API|Strapi Documents API]], aby prošla validacemi a lifecycles. ^[how-to/restore-db/README.md:75-86]

## Sources

- [how-to/restore-db/README.md](how-to/restore-db/README.md)
