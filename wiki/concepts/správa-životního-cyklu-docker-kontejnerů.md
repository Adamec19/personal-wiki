---
title: Správa životního cyklu Docker kontejnerů
summary: Výpis běžících i zastavených kontejnerů a jejich spouštění, zastavování, restartování a odstraňování pomocí Docker CLI.
sources:
  - how-to/docker-basics/README.md
kind: concept
createdAt: "2026-11-11T10:55:55.291Z"
updatedAt: "2026-11-11T10:55:55.291Z"
tags:
  - docker
  - kontejnery
aliases:
  - správa-životního-cyklu-docker-kontejnerů
  - SŽCDK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Správa životního cyklu Docker kontejnerů

Správa životního cyklu Docker kontejnerů zahrnuje přehled běžících i zastavených kontejnerů, jejich spuštění, zastavení, restart a odstranění. ^[how-to/docker-basics/README.md:3-12]

## Přehled kontejnerů

Příkaz `docker ps` zobrazí běžící kontejnery. Přepínač `-a` rozšíří výpis také o zastavené kontejnery. ^[how-to/docker-basics/README.md:6-7]

```bash
docker ps
docker ps -a
```

## Spuštění, zastavení a restart

Existující kontejner lze spustit pomocí `docker start`, zastavit pomocí `docker stop` a restartovat pomocí `docker restart`. V příkazech nahraďte `nazev-kontejneru` názvem příslušného kontejneru. ^[how-to/docker-basics/README.md:8-10]

```bash
docker start nazev-kontejneru
docker stop nazev-kontejneru
docker restart nazev-kontejneru
```

## Odstranění kontejneru

Příkaz `docker rm` odstraní konkrétní kontejner, který musí být zastavený. Pro odstranění všech zastavených kontejnerů slouží `docker container prune`; tento hromadný úklid souvisí s tématem [[Čištění Docker prostředí]]. ^[how-to/docker-basics/README.md:11-12, how-to/docker-basics/README.md:76-80]

```bash
docker rm nazev-kontejneru
docker container prune
```

## Diagnostika problémů

Pokud kontejner neběží a potřebujete zjistit příčinu, zobrazte jeho logy příkazem `docker logs nazev-kontejneru`. Další možnosti popisuje [[Logování a diagnostika Docker kontejnerů]]. ^[how-to/docker-basics/README.md:87-92]

Pokud spuštění blokuje obsazený port, zdroj doporučuje vypsat běžící kontejnery pomocí `docker ps` a zastavit kontejner, který port blokuje. Přehled názvů a portů lze zobrazit formátovaným výpisem; souvisejícím tématem je [[Diagnostika portů Docker kontejnerů]]. ^[how-to/docker-basics/README.md:99-108]

```bash
docker ps --format "table {{.Names}}\t{{.Ports}}"
docker stop kontejner-co-blokuje
```

## Správa více služeb

Pro společné spouštění více kontejnerů slouží Docker Compose. Příkaz `docker compose up -d` spustí všechny služby na pozadí, `docker compose down` je zastaví a `docker compose restart postgres` restartuje konkrétní službu. Podrobnosti rozvádí [[Správa více služeb pomocí Docker Compose]]. ^[how-to/docker-basics/README.md:62-70]

Příkaz `docker compose down -v` navíc smaže volumes, a tím i data databáze. Při správě životního cyklu je proto nutné rozlišovat běžné zastavení služeb od odstranění jejich dat. ^[how-to/docker-basics/README.md:65-67]

## Sources

- [Docker Basics — praktický cheat sheet](how-to/docker-basics/README.md)
