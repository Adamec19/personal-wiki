---
title: Unknown Types, Narrowing, and Type Guards
summary: Treat external values as unknown instead of any, then narrow or validate them before use.
sources:
  - how-to/typescript-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:06:05.350Z"
updatedAt: "2026-11-11T11:06:05.350Z"
tags:
  - typescript
  - type-safety
  - narrowing
aliases:
  - unknown-types-narrowing-and-type-guards
  - Type Guards and Unknown Types, Narrowing,
  - UTNATG
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Unknown Types, Narrowing, and Type Guards

Typ `unknown` je doporučený výchozí bod pro hodnoty přicházející zvenčí. Místo použití `any` jako zkratky je vhodné začít s `unknown` a data následně zúžit nebo validovat. ^[how-to/typescript-cheat-sheet/README.md:26-27, how-to/typescript-cheat-sheet/README.md:30-37]

## Zužování typů a type guards

Zužování typů a type guards jsou tématem při práci s union typy nebo daty, která mohou mít více variant. Pokud hodnota představuje jednu z několika variant, průvodce doporučuje použít union a diskriminant; souvisejícím konceptem jsou [[Discriminated Unions]]. ^[how-to/typescript-cheat-sheet/README.md:13-13, how-to/typescript-cheat-sheet/README.md:32-33]

## Externí data a runtime validace

TypeScript kontroluje kód při buildu nebo v editoru, ale automaticky nevaliduje data přicházející za běhu z API, formuláře nebo localStorage. Práce s `unknown` proto souvisí s rozlišením mezi [[Compile-time typy versus runtime validace|compile-time typy a runtime validací]]. Pokud je potřeba ověřit data za běhu, průvodce doporučuje runtime schema nebo parser. ^[how-to/typescript-cheat-sheet/README.md:5-5, how-to/typescript-cheat-sheet/README.md:32-37]

## Praktický postup

Pro externí hodnotu začněte typem `unknown` a před dalším použitím ji zužte nebo validujte. U více variant zvažte union s diskriminantem. Dodaný zdroj tato doporučení shrnuje, ale konkrétní implementace type guards neuvádí; další související témata jsou [[Unknown Versus Any]] a [[TypeScript Type Narrowing]]. ^[how-to/typescript-cheat-sheet/README.md:13-13, how-to/typescript-cheat-sheet/README.md:26-37]

## Sources

- [TypeScript Cheat Sheet](how-to/typescript-cheat-sheet/README.md)
