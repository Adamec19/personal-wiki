---
title: Správa více služeb pomocí Docker Compose
summary: Docker Compose umožňuje společné spouštění a zastavování služeb, sledování logů a práci s jednotlivými službami; down -v odstraňuje také volumes a může smazat databázová data.
sources:
  - how-to/docker-basics/README.md
kind: concept
createdAt: "2026-11-11T10:56:07.015Z"
updatedAt: "2026-11-11T10:56:07.015Z"
tags:
  - docker
  - docker-compose
  - volumes
aliases:
  - správa-více-služeb-pomocí-docker-compose
  - SVSPDC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Správa více služeb pomocí Docker Compose

Docker Compose umožňuje spouštět více kontejnerů najednou a spravovat služby společně nebo jednotlivě. Základní příkazy zahrnují spuštění a zastavení služeb, sledování logů, restart konkrétní služby a spuštění příkazu uvnitř ní. ^[how-to/docker-basics/README.md:62-72]

## Spuštění a zastavení služeb

Příkaz `docker compose up -d` spustí všechny služby na pozadí. Příkaz `docker compose down` je zastaví. ^[how-to/docker-basics/README.md:65-66]

```bash
docker compose up -d
docker compose down
```

Varianta `docker compose down -v` navíc smaže volumes. **Tím se smažou také data databáze uložená v těchto volumes.** ^[how-to/docker-basics/README.md:67-67]

```bash
docker compose down -v
```

## Sledování logů

Příkaz `docker compose logs -f` sleduje logy všech služeb. Přidáním názvu služby lze výpis omezit například na `postgres`. Související postupy popisuje [[Logování a diagnostika Docker kontejnerů]]. ^[how-to/docker-basics/README.md:68-69]

```bash
docker compose logs -f
docker compose logs -f postgres
```

## Operace nad konkrétní službou

Jednotlivou službu lze restartovat pomocí `docker compose restart`. Příkaz `docker compose exec` umožňuje spustit příkaz uvnitř služby; v příkladu otevírá klienta `psql` pod uživatelem `postgres`. Další možnosti nabízí [[Spouštění příkazů uvnitř kontejnerů]]. ^[how-to/docker-basics/README.md:70-71]

```bash
docker compose restart postgres
docker compose exec postgres psql -U postgres
```

## Sources

- [Docker Basics — praktický cheat sheet](how-to/docker-basics/README.md)
