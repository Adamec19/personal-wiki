---
title: TypeScript Type Narrowing
summary: Narrowing refines a broad type into a more specific variant based on conditions, enabling access to variant-specific properties.
sources:
  - how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md
kind: concept
createdAt: "2026-11-11T11:03:38.762Z"
updatedAt: "2026-11-11T11:03:38.762Z"
tags:
  - typescript
  - type-system
aliases:
  - typescript-type-narrowing
  - TTN
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Type Narrowing

Narrowing je proces, při kterém TypeScript podle podmínky zúží širší typ na konkrétnější variantu. Umožňuje tak přistupovat k vlastnostem odpovídajícím ověřenému typu. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:3-14]

## Kontrola pomocí `typeof`

Operátor `typeof` umožňuje rozlišit například `string` a `number`. V následujícím příkladu TypeScript ve větvi podmínky dovolí volání `toFixed`, zatímco po jejím opuštění pomocí `return` pracuje s hodnotou jako s řetězcem. Viz [[typeof Type Guards]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:5-17]

```ts
const formatValue = (value: string | number): string => {
  if (typeof value === "number") {
    return value.toFixed(2);
  }

  return value.toUpperCase();
};
```

## Diskriminované uniony

Varianty unionu lze rozlišovat společnou vlastností, například `type`, `kind` nebo `status`. Při větvení podle tohoto diskriminantu TypeScript rozpozná konkrétní variantu a dovolí přístup pouze k jejím vlastnostem. Viz [[Discriminated Unions]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:19-44]

```ts
type RequestState =
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; error: Error };

const renderState = (state: RequestState): string => {
  switch (state.status) {
    case "loading":
      return "Načítám";
    case "success":
      return state.data.join(", ");
    case "error":
      return state.error.message;
  }
};
```

## Vlastní type guardy

Vlastní kontrolní funkce může vracet type predicate ve tvaru `value is SomeType`. TypeScript podle výsledku této funkce zúží typ v navazující podmínce. Predicate musí odpovídat skutečné kontrole: chybná deklarace pouze přesvědčí compiler, ale nezmění runtime data. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:46-70]

```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };

const isFish = (animal: Fish | Bird): animal is Fish => {
  return "swim" in animal;
};

const move = (animal: Fish | Bird): void => {
  if (isFish(animal)) {
    animal.swim();
    return;
  }

  animal.fly();
};
```

## Ověření vlastností objektu

U hodnoty typu `unknown` lze kombinovat kontrolu `typeof`, vyloučení `null`, operátor `in` a kontrolu typu konkrétní vlastnosti. Následující guard ověřuje, že hodnota je nenulový objekt s vlastností `message` typu `string`. Viz [[Property Validation with in and Null Checks]] a [[Object type guards]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:72-85]

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

## Kontrola úplnosti pomocí `never`

Funkce přijímající `never` umožňuje kontrolovat, zda `switch` pokrývá všechny varianty unionu. Po přidání nové varianty upozorní volání `assertNever(state)` na místo, které je potřeba doplnit. Viz [[Exhaustiveness Checking with never]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:87-106]

```ts
const assertNever = (value: never): never => {
  throw new Error(`Unhandled state: ${String(value)}`);
};

const getLabel = (state: RequestState): string => {
  switch (state.status) {
    case "loading":
      return "Načítám";
    case "success":
      return "Hotovo";
    case "error":
      return "Chyba";
    default:
      return assertNever(state);
  }
};
```

## Sources

- [Narrowing and Type Guards](how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md)
