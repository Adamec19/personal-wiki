---
title: Logování a diagnostika Docker kontejnerů
summary: Použití docker logs pro zobrazení logů, průběžné sledování výstupu a omezení na poslední řádky při diagnostice problémů.
sources:
  - how-to/docker-basics/README.md
kind: concept
createdAt: "2026-11-11T10:55:56.411Z"
updatedAt: "2026-11-11T10:55:56.411Z"
tags:
  - docker
  - logování
  - diagnostika
aliases:
  - logování-a-diagnostika-docker-kontejnerů
  - LADDK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Logování a diagnostika Docker kontejnerů

Logy slouží k diagnostice problémů s kontejnerem, například když kontejner neběží a je potřeba zjistit příčinu. Příkaz `docker logs` zobrazí logy konkrétního kontejneru. ^[how-to/docker-basics/README.md:87-92]

## Zobrazení a sledování logů

Logy lze zobrazit jednorázově, sledovat živě pomocí přepínače `-f` nebo omezit výpis na posledních 50 řádků pomocí `--tail 50`. ^[how-to/docker-basics/README.md:16-22]

```bash
docker logs nazev-kontejneru
docker logs -f nazev-kontejneru
docker logs --tail 50 nazev-kontejneru
```

## Kontrola stavu kontejnerů

Příkaz `docker ps` vypíše běžící kontejnery; varianta `docker ps -a` zahrne také zastavené. Navazující operace popisuje [[Správa životního cyklu Docker kontejnerů]]. ^[how-to/docker-basics/README.md:3-12]

```bash
docker ps
docker ps -a
```

## Diagnostika obsazených portů

Pokud se kontejner nespustí kvůli obsazenému portu, zdroj doporučuje zkontrolovat běžící kontejnery a zastavit kontejner, který port blokuje. Přehled názvů a portů poskytne formátovaný výpis `docker ps`; souvisejícím tématem je [[Diagnostika portů Docker kontejnerů]]. ^[how-to/docker-basics/README.md:99-108]

```bash
docker ps
docker stop kontejner-co-blokuje
docker ps --format "table {{.Names}}\t{{.Ports}}"
```

## Kontrola uvnitř kontejneru

Pro kontrolu uvnitř kontejneru lze otevřít shell pomocí `docker exec -it`. Pokud není dostupný `bash`, lze použít `sh`. Příkaz `docker exec` umožňuje také jednorázově spustit například databázový příkaz; více viz [[Spouštění příkazů uvnitř kontejnerů]]. ^[how-to/docker-basics/README.md:26-34]

```bash
docker exec -it nazev-kontejneru bash
docker exec -it nazev-kontejneru sh
docker exec -i nazev-kontejneru psql -U postgres -d moje_db -c "\dt"
```

## Logy v Docker Compose

V prostředí Docker Compose lze živě sledovat logy všech služeb nebo pouze konkrétní služby, například `postgres`. Tento postup souvisí se [[Správa více služeb pomocí Docker Compose|správou více služeb pomocí Docker Compose]]. ^[how-to/docker-basics/README.md:62-69]

```bash
docker compose logs -f
docker compose logs -f postgres
```

## Sources

- [Docker Basics — praktický cheat sheet](how-to/docker-basics/README.md)
