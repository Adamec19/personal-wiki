---
title: Čištění Docker prostředí
summary: Příkazy prune slouží k odstraňování zastavených kontejnerů, nepotřebných images a dalších prostředků pro uvolnění místa.
sources:
  - how-to/docker-basics/README.md
kind: concept
createdAt: "2026-11-11T10:56:09.922Z"
updatedAt: "2026-11-11T10:56:09.922Z"
tags:
  - docker
  - údržba
  - úložiště
aliases:
  - čištění-docker-prostředí
  - ČDP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Čištění Docker prostředí

Čištění Docker prostředí zahrnuje odstranění zastavených kontejnerů, nepotřebných images a dalších prostředků. Zdroj rozlišuje cílené čištění příkazy `docker container prune` a `docker image prune` od širšího čištění pomocí `docker system prune`. ^[how-to/docker-basics/README.md:76-82]

## Základní příkazy

Příkaz `docker container prune` smaže všechny zastavené kontejnery. Souvisí tak se [[Správa životního cyklu Docker kontejnerů|správou životního cyklu kontejnerů]]. ^[how-to/docker-basics/README.md:78-79]

```bash
docker container prune
```

Příkaz `docker image prune` odstraní nepotřebné images; další operace s nimi popisuje [[Správa Docker images]]. ^[how-to/docker-basics/README.md:52-58, how-to/docker-basics/README.md:80-80]

```bash
docker image prune
```

Příkaz `docker system prune` slouží k širšímu čištění kontejnerů, images a cache. Zdroj jej označuje za nevratnou operaci a doporučuje jej použít pouze tehdy, když dochází místo. ^[how-to/docker-basics/README.md:81-83]

```bash
docker system prune
```

## Odstranění volumes v Docker Compose

Při [[Správa více služeb pomocí Docker Compose|správě služeb pomocí Docker Compose]] příkaz `docker compose down -v` zastaví služby a smaže volumes. Tím smaže také data databáze uložená v těchto volumes. ^[how-to/docker-basics/README.md:62-67]

```bash
docker compose down -v
```

## Sources

- [Docker Basics — praktický cheat sheet](how-to/docker-basics/README.md)
