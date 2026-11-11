---
title: PostgreSQL containers for Strapi
summary: Run PostgreSQL instances for Strapi in Docker with configured credentials, database names, host ports, image versions, and persistent named volumes.
sources:
  - how-to/direct-dev/strapi/README.md
kind: concept
createdAt: "2026-11-11T10:55:38.695Z"
updatedAt: "2026-11-11T10:55:38.695Z"
tags:
  - strapi
  - postgresql
  - docker
aliases:
  - postgresql-containers-for-strapi
  - PCFS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# PostgreSQL containers for Strapi

PostgreSQL kontejnery pro Strapi lze vytvořit pomocí `docker run`. Uvedená konfigurace používá databázi `postgres_strapi`, uživatele `postgres` a heslo `direct`. Dvě varianty kontejneru mají odlišné názvy, hostitelské porty a datové svazky. ^[how-to/direct-dev/strapi/README.md:5-25]

## Vytvoření kontejnerů

Kontejner `postgres_strapi` používá image `postgres:15`, zpřístupňuje PostgreSQL na hostitelském portu `5432` a připojuje svazek `postgres_strapi_data` do `/var/lib/postgresql/data`. ^[how-to/direct-dev/strapi/README.md:5-14]

```bash
docker run -d --name postgres_strapi \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=direct \
  -e POSTGRES_DB=postgres_strapi \
  -p 5432:5432 \
  -v postgres_strapi_data:/var/lib/postgresql/data \
  postgres:15
```

Druhý kontejner `postgres_strapi_2` používá image `postgres:15.3-alpine3.18` a samostatný svazek `postgres_strapi_2_data`. Hostitelský port `5433` mapuje na port `5432` uvnitř kontejneru. Název databáze zůstává `postgres_strapi`. ^[how-to/direct-dev/strapi/README.md:16-25]

```bash
docker run -d --hostname postgres_strapi_2 --name postgres_strapi_2 \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=direct \
  -e POSTGRES_DB=postgres_strapi \
  -p 5433:5432 \
  -v postgres_strapi_2_data:/var/lib/postgresql/data \
  postgres:15.3-alpine3.18
```

## Správa a kontrola databáze

Běžící kontejnery vypíše `docker ps`, všechny kontejnery včetně zastavených `docker ps -a`. Kontejner lze zastavit příkazem `docker stop` a znovu spustit příkazem `docker start`; souvisejícím tématem je [[Správa životního cyklu Docker kontejnerů]]. ^[how-to/direct-dev/strapi/README.md:96-104]

```bash
docker ps
docker ps -a
docker stop postgres_strapi
docker start postgres_strapi
```

Databázi lze kontrolovat pomocí `psql` spuštěného přes `docker exec`. Příkaz `\l` vypisuje databáze a `\dt` tabulky vybrané databáze. Tabulka `admin_users` obsahuje administrátorské účty Strapi; další operace popisuje [[Managing Strapi administrator records with psql]]. ^[how-to/direct-dev/strapi/README.md:106-122]

```bash
docker exec -it postgres_strapi psql -U postgres -c "\l"
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "\dt"
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "SELECT email FROM admin_users;"
```

## Import SQL dumpu

Zdroj uvádí import pomocí `python3 restore_db.py` nebo ruční postup: zkopírovat SQL dump do kontejneru a následně jej provést příkazem `psql -f`. Podrobněji s tím souvisí [[Restoring a Strapi SQL database dump]] a [[Kopírování souborů mezi hostitelem a kontejnerem]]. ^[how-to/direct-dev/strapi/README.md:29-40]

```bash
docker cp /Users/martin.adamec/work/how-to/restore-db/db_strapi_backup_22.12_2026.sql postgres_strapi:/tmp/restore.sql
docker exec -i postgres_strapi psql -U postgres -d postgres_strapi -f /tmp/restore.sql
```

## Připojení z DBeaveru

Pro [[Connecting DBeaver to Strapi PostgreSQL databases|připojení z DBeaveru]] se používá hostitel `localhost`, port `5432` pro `postgres_strapi` nebo `5433` pro `postgres_strapi_2`, uživatel `postgres`, heslo `direct` a databáze `postgres_strapi`. Obnovení připojení zdroj popisuje jako pravý klik → Invalidate/Reconnect → F5. ^[how-to/direct-dev/strapi/README.md:126-134]

## Sources

- [Strapi Database - Quick Commands](how-to/direct-dev/strapi/README.md)
