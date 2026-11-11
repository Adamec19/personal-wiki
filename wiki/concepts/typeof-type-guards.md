---
title: typeof Type Guards
summary: Checks using typeof narrow union types to primitive types such as string or number within control-flow branches.
sources:
  - how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md
kind: concept
createdAt: "2026-11-11T11:03:32.947Z"
updatedAt: "2026-11-11T11:03:32.947Z"
tags:
  - typescript
  - type-guards
aliases:
  - typeof-type-guards
  - TTG
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# typeof Type Guards

`typeof` umožňuje TypeScriptu zúžit širší typ podle podmínky na konkrétnější variantu. Jde o způsob [[TypeScript Type Narrowing|narrowingu]], při kterém kontrola typu hodnoty určuje, jaké operace jsou v dané větvi dostupné. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:3-17]

## Zúžení union typu

U parametru typu `string | number` kontrola `typeof value === "number"` zúží hodnotu ve větvi `if` na `number`, takže lze zavolat `toFixed(2)`. Protože tato větev vrací výsledek, ve zbývající části funkce je hodnota typu `string` a lze použít `toUpperCase()`. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:8-14]

```ts
const formatValue = (value: string | number): string => {
  if (typeof value === "number") {
    return value.toFixed(2);
  }

  return value.toUpperCase();
};
```

## Kontrola objektů a jejich vlastností

Při ověřování hodnoty typu `unknown` lze `typeof` kombinovat s kontrolou proti `null` a operátorem `in`. Následující [[Object type guards|objektový type guard]] ověřuje, že hodnota je objekt, není `null`, obsahuje vlastnost `message` a tato vlastnost má typ `string`. Tento postup souvisí s [[Property Validation with in and Null Checks|ověřováním vlastností pomocí `in` a kontroly `null`]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:72-85]

```ts
const hasMessage = (value: unknown): value is { message: string } => {
  return (
    typeof value === "object" &&
    value !== null &&
    "message" in value &&
    typeof value.message === "string"
  );
};
```

Návratový type predicate `value is { message: string }` sděluje TypeScriptu výsledek vlastní kontroly. Musí však odpovídat skutečnému ověření za běhu: chybný predicate pouze přesvědčí compiler a nezmění runtime data. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:48-70]

## Sources

- [Narrowing and Type Guards](how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md)
