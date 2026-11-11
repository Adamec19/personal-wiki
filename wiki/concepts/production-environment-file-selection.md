---
title: Production environment file selection
summary: The script accepts an environment filename or path, searches the project root and envs directory, and copies the selected configuration into .env.
sources:
  - how-to/docker-basics/local-prod-web/README.md
kind: concept
createdAt: "2026-11-11T10:56:28.806Z"
updatedAt: "2026-11-11T10:56:28.806Z"
tags:
  - configuration
  - environment-variables
aliases:
  - production-environment-file-selection
  - PEFS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Production environment file selection

Výběr env souboru určuje konfiguraci, kterou skript `run-local-prod.sh` použije při [[Local production execution without Docker|lokálním spuštění produkčního buildu]]. Vybraný soubor skript zkopíruje do `.env`, kde ho očekávají aplikace i build. ^[how-to/docker-basics/local-prod-web/README.md:97-105]

## Zadání env souboru

První argument skriptu určuje kořen projektu, druhý název nebo cestu k env souboru. Samotný název se hledá v kořenu projektu i v jeho adresáři `envs/`. Bez druhého argumentu se použije `envs/.env.PUBLIC_WEB_PROD`; bez prvního argumentu je kořenem projektu aktuální adresář. ^[how-to/docker-basics/local-prod-web/README.md:58-71]

```bash
# Název souboru v projektu nebo v envs/
./run-local-prod.sh /cesta/k/projektu .env.PROD

# Soubor v kořenu projektu
./run-local-prod.sh /cesta/k/projektu .env

# Explicitní relativní nebo absolutní cesta
./run-local-prod.sh /cesta/k/projektu envs/.env.PROD
./run-local-prod.sh /cesta/k/projektu /cesta/k/env/.env.PROD
```

Tyto varianty umožňují změnit projekt nebo umístění env souboru pomocí argumentů bez úpravy skriptu. ^[how-to/docker-basics/local-prod-web/README.md:75-85, how-to/docker-basics/local-prod-web/README.md:144-145]

## Produkční build s různou konfigurací

Skript vytváří produkční standalone build i při výběru souboru `.env.PUBLIC_WEB_DEV`. V uvedeném příkladu projektu `direct-public-web` lze zvolit `.env.PUBLIC_WEB_PROD` nebo `.env.PUBLIC_WEB_DEV`; v obou případech skript použije konfiguraci z `envs/`, sestaví aplikaci a spustí standalone server na `http://localhost:3000`. ^[how-to/docker-basics/local-prod-web/README.md:165-184]

Výběr env souboru je součástí [[Production build validation versus development mode|ověření produkčního buildu]]. Pro běžný vývoj s hot reloadem slouží `pnpm dev`; změny zdrojových souborů se v již vytvořeném produkčním buildu automaticky neprojeví a vyžadují nové spuštění skriptu. ^[how-to/docker-basics/local-prod-web/README.md:147-157]

## Ochrana původní konfigurace

Před sestavením skript ověří existenci vybraného env souboru. Existující lokální `.env` dočasně přesune do `.env.before-local-prod` a na jeho místo zkopíruje zvolenou konfiguraci. Po ukončení odstraní dočasný `.env` a obnoví původní soubor. ^[how-to/docker-basics/local-prod-web/README.md:97-110]

Tyto [[Environment backup and restoration safeguards|pojistky zálohování a obnovy]] zahrnují odmítnutí dalšího běhu, pokud už `.env.before-local-prod` existuje, a automatickou obnovu i při ukončení přes `Ctrl+C`. Pokud po neobvyklém ukončení záloha zůstane, je potřeba před ručním přesunem nebo odstraněním zkontrolovat `.env` i `.env.before-local-prod`. ^[how-to/docker-basics/local-prod-web/README.md:116-131]

## Sources

- [Lokální spuštění produkčního buildu podobně jako v Dockeru](how-to/docker-basics/local-prod-web/README.md)
