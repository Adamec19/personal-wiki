---
title: Výchozí hodnoty generických parametrů
summary: Generický parametr může mít výchozí typ, například unknown, který usnadňuje použití, ale nemá zakrývat chybějící typovou informaci.
sources:
  - how-to/typescript-cheat-sheet/02-functions-and-generics.md
kind: concept
createdAt: "2026-11-11T11:03:25.327Z"
updatedAt: "2026-11-11T11:03:25.327Z"
tags:
  - typescript
  - generics
  - type-defaults
aliases:
  - výchozí-hodnoty-generických-parametrů
  - VHGP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Výchozí hodnoty generických parametrů

Výchozí hodnota generického parametru určuje typ použitý při vynechání daného typového argumentu. V následujícím příkladu má parametr `TData` výchozí typ `unknown`; konkrétní typ dat lze zadat explicitně. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:57-69]

## Příklad použití

```ts
type ApiResult<TData = unknown> = {
  data: TData;
  error: Error | null;
};

const result: ApiResult<{ id: string }> = {
  data: { id: "1" },
  error: null
};
```

Zápis `ApiResult` používá pro `data` typ `unknown`. Zápis `ApiResult<{ id: string }>` výchozí typ nahrazuje a určuje, že `data` obsahuje objekt s vlastností `id` typu `string`. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:60-69]

## Kdy výchozí typ použít

Výchozí typ usnadňuje používání generického typu, ale nesmí zakrýt chybějící typovou informaci. Generický parametr má zachovávat důležitý vztah mezi typy; pokud bude typ vždy stejný nebo generikum pouze zhorší čitelnost, je vhodné zvážit jeho vynechání. Související témata jsou [[Kdy generika nepoužívat]] a [[Unknown Versus Any]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:71-71, how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-110]

## Sources

- [Functions and Generics](how-to/typescript-cheat-sheet/02-functions-and-generics.md)
