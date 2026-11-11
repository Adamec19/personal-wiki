---
title: Production build validation versus development mode
summary: The standalone workflow validates built artifacts and runtime behavior without hot reload, so source changes require rebuilding and restarting the script.
sources:
  - how-to/docker-basics/local-prod-web/README.md
kind: concept
createdAt: "2026-11-11T10:56:42.233Z"
updatedAt: "2026-11-11T10:56:42.233Z"
tags:
  - testing
  - production-builds
  - development-workflow
aliases:
  - production-build-validation-versus-development-mode
  - PBVVDM
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Production build validation versus development mode

Ověření produkčního buildu kontroluje výsledek sestavení aplikace a chování výsledného serveru. Popsaný postup pro Next.js zahrnuje standalone server a statické soubory; aplikaci spouští přímo na hostitelském počítači bez vytváření a spouštění Docker image. Viz [[Local production execution without Docker]]. ^[how-to/docker-basics/local-prod-web/README.md:3-17, how-to/docker-basics/local-prod-web/README.md:112-114]

## Vývojový režim

Pro běžný vývoj s hot reloadem slouží příkaz `pnpm dev`. Produkční ověření pomocí `run-local-prod.sh` naproti tomu vyžaduje po změnách zdrojových souborů nové spuštění skriptu: změny se do již vytvořeného buildu automaticky nepromítnou. ^[how-to/docker-basics/local-prod-web/README.md:147-157]

```bash
pnpm dev
```

## Ověření produkčního buildu

Skript `run-local-prod.sh` napodobuje důležité části produkčního Dockerfile: použije vybraný env soubor, nainstaluje závislosti příkazem `pnpm install --frozen-lockfile`, provede `pnpm build`, zkopíruje `.next/static` a `public` do `.next/standalone` a spustí `.next/standalone/server.js` přes Node.js. Souvisí s [[Dependency installation with a frozen lockfile]] a [[Next.js standalone runtime packaging]]. ^[how-to/docker-basics/local-prod-web/README.md:95-108]

```bash
./run-local-prod.sh /cesta/k/projektu .env.PROD
```

První argument určuje kořen projektu, druhý název nebo cestu k env souboru. Název se hledá v kořenu projektu i v adresáři `envs/`; bez druhého argumentu se použije `envs/.env.PUBLIC_WEB_PROD`. Výběr konfigurace popisuje také [[Production environment file selection]]. ^[how-to/docker-basics/local-prod-web/README.md:58-71]

## Rozsah a omezení ověření

Postup předpokládá projekt s příkazem `pnpm build`, Next.js standalone outputem, Node.js, Corepackem a připraveným env souborem. Pro jinou strukturu buildu je nutné skript upravit. ^[how-to/docker-basics/local-prod-web/README.md:19-34]

Lokální běh nastavuje URL na `http://localhost:3000` a vypíná Redis cache. Ověřuje tedy produkční build a runtime standalone serveru s těmito lokálními úpravami konfigurace. ^[how-to/docker-basics/local-prod-web/README.md:105-114]

Původní `.env` skript dočasně zálohuje a po ukončení obnoví, včetně ukončení přes `Ctrl+C`. Pokud záloha `.env.before-local-prod` již existuje, další běh odmítne, aby ji nepřepsal. Viz [[Environment backup and restoration safeguards]]. ^[how-to/docker-basics/local-prod-web/README.md:99-110, how-to/docker-basics/local-prod-web/README.md:116-122]

## Sources

- [Lokální spuštění produkčního buildu podobně jako v Dockeru](how-to/docker-basics/local-prod-web/README.md)
