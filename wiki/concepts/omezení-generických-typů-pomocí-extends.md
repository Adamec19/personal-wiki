---
title: Omezení generických typů pomocí extends
summary: Constraint pomocí extends vyžaduje určité vlastnosti generického typu, přičemž dovoluje další vlastnosti navíc.
sources:
  - how-to/typescript-cheat-sheet/02-functions-and-generics.md
kind: concept
createdAt: "2026-11-11T11:03:13.567Z"
updatedAt: "2026-11-11T11:03:13.567Z"
tags:
  - typescript
  - generics
  - type-constraints
aliases:
  - omezení-generických-typů-pomocí-extends
  - OGTPE
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Omezení generických typů pomocí extends

Omezení generického typu pomocí `extends` určuje, jaké vlastnosti musí předaný typ splňovat. Používá se tehdy, když generická funkce potřebuje určitou schopnost vstupní hodnoty, například přístup k vlastnosti `id`. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:30-42]

## Požadované vlastnosti

Typ `WithId` definuje požadovanou vlastnost `id`. Zápis `T extends WithId` umožňuje funkci `getId` tuto vlastnost použít a zároveň přijmout objekt s dalšími vlastnostmi, například `name`. Omezení neznamená, že `T` musí být přesně `WithId`; musí mít alespoň jeho vlastnosti. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:32-42]

```ts
type WithId = { id: string };

const getId = <T extends WithId>(value: T): string => value.id;

const userId = getId({ id: "user-1", name: "Ada" });
```

## Omezení klíče pomocí keyof

Zápis `K extends keyof T` omezuje parametr klíče na klíče typu `T`. Návratový typ `T[K]` pak vyjadřuje typ hodnoty vybraného klíče; souvisí s konceptem [[TypeScript Indexed Access Types]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:44-55]

```ts
const getProperty = <T, K extends keyof T>(object: T, key: K): T[K] => {
  return object[key];
};

const user = { id: "1", age: 37 };
const age = getProperty(user, "age");
```

## Kdy omezené generikum použít

Generikum má zachovávat důležitý vztah mezi typy. Pokud bude funkce pracovat vždy s jediným konkrétním typem nebo generikum pouze zhorší čitelnost, je vhodné zvážit jednodušší zápis. Další souvislosti popisuje [[Kdy generika nepoužívat]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-110]

## Sources

- how-to/typescript-cheat-sheet/02-functions-and-generics.md
