---
title: Layered dependencies and feature isolation
summary: Features may depend on shared code, while shared code should avoid feature imports and features should avoid direct dependencies on one another.
sources:
  - how-to/react-cheat-sheet/01-architecture.md
kind: concept
createdAt: "2026-11-11T10:57:43.063Z"
updatedAt: "2026-11-11T10:57:43.063Z"
tags:
  - architecture
  - dependency-management
  - modularity
aliases:
  - layered-dependencies-and-feature-isolation
  - feature isolation and Layered dependencies
  - LDAFI
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Layered dependencies and feature isolation

Vrstvené závislosti určují, které části aplikace mohou používat jiné vrstvy. Izolace features omezuje přímé vazby mezi jednotlivými funkcionalitami: feature může používat sdílenou vrstvu, ale sdílený kód nemá importovat konkrétní feature a jednotlivé features se nemají přímo propojovat. ^[how-to/react-cheat-sheet/01-architecture.md:23-31]

## Organizace vrstev

[[Feature-based code organization]] seskupuje kód podle domény nebo funkcionality. Konkrétní feature může obsahovat vlastní komponenty, hooky, modely a služby. Globálně sdílené UI, obecné utility, infrastruktura a globální služby mají samostatné umístění; vrstva `app` obsahuje routy, layouty a composition root. ^[how-to/react-cheat-sheet/01-architecture.md:3-21]

Zdroj vyjadřuje preferované vrstvení schématem `shared → features → app`. Pravidla importů dovolují feature používat shared vrstvu, zatímco opačná závislost je nežádoucí. Pokud se logika používá na více místech, do sdílené vrstvy se přesouvá její skutečně obecná část. ^[how-to/react-cheat-sheet/01-architecture.md:23-31]

## Odpovědnosti a ověřování izolace

Každý modul má mít jednu jasnou odpovědnost. [[Separation of business logic from routing|Oddělení business logiky od routování]] udržuje business logiku mimo soubory rout a layoutů. Při kontrole architektury je vhodné ověřit také to, že sdílený kód neimportuje konkrétní feature a že lze feature testovat bez spuštění celé aplikace; s tím souvisí [[Independent feature testability]]. ^[how-to/react-cheat-sheet/01-architecture.md:58-64]

## Sources

- how-to/react-cheat-sheet/01-architecture.md
