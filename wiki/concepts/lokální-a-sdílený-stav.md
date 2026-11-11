---
title: Lokální a sdílený stav
summary: Stav jedné obrazovky patří do lokálního state; při sdílení mezi vzdálenými částmi aplikace je vhodné zvážit context nebo store.
sources:
  - how-to/react-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:01:06.688Z"
updatedAt: "2026-11-11T11:01:06.688Z"
tags:
  - react
  - state
  - context
aliases:
  - lokální-a-sdílený-stav
  - LASS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Lokální a sdílený stav

Při rozhodování o umístění stavu v React aplikaci je důležité určit, které části aplikace jej potřebují. Stav platný pouze pro jednu obrazovku patří do lokálního state. Pokud jej sdílí více vzdálených částí aplikace, je vhodné zvážit [[React Context and Providers|context]] nebo store. ^[how-to/react-cheat-sheet/README.md:24-26]

## Rozhodování o stavu

Ne každá hodnota potřebuje vlastní stav. Pokud lze hodnotu odvodit z props nebo existujícího state, vypočítej ji během renderu. Tuto situaci rozebírají [[Odvozené hodnoty během renderu]]. ^[how-to/react-cheat-sheet/README.md:27-27]

Synchronizace Reactu s externím systémem je důvodem pro použití `useEffect`. Jde o samostatné rozhodnutí vedle toho, zda má být stav lokální, nebo sdílený; souvisejícím tématem je [[Synchronizace s externími systémy pomocí useEffect]]. ^[how-to/react-cheat-sheet/README.md:24-28]

## Hranice a datový tok

Nejdříve navrhuj [[Hranice a datový tok v React aplikaci|hranice a datový tok]], potom abstrakce. Znovupoužitelná komponenta má být jednoduchá na použití a nemá znát business pravidla svého konzumenta. ^[how-to/react-cheat-sheet/README.md:31-33]

## Sources

- [React Cheat Sheet](how-to/react-cheat-sheet/README.md)
