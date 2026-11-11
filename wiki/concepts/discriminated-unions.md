---
title: Discriminated Unions
summary: A shared property with distinct literal values lets TypeScript identify each union variant and its available properties.
sources:
  - how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md
  - how-to/typescript-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:03:47.223Z"
updatedAt: "2026-11-11T11:03:47.223Z"
tags:
  - typescript
  - union-types
aliases:
  - discriminated-unions
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Discriminated Unions

Discriminated union je sjednocení typů, jejichž varianty mají společnou vlastnost s rozlišující hodnotou — diskriminant. Typicky se používá `type` nebo `kind`; v následující ukázce je to `status`. Kontrola této vlastnosti umožňuje TypeScriptu zúžit union na konkrétní variantu a zpřístupnit její vlastnosti. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:19-44]

## Modelování variant

Stav požadavku lze popsat třemi variantami: načítání, úspěch s daty a chyba. Každá varianta má vlastní hodnotu `status` a obsahuje odpovídající údaje. Tento vzor se hodí pro [[Správa stavu API požadavků|správu stavu API požadavků]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:24-28]

```ts
type LoadingState = { status: "loading" };
type SuccessState = { status: "success"; data: string[] };
type ErrorState = { status: "error"; error: Error };

type RequestState = LoadingState | SuccessState | ErrorState;
```

## Zúžení podle diskriminantu

Při větvení pomocí `switch` nad `state.status` zná TypeScript v každé větvi přesnou variantu. Ve větvi `"success"` dovolí přístup k `data`, ve větvi `"error"` k `error`. Jde o [[TypeScript Type Narrowing|zúžení typu]] podle podmínky. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:3-3, how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:30-44]

```ts
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

export { renderState };
```

## Kontrola úplnosti

Pomocná funkce `assertNever` umožňuje [[Exhaustiveness Checking with never|kontrolovat pokrytí všech variant]]. Pokud do unionu přibude nová varianta bez odpovídající větve, předání zbývajícího stavu do parametru typu `never` odhalí místo, které je třeba doplnit. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:87-103]

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

export { getLabel };
```

## Externí data a runtime validace

Discriminated union sám neověřuje data přijatá z API, formuláře nebo localStorage. TypeScript kontroluje kód při buildu nebo v editoru; externí hodnoty je vhodné přijmout jako `unknown` a ověřit za běhu. S tím souvisí [[Compile-time typy versus runtime validace]]. ^[how-to/typescript-cheat-sheet/README.md:5-5, how-to/typescript-cheat-sheet/README.md:30-37]

## Sources

- [Narrowing and Type Guards](how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md)
- [TypeScript Cheat Sheet](how-to/typescript-cheat-sheet/README.md)
