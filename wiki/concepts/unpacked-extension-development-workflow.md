---
title: Unpacked Extension Development Workflow
summary: Developers load a local extension through Developer mode at chrome://extensions/ and reload it after editing its files.
sources:
  - how-to/chrome-extension/README.md
kind: concept
createdAt: "2026-11-11T10:54:40.813Z"
updatedAt: "2026-11-11T10:54:40.813Z"
tags:
  - chrome-extensions
  - development-workflow
aliases:
  - unpacked-extension-development-workflow
  - UEDW
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Unpacked Extension Development Workflow

Vývoj rozbaleného rozšíření umožňuje načíst lokální složku rozšíření do Chrome pomocí **Load unpacked**. Zdrojový příklad používá složku `bypass-sharepoint/`, která obsahuje konfiguraci `manifest.json`, síťová pravidla `rules.json` a metadata generovaná prohlížečem. ^[how-to/chrome-extension/README.md:9-16, how-to/chrome-extension/README.md:100-106]

## Načtení do Chrome

1. Otevři `chrome://extensions/`.
2. Zapni **Developer mode** vpravo nahoře.
3. Klikni na **Load unpacked**.
4. Vyber složku rozšíření, například `bypass-sharepoint`.

Po výběru složky se rozšíření nainstaluje a bude aktivní. ^[how-to/chrome-extension/README.md:100-106]

## Úpravy a opětovné načtení

V příkladu založeném na [[Chrome Extensions with Manifest V3]] se cílová adresa přesměrování mění v `rules.json` pomocí `redirect.url`. Výběr zdrojových URL určuje `condition.regexFilter`; při změně domény je potřeba upravit také `host_permissions` v `manifest.json`. Tyto části souvisejí s [[Declarative URL Redirection]] a [[Extension Host Permissions]]. ^[how-to/chrome-extension/README.md:112-138]

Po uložení změn otevři `chrome://extensions/` a u příslušného rozšíření klikni na **Reload**. Tento krok je součástí pracovního cyklu úpravy souborů a opětovného načtení rozšíření. ^[how-to/chrome-extension/README.md:140-142]

## Ověření chování

Funkčnost ověř návštěvou URL, na kterou se pravidlo vztahuje. V uvedeném příkladu má návštěva `https://directpojistovnaas.sharepoint.com/sites/Directintranet/` vyvolat přesměrování na `https://google.com`. ^[how-to/chrome-extension/README.md:82-84, how-to/chrome-extension/README.md:108]

## Sources

- [how-to/chrome-extension/README.md](how-to/chrome-extension/README.md)
