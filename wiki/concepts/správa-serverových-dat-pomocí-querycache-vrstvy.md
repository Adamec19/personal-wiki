---
title: Správa serverových dat pomocí query/cache vrstvy
summary: Serverová data mají být spravována query/cache vrstvou místo ručně udržovaného globálního stavu.
sources:
  - how-to/react-cheat-sheet/03-state-and-effects.md
kind: concept
createdAt: "2026-11-11T10:58:18.880Z"
updatedAt: "2026-11-11T10:58:18.880Z"
tags:
  - server-state
  - caching
  - state-management
aliases:
  - správa-serverových-dat-pomocí-querycache-vrstvy
  - SSDPQV
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Správa serverových dat pomocí query/cache vrstvy

Serverová data patří do query/cache vrstvy, nikoli do ručně spravovaného globálního stavu. Při rozhodování o umístění stavu představují samostatnou kategorii vedle lokálního stavu komponent a stavu sdíleného v rámci jedné oblasti aplikace. ^[how-to/react-cheat-sheet/03-state-and-effects.md:3-10]

## Volba umístění stavu

Stav má být na nejnižším místě v komponentovém stromu, které jej potřebuje. Jedné komponentě stačí `useState`, sourozenci mohou sdílet stav ve společném rodiči a vzdálené části jedné oblasti mohou použít context nebo feature store. Pro serverová data je určená query/cache vrstva. Související princip popisuje [[Umístění a sdílení stavu v komponentovém stromu]]. ^[how-to/react-cheat-sheet/03-state-and-effects.md:3-10]

## Jediný zdroj pravdy

Při práci se stavem je potřeba zabránit více zdrojům pravdy pro stejnou hodnotu. Hodnoty odvozené z existujících props nebo stavu se nemají ukládat jako další state a synchronizovat pomocí `useEffect`; mají se přímo vypočítat. Tento princip rozvádí [[Odvozené hodnoty a jediný zdroj pravdy]]. ^[how-to/react-cheat-sheet/03-state-and-effects.md:12-21, how-to/react-cheat-sheet/03-state-and-effects.md:43-48]

## Vztah k efektům

`useEffect` slouží k synchronizaci s externím systémem, například se síťovým nebo jiným imperativním API. Toto vymezení doplňuje doporučení svěřit serverová data query/cache vrstvě. Pokud effect vytváří prostředek vyžadující úklid, cleanup musí zrušit přesně to, co effect vytvořil; viz [[Synchronizace s externími systémy pomocí useEffect]] a [[Cleanup efektů]]. ^[how-to/react-cheat-sheet/03-state-and-effects.md:10-10, how-to/react-cheat-sheet/03-state-and-effects.md:23-41]

## Sources

- [State and Effects](how-to/react-cheat-sheet/03-state-and-effects.md)
