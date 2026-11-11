---
title: Zachování vztahu mezi typy pomocí generik
summary: Generický parametr zachovává vztah mezi vstupním a výstupním typem, například při získání prvního prvku pole.
sources:
  - how-to/typescript-cheat-sheet/02-functions-and-generics.md
kind: concept
createdAt: "2026-11-11T11:03:16.151Z"
updatedAt: "2026-11-11T11:03:16.151Z"
tags:
  - typescript
  - generics
aliases:
  - zachování-vztahu-mezi-typy-pomocí-generik
  - ZVMTPG
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Zachování vztahu mezi typy pomocí generik

Generika zachovávají vztah mezi typy vstupů a výstupů. Typový parametr umožňuje vyjádřit, že návratový typ závisí na typu předaných dat, místo aby se tato souvislost ztratila. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:17-26]

## Vztah mezi vstupem a výstupem

Funkce `first` používá parametr `T` pro typ prvků pole i vráceného prvku. Při předání číselného pole je výsledkem `number | undefined`, při předání pole řetězců `string | undefined`. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:19-26]

```ts
const first = <T,>(items: T[]): T | undefined => items[0];

const firstNumber = first([1, 2, 3]);
const firstName = first(["Ada", "Grace"]);
```

Zápis `<T,>` s čárkou je vhodný v souborech `.tsx`, protože zabraňuje interpretaci generika jako JSX tagu. Podrobněji viz [[Syntaxe generik v TSX]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:28-28]

## Omezení typového parametru

Pokud funkce potřebuje určitou vlastnost, lze typový parametr omezit pomocí `extends`. Omezení `T extends WithId` vyžaduje alespoň vlastnosti typu `WithId`; nevylučuje další vlastnosti předaného objektu. Viz [[Omezení generických typů pomocí extends]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:30-42]

```ts
type WithId = { id: string };

const getId = <T extends WithId>(value: T): string => value.id;

const userId = getId({ id: "user-1", name: "Ada" });
```

## Vztah mezi objektem, klíčem a hodnotou

Pomocí `K extends keyof T` lze omezit klíč na klíče konkrétního objektu. Návratový typ `T[K]` potom odpovídá hodnotě vybraného klíče: v uvedeném příkladu má `age` typ `number`. Souvisejícím konceptem je [[TypeScript Indexed Access Types]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:44-55]

```ts
const getProperty = <T, K extends keyof T>(object: T, key: K): T[K] => {
  return object[key];
};

const user = { id: "1", age: 37 };
const age = getProperty(user, "age");
```

## Vztahy v komponentách

U [[Generické komponenty|generických komponent]] může stejný parametr `T` propojit typ položek s argumenty callbacků. Například `SelectProps<T>` zajišťuje, že `options`, `getValue`, `getLabel` a `onChange` pracují se stejným typem položky. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:73-83]

```ts
type SelectProps<T> = {
  options: T[];
  getValue: (option: T) => string;
  getLabel: (option: T) => string;
  onChange: (option: T) => void;
};
```

## [[kdy-generika-nepoužívat|Kdy generika nepoužívat]]

Generikum má zachovat důležitý vztah mezi typy. Není vhodné, pokud bude typ vždy jediný konkrétní typ, zhoršuje čitelnost, nahrazuje explicitní union business variant nebo by bylo srozumitelnější použít `unknown` a následné zúžení typu. Viz [[Kdy generika nepoužívat]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-110]

Výchozí typový parametr může použití usnadnit, ale nemá zakrývat chybějící typovou informaci. Zdroj uvádí například `ApiResult<TData = unknown>`. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:57-71]

## Sources

- [Functions and Generics](how-to/typescript-cheat-sheet/02-functions-and-generics.md)
