---
title: Správa Docker images
summary: Výpis lokálních images, jejich stahování z Docker Hub a odstraňování pomocí docker images, docker pull a docker rmi.
sources:
  - how-to/docker-basics/README.md
kind: concept
createdAt: "2026-11-11T10:56:04.892Z"
updatedAt: "2026-11-11T10:56:04.892Z"
tags:
  - docker
  - images
aliases:
  - správa-docker-images
  - SDI
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Správa Docker images

Základní správa Docker images zahrnuje zobrazení stažených images, stažení image z Docker Hub a odstranění image. ^[how-to/docker-basics/README.md:52-58]

## Základní příkazy

Příkaz `docker images` zobrazí stažené images. ^[how-to/docker-basics/README.md:54-55]

```bash
docker images
```

Příkaz `docker pull` stáhne image z Docker Hub. Následující příklad stáhne `postgres:15`. ^[how-to/docker-basics/README.md:57-58]

```bash
docker pull postgres:15
```

Příkaz `docker rmi` smaže zadaný image. Zástupný název `nazev-image` nahraďte názvem image, který chcete odstranit. ^[how-to/docker-basics/README.md:54-56]

```bash
docker rmi nazev-image
```

## Čištění nepotřebných images

Pro odstranění nepotřebných images slouží `docker image prune`. Tento příkaz patří mezi nástroje pro [[Čištění Docker prostředí]]. ^[how-to/docker-basics/README.md:76-80]

```bash
docker image prune
```

Širší úklid nabízí `docker system prune`, který zahrnuje kontejnery, images a cache. Zdroj jej označuje za nevratnou operaci určenou pro situace, kdy dochází místo. ^[how-to/docker-basics/README.md:79-83]

## Sources

- [Docker Basics — praktický cheat sheet](how-to/docker-basics/README.md)
