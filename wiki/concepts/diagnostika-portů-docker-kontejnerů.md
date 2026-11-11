---
title: Diagnostika portů Docker kontejnerů
summary: Výpis portů pomocí docker ps pomáhá odhalit obsazené porty a určit kontejner, který je potřeba zastavit pro uvolnění portu.
sources:
  - how-to/docker-basics/README.md
kind: concept
createdAt: "2026-11-11T10:56:08.896Z"
updatedAt: "2026-11-11T10:56:08.896Z"
tags:
  - docker
  - síť
  - diagnostika
aliases:
  - diagnostika-portů-docker-kontejnerů
  - DPDK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Diagnostika portů Docker kontejnerů

Při problému se spuštěním kontejneru kvůli obsazenému portu lze pomocí `docker ps` zjistit, které kontejnery běží. Přehled názvů kontejnerů a jejich portů zobrazí příkaz s volbou `--format`. ^[how-to/docker-basics/README.md:99-108]

## Přehled portů

Následující příkaz zobrazí tabulku se sloupci pro názvy kontejnerů a porty: ^[how-to/docker-basics/README.md:105-108]

```bash
docker ps --format "table {{.Names}}\t{{.Ports}}"
```

## Řešení obsazeného portu

Pokud se kontejner nespustí kvůli obsazenému portu, zdroj uvádí tento postup: zobrazit běžící kontejnery a zastavit kontejner, který port blokuje. Zastavení kontejneru souvisí se [[Správa životního cyklu Docker kontejnerů|správou životního cyklu kontejnerů]]. ^[how-to/docker-basics/README.md:99-103]

```bash
docker ps
docker stop kontejner-co-blokuje
```

Pokud příčina nefunkčního kontejneru není zřejmá, lze zobrazit jeho logy příkazem `docker logs`. Podrobněji viz [[Logování a diagnostika Docker kontejnerů]]. ^[how-to/docker-basics/README.md:87-92]

```bash
docker logs nazev-kontejneru
```

## Sources

- [Docker Basics — praktický cheat sheet](how-to/docker-basics/README.md)
