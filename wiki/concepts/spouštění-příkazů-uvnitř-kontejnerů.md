---
title: Spouštění příkazů uvnitř kontejnerů
summary: Použití docker exec pro otevření shellu nebo jednorázové spuštění příkazu, například databázového klienta psql.
sources:
  - how-to/docker-basics/README.md
kind: concept
createdAt: "2026-11-11T10:55:53.191Z"
updatedAt: "2026-11-11T10:55:53.191Z"
tags:
  - docker
  - shell
  - databáze
aliases:
  - spouštění-příkazů-uvnitř-kontejnerů
  - SPUK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Spouštění příkazů uvnitř kontejnerů

Příkaz `docker exec` umožňuje otevřít shell nebo jednorázově spustit příkaz uvnitř kontejneru. Lze jej využít například pro přístup k PostgreSQL databázi. ^[how-to/docker-basics/README.md:26-34]

## Otevření shellu

Pro otevření shellu slouží `docker exec -it` s názvem kontejneru a požadovaným shellem. Pokud `bash` není k dispozici, lze použít `sh`. ^[how-to/docker-basics/README.md:28-30]

```bash
docker exec -it nazev-kontejneru bash
docker exec -it nazev-kontejneru sh
```

## Jednorázové spuštění příkazu

Příkaz lze spustit přímo bez otevírání shellu. Následující příklad zavolá klienta `psql` jako uživatel `postgres`, připojí se k databázi `moje_db` a provede příkaz `\dt`. ^[how-to/docker-basics/README.md:32-34]

```bash
docker exec -i nazev-kontejneru psql -U postgres -d moje_db -c "\dt"
```

Pro interaktivní přístup k PostgreSQL v kontejneru `postgres_strapi` zdroj uvádí tento příkaz. Souvisejícím tématem je [[PostgreSQL containers for Strapi]]. ^[how-to/docker-basics/README.md:94-97]

```bash
docker exec -it postgres_strapi psql -U postgres
```

## Spuštění příkazu přes Docker Compose

Při [[Správa více služeb pomocí Docker Compose|správě služeb pomocí Docker Compose]] lze použít `docker compose exec` s názvem služby. Následující příklad spustí klienta `psql` ve službě `postgres` pod uživatelem `postgres`. ^[how-to/docker-basics/README.md:62-71]

```bash
docker compose exec postgres psql -U postgres
```

## Sources

- [Docker Basics — praktický cheat sheet](how-to/docker-basics/README.md)
