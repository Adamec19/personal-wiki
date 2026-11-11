---
title: Connecting DBeaver to Strapi PostgreSQL databases
summary: Connect DBeaver to the local PostgreSQL instances through their mapped host ports and refresh connections with Invalidate/Reconnect and F5.
sources:
  - how-to/direct-dev/strapi/README.md
kind: concept
createdAt: "2026-11-11T10:55:52.243Z"
updatedAt: "2026-11-11T10:55:52.243Z"
tags:
  - dbeaver
  - postgresql
  - database-tools
aliases:
  - connecting-dbeaver-to-strapi-postgresql-databases
  - CDTSPD
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Connecting DBeaver to Strapi PostgreSQL databases

DBeaver se k lokálním PostgreSQL databázím pro Strapi připojuje přes `localhost`. Kontejner `postgres_strapi` používá port `5432`, zatímco `postgres_strapi_2` má v základní konfiguraci port `5433`. Oba používají databázi `postgres_strapi`. ^[how-to/direct-dev/strapi/README.md:126-132]

## Nastavení připojení

V DBeaveru nastavte připojení podle cílového kontejneru. Uživatelské jméno, heslo i název databáze jsou pro obě uvedené konfigurace stejné. ^[how-to/direct-dev/strapi/README.md:126-132]

| Pole | `postgres_strapi` | `postgres_strapi_2` |
|---|---|---|
| Host | `localhost` | `localhost` |
| Port | `5432` | `5433` |
| User | `postgres` | `postgres` |
| Password | `direct` | `direct` |
| Database | `postgres_strapi` | `postgres_strapi` |

Porty odpovídají mapování Dockeru `5432:5432` a `5433:5432`: druhý kontejner tedy zpřístupňuje svůj databázový port `5432` na hostitelském portu `5433`. Souvisí s tématem [[PostgreSQL containers for Strapi]]. ^[how-to/direct-dev/strapi/README.md:5-24]

## Odlišný port při přenosu hesla

Postup pro přenos hashe administrátorského hesla spouští `postgres_strapi_2` s mapováním `5432:5432` po zastavení původního kontejneru. Pokud používáte tuto variantu, nastavte v DBeaveru port `5432` i pro `postgres_strapi_2`. Viz [[Resetting a Strapi administrator password by transferring its hash]]. ^[how-to/direct-dev/strapi/README.md:44-59]

## Obnovení připojení

Pro obnovení v DBeaveru použijte pravé tlačítko myši → **Invalidate/Reconnect** → **F5**. ^[how-to/direct-dev/strapi/README.md:134-134]

## Sources

- [Strapi Database - Quick Commands](how-to/direct-dev/strapi/README.md)
