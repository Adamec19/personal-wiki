---
title: Exhaustiveness Checking with never
summary: Passing an unhandled union variant to an assertNever function exposes incomplete switch statements when new variants are added.
sources:
  - how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md
kind: concept
createdAt: "2026-11-11T11:03:49.531Z"
updatedAt: "2026-11-11T11:03:49.531Z"
tags:
  - typescript
  - union-types
  - exhaustiveness
aliases:
  - exhaustiveness-checking-with-never
  - ECWN
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Exhaustiveness Checking with never

Exhaustiveness checking ověřuje, že jsou obslouženy všechny varianty union typu. Funkce `assertNever` s parametrem typu `never` umožňuje odhalit místa, která je potřeba doplnit po přidání nové varianty. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:87-106]

## Princip

U [[Discriminated Unions|diskriminovaného unionu]] rozlišuje jednotlivé varianty společná vlastnost, například `status`. Ve větvích příkazu `switch` TypeScript zúží typ na odpovídající variantu. Pokud jsou všechny varianty obslouženy, větev `default` může předat zbývající hodnotu funkci přijímající `never`. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:21-44, how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:89-103]

## Příklad

Následující union představuje načítání, úspěch a chybu. Funkce `getLabel` obsluhuje všechny tři varianty a zbývající větev předává do `assertNever`. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:24-28, how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:91-103]

```ts
type LoadingState = { status: "loading" };
type SuccessState = { status: "success"; data: string[] };
type ErrorState = { status: "error"; error: Error };

type RequestState = LoadingState | SuccessState | ErrorState;

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

Po rozšíření `RequestState` o další variantu bez odpovídající větve již zbývající hodnota neodpovídá typu `never`. Volání `assertNever(state)` tak upozorní na neúplné zpracování. Pokud se funkce `assertNever` spustí za běhu, vyhodí chybu s neobslouženou hodnotou. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:89-103]

## Sources

- [Narrowing and Type Guards](how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md)
