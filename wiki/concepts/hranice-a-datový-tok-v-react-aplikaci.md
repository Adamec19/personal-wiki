---
title: Hranice a datový tok v React aplikaci
summary: Návrh aplikace má začínat vymezením hranic a datového toku, teprve poté mají vznikat abstrakce.
sources:
  - how-to/react-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:01:09.912Z"
updatedAt: "2026-11-11T11:01:09.912Z"
tags:
  - react
  - architektura
aliases:
  - hranice-a-datový-tok-v-react-aplikaci
  - HADTVRA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Hranice a datový tok v React aplikaci

Při návrhu React aplikace mají hranice a datový tok předcházet abstrakcím. Znovupoužitelná komponenta má být jednoduchá na použití a nemá znát business pravidla svého konzumenta. S tím souvisí [[Návrh znovupoužitelných komponent]] a [[Oddělení business logiky od generického UI]]. ^[how-to/react-cheat-sheet/README.md:31-33]

## Rozdělení odpovědností a umístění stavu

Pro čistě vizuální prvek je výchozím řešením komponenta. Stav platný jen pro jednu obrazovku patří do lokálního state; pokud jej sdílí více vzdálených částí aplikace, je vhodné zvážit context nebo store. Tato rozhodnutí určují [[Umístění a sdílení stavu v komponentovém stromu]]. ^[how-to/react-cheat-sheet/README.md:24-26]

## Odvozené hodnoty a synchronizace

Hodnotu odvoditelnou z props nebo state je vhodné vypočítat během renderu. `useEffect` slouží k synchronizaci Reactu s externím systémem. Při návrhu datového toku je proto užitečné rozlišovat [[Odvozené hodnoty během renderu]] a [[Synchronizace s externími systémy pomocí useEffect]]. ^[how-to/react-cheat-sheet/README.md:27-28]

## Obecné principy a projektové konvence

Obecné React principy je potřeba odlišovat od projektových konvencí a ty přizpůsobit konkrétnímu codebase. Například zápis komponent a [[custom-hooks|Custom Hooks]] jako `const` arrow functions s pojmenovanými exporty na konci souboru je konvencí uvedených ukázek. ^[how-to/react-cheat-sheet/README.md:5-5, how-to/react-cheat-sheet/README.md:35-37]

## Sources

- [React Cheat Sheet](how-to/react-cheat-sheet/README.md)
