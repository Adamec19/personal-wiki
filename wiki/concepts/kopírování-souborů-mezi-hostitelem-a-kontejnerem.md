---
title: Kopírování souborů mezi hostitelem a kontejnerem
summary: Příkaz docker cp umožňuje přenášet soubory oběma směry mezi lokálním počítačem a kontejnerem.
sources:
  - how-to/docker-basics/README.md
kind: concept
createdAt: "2026-11-11T10:56:00.470Z"
updatedAt: "2026-11-11T10:56:00.470Z"
tags:
  - docker
  - soubory
aliases:
  - kopírování-souborů-mezi-hostitelem-a-kontejnerem
  - KSMHAK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Kopírování souborů mezi hostitelem a kontejnerem

Příkaz `docker cp` slouží ke kopírování souborů oběma směry mezi hostitelským počítačem a kontejnerem. Cesta uvnitř kontejneru se zapisuje ve tvaru `nazev-kontejneru:/cesta/soubor`; pořadí argumentů určuje zdroj a cíl kopírování. ^[how-to/docker-basics/README.md:40-48]

## Z hostitele do kontejneru

Pro zkopírování souboru do kontejneru uveďte nejprve lokální cestu a potom název kontejneru s cílovou cestou. Následující příklad kopíruje SQL soubor do `/tmp/soubor.sql` v kontejneru. ^[how-to/docker-basics/README.md:43-44]

```bash
docker cp /lokalni/cesta/soubor.sql nazev-kontejneru:/tmp/soubor.sql
```

## Z kontejneru na hostitele

Pro kopírování opačným směrem uveďte nejprve název kontejneru se zdrojovou cestou a potom cílovou cestu na hostiteli. ^[how-to/docker-basics/README.md:46-47]

```bash
docker cp nazev-kontejneru:/tmp/soubor.sql /lokalni/cesta/soubor.sql
```

## Související operace

Ke spuštění příkazu uvnitř kontejneru slouží `docker exec`, popsaný v tématu [[Spouštění příkazů uvnitř kontejnerů]]. Zdroj uvádí jak otevření shellu, tak jednorázové spuštění databázového příkazu pomocí `psql`. ^[how-to/docker-basics/README.md:26-34]

## Sources

- [Docker Basics — praktický cheat sheet](how-to/docker-basics/README.md)
