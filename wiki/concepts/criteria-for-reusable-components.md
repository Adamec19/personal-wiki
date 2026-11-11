---
title: Criteria for Reusable Components
summary: Extract reusable components around stable purposes, clear contracts, and multiple real uses; consider composition before abstracting small JSX similarities solely for DRY.
sources:
  - how-to/react-cheat-sheet/02-components.md
kind: concept
createdAt: "2026-11-11T10:58:09.294Z"
updatedAt: "2026-11-11T10:58:09.294Z"
tags:
  - components
  - abstraction
  - reusability
aliases:
  - criteria-for-reusable-components
  - CFRC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Criteria for Reusable Components

Znovupoužitelná komponenta je vhodná tehdy, když má stabilní účel, jasný kontrakt a více reálných použití. Samotná podobnost kódu není dostatečným důvodem k vytvoření abstrakce: pokud se dvě použití liší pouze dvěma řádky JSX, je vhodné nejprve zvážit [[Composition Through Children|composition]]. ^[how-to/react-cheat-sheet/02-components.md:64-66]

## Jasný veřejný kontrakt

Props tvoří veřejné API komponenty. Kontrakt by měl upřednostňovat malé, explicitní props před univerzálním objektem s mnoha volitelnými hodnotami. Tento princip rozvíjí [[Component Props as a Public Contract]]. ^[how-to/react-cheat-sheet/02-components.md:3-5]

## Oddělení obsahu a rozhodování

Vizuální wrapper nemá znát konkrétní obsah; může jej přijímat přes `children`. Tím lze sdílet obal a konkrétní obsah skládat samostatně. ^[how-to/react-cheat-sheet/02-components.md:41-55]

Obecný Button nebo Input nemá obsahovat business rozhodnutí. Callback má zůstat u komponenty, která vlastní rozhodnutí, a jeho název má vyjadřovat akci, například `onSubmit`, `onRemove` nebo `onChange`. Souvisejí s tím [[Event Callbacks and Decision Ownership]] a [[Oddělení business logiky od generického UI]]. ^[how-to/react-cheat-sheet/02-components.md:57-61]

## Vlastnictví stavu

Pokud rodič potřebuje hodnotu znát nebo řídit, je vhodná controlled komponenta. Kopírování props do lokálního stavu pouze pro pohodlnější práci vytváří synchronizační problém. Viz [[Controlled Components and State Ownership]]. ^[how-to/react-cheat-sheet/02-components.md:25-39]

## Sources

- [Components](how-to/react-cheat-sheet/02-components.md)
