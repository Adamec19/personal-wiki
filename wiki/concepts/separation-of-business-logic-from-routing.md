---
title: Separation of business logic from routing
summary: Keep business logic outside route and layout files, with each module having one clear responsibility.
sources:
  - how-to/react-cheat-sheet/01-architecture.md
kind: concept
createdAt: "2026-11-11T10:57:49.530Z"
updatedAt: "2026-11-11T10:57:49.530Z"
tags:
  - separation-of-concerns
  - routing
  - maintainability
aliases:
  - separation-of-business-logic-from-routing
  - SOBLFR
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Separation of business logic from routing

Oddělení business logiky od routování znamená držet doménovou logiku mimo soubory routes a layoutů. Každý modul má mít jednu jasnou odpovědnost; vrstva `app/` slouží pro routes, layouty a skládání aplikace. ^[how-to/react-cheat-sheet/01-architecture.md:9-19, how-to/react-cheat-sheet/01-architecture.md:58-64]

## Umístění logiky a závislosti

V rámci [[Feature-based code organization]] se kód seskupuje podle domény nebo feature. Konkrétní feature může obsahovat vlastní komponenty, hooky, modely a služby. Skutečně obecná logika používaná na více místech patří do sdílené vrstvy. ^[how-to/react-cheat-sheet/01-architecture.md:3-21, how-to/react-cheat-sheet/01-architecture.md:31-31]

Směr závislostí odpovídá principu [[Layered dependencies and feature isolation]]: feature může používat sdílenou vrstvu, ale sdílený kód nemá importovat konkrétní feature a jednotlivé features se nemají přímo propojovat. ^[how-to/react-cheat-sheet/01-architecture.md:23-31]

## Odpovědnost stránky a komponent

Oddělení business logiky nevylučuje přípravu dat ve stránce. Serverová komponenta může načíst data a složit stránku, zatímco klientská komponenta vlastní interaktivitu, události a browser API. V rámci [[Server and client component boundaries]] má hranice klientské části zůstat co nejhlouběji; `use client` se nemá automaticky přidávat do celé feature. ^[how-to/react-cheat-sheet/01-architecture.md:33-55]

## Kontrola návrhu

Při kontrole návrhu je vhodné ověřit jasnou odpovědnost každého modulu, umístění business logiky mimo routes a layouty, správný směr závislostí a omezení klientské hranice na potřebnou interaktivitu. Dalším kritériem je [[Independent feature testability|možnost testovat feature samostatně]] bez spuštění celé aplikace. ^[how-to/react-cheat-sheet/01-architecture.md:58-64]

## Sources

- [Architecture](how-to/react-cheat-sheet/01-architecture.md)
