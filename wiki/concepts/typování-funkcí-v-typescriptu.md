---
title: Typování funkcí v TypeScriptu
summary: Veřejné helpery mají mít explicitně typované vstupy i návratovou hodnotu; lokální funkce mohou využít inferenci návratového typu.
sources:
  - how-to/typescript-cheat-sheet/02-functions-and-generics.md
kind: concept
createdAt: "2026-11-11T11:03:12.913Z"
updatedAt: "2026-11-11T11:03:12.913Z"
tags:
  - typescript
  - functions
aliases:
  - typování-funkcí-v-typescriptu
  - TFVT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Typování funkcí v TypeScriptu

Typování funkcí určuje typy vstupních parametrů a návratové hodnoty. U veřejných helperů je vhodné explicitně typovat obojí; u lokálních funkcí může návratový typ bezpečně odvodit [[Type Inference and Explicit Annotations|typová inference]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:3-15]

## Funkční typ jako kontrakt

Typ funkce lze pojmenovat pomocí typového aliasu a přiřadit jej implementaci. V příkladu `FormatPrice` přijímá `number` a `string` a vrací `string`; parametry implementace přebírají typy z tohoto kontraktu. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:5-15]

```ts
type FormatPrice = (value: number, currency: string) => string;

const formatPrice: FormatPrice = (value, currency) => {
  return `${value.toFixed(2)} ${currency}`;
};

export { formatPrice };
```

## Generické funkce

Generický parametr zachovává vztah mezi vstupním a výstupním typem. Funkce `first` pracuje s polem prvků typu `T` a vrací `T | undefined`. Zápis `<T,>` s čárkou je praktický v souborech `.tsx`, kde brání interpretaci generika jako JSX tagu; podrobněji viz [[Syntaxe generik v TSX]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:17-28]

```ts
const first = <T,>(items: T[]): T | undefined => items[0];

const firstNumber = first([1, 2, 3]);
const firstName = first(["Ada", "Grace"]);
```

### Omezení pomocí `extends`

Pokud funkce vyžaduje určitou vlastnost vstupu, lze generický parametr omezit pomocí `extends`. Omezení `T extends WithId` znamená, že `T` musí mít alespoň vlastnosti typu `WithId`, nikoli že se mu musí přesně rovnat. Viz [[Omezení generických typů pomocí extends]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:30-42]

```ts
type WithId = { id: string };

const getId = <T extends WithId>(value: T): string => value.id;

const userId = getId({ id: "user-1", name: "Ada" });
```

### Vztah klíče a návratové hodnoty

Kombinace `K extends keyof T` a návratového typu `T[K]` propojuje povolený klíč s typem vrácené hodnoty. `keyof T` představuje union klíčů typu `T`; `T[K]` vybírá typ hodnoty příslušného klíče, jak popisuje [[TypeScript Indexed Access Types]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:44-55]

```ts
const getProperty = <T, K extends keyof T>(object: T, key: K): T[K] => {
  return object[key];
};

const user = { id: "1", age: 37 };
const age = getProperty(user, "age");
```

## [[kdy-generika-nepoužívat|Kdy generika nepoužívat]]

Generikum má zachovávat důležitý vztah mezi typy. Není vhodné, pokud funkce vždy pracuje s jediným konkrétním typem, zhoršuje čitelnost, zastírá business varianty vhodné pro explicitní union nebo je méně srozumitelné než `unknown` s následným narrowing. Viz [[Kdy generika nepoužívat]] a [[TypeScript Type Narrowing]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-110]

## Sources

- [Functions and Generics](how-to/typescript-cheat-sheet/02-functions-and-generics.md)
