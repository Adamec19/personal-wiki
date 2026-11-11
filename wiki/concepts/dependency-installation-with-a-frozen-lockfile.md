---
title: Dependency installation with a frozen lockfile
summary: The build workflow enables Corepack and runs pnpm install --frozen-lockfile before creating the production build with pnpm build.
sources:
  - how-to/docker-basics/local-prod-web/README.md
kind: concept
createdAt: "2026-11-11T10:56:23.181Z"
updatedAt: "2026-11-11T10:56:23.181Z"
tags:
  - pnpm
  - dependencies
  - build-process
aliases:
  - dependency-installation-with-a-frozen-lockfile
  - DIWAFL
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Dependency installation with a frozen lockfile

Instalace závislostí pomocí `pnpm install --frozen-lockfile` je součástí postupu pro [[Local production execution without Docker|lokální spuštění produkčního buildu bez Dockeru]]. Skript `run-local-prod.sh` tím napodobuje instalační krok produkčního Dockerfile před vytvořením Next.js standalone buildu. ^[how-to/docker-basics/local-prod-web/README.md:7-17, how-to/docker-basics/local-prod-web/README.md:103-108]

## Zařazení do postupu

Skript nejprve přejde do kořene projektu, ověří vybraný env soubor a připraví jej jako `.env`. Poté zapne Corepack a nainstaluje závislosti následujícím příkazem. ^[how-to/docker-basics/local-prod-web/README.md:97-104]

```bash
pnpm install --frozen-lockfile
```

Po instalaci následuje `pnpm build`, zkopírování `.next/static` a `public` do `.next/standalone` a spuštění výsledného serveru přes Node.js. Instalace tak předchází ověření produkčního buildu včetně standalone serveru a statických souborů. ^[how-to/docker-basics/local-prod-web/README.md:105-114]

## Předpoklady a přenositelnost

Uvedený postup předpokládá projekt s `package.json`, příkazem `pnpm build` a Next.js standalone outputem, dostupný Node.js a Corepack i přístup k repozitáři a jeho závislostem. Při přenosu skriptu do jiného projektu je potřeba ověřit zejména použití `pnpm` a příkazu `pnpm build`. ^[how-to/docker-basics/local-prod-web/README.md:19-24, how-to/docker-basics/local-prod-web/README.md:133-139]

## Sources

- [Lokální spuštění produkčního buildu podobně jako v Dockeru](how-to/docker-basics/local-prod-web/README.md)
