---
title: Kdy generika nepoužívat
summary: Generika mají zachovávat důležité vztahy mezi typy; konkrétní typ, explicitní union nebo unknown s narrowing mohou být srozumitelnější.
sources:
  - how-to/typescript-cheat-sheet/02-functions-and-generics.md
kind: concept
createdAt: "2026-11-11T11:03:29.007Z"
updatedAt: "2026-11-11T11:03:29.007Z"
tags:
  - typescript
  - generics
  - type-design
aliases:
  - kdy-generika-nepoužívat
  - KGN
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Kdy generika nepoužívat

Generika mají zachovat důležitý vztah mezi typy, například mezi vstupem a výstupem funkce. Pokud takový vztah nevyjadřují a pouze vytvářejí dojem flexibility, není jejich použití přínosné. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:17-26, how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-110]

## Kdy zvolit jednodušší typování

Pokud bude funkce nebo komponenta vždy pracovat s jediným konkrétním typem, použij tento typ přímo. Generikum vynech také tehdy, když pouze zhoršuje čitelnost. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-106]

Business varianty, které mají být vyjádřeny explicitním unionem, nemodeluj generikem. Souvisejícím konceptem jsou [[Union and Literal Types]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-107]

Pokud je srozumitelnější použít `unknown` a následně typ zúžit, dej tomuto postupu přednost před generikem. Viz [[Unknown Versus Any]] a [[TypeScript Type Narrowing]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-108]

## Kdy má generikum smysl

U funkce vracející první prvek pole generikum zachovává vztah mezi typem prvků a návratovou hodnotou: `first<T>(items: T[]): T | undefined`. Takové použití předává důležitou typovou informaci; další příklady popisuje [[Generic Functions and Components]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:17-26]

Ani výchozí hodnota generického parametru by neměla zamaskovat chybějící typovou informaci. Jejím účelem je pohodlnější použití. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:57-71]

## Sources

- [Functions and Generics](how-to/typescript-cheat-sheet/02-functions-and-generics.md)
