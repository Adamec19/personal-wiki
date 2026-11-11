---
title: TypeScript infer Keyword
summary: Capture part of a matched type inside a conditional type, such as the value wrapped by a Promise.
sources:
  - how-to/typescript-cheat-sheet/05-advanced-types.md
kind: concept
createdAt: "2026-11-11T11:04:25.195Z"
updatedAt: "2026-11-11T11:04:25.195Z"
tags:
  - typescript
  - type-inference
  - conditional-types
aliases:
  - typescript-infer-keyword
  - TIK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript infer Keyword

Klíčové slovo `infer` pojmenuje část typu uvnitř [[TypeScript Conditional Types|conditional type]]. Umožňuje tuto část použít ve výsledku podmíněného typu. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:46-54]

## Příklad: získání typu z Promise

Typ `UnwrapPromise<T>` ověří, zda `T` odpovídá `Promise<infer TValue>`. Pokud ano, výsledkem je odvozený typ `TValue`; jinak zůstává původní typ `T`. V uvedeném příkladu tak `User` odpovídá typu `{ id: string }`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:50-54]

```ts
type UnwrapPromise<T> = T extends Promise<infer TValue> ? TValue : T;

type User = UnwrapPromise<Promise<{ id: string }>>;
```

## Distribuce přes union

Pokud conditional type začíná přímo typovým parametrem, může se vyhodnocení distribuovat přes jednotlivé členy unionu. Toto chování popisují [[Distributive Conditional Types]]; je užitečné, ale u složitých typů může zhoršovat čitelnost. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:56-56]

## Sources

- [Advanced Types](how-to/typescript-cheat-sheet/05-advanced-types.md)
