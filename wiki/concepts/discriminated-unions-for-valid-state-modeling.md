---
title: Discriminated unions for valid state modeling
summary: Model mutually exclusive states with discriminated unions to prevent invalid combinations of flags and associated data.
sources:
  - how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md
kind: concept
createdAt: "2026-11-11T11:05:22.870Z"
updatedAt: "2026-11-11T11:05:22.870Z"
tags:
  - typescript
  - state-modeling
  - type-safety
aliases:
  - discriminated-unions-for-valid-state-modeling
  - DUFVSM
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# [[discriminated-unions|Discriminated Unions]] for valid state modeling

Discriminated union modeluje stav jako sjednocení konkrétních variant rozlišených společnou vlastností, například `status`. Každá varianta obsahuje pouze data odpovídající danému stavu. Zdroj tento přístup doporučuje před kombinacemi boolean příznaků, které mohou připustit neplatné stavy. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:3-25]

## Problém s boolean příznaky

Samostatné příznaky `isLoading` a `isError` spolu s volitelnými vlastnostmi `data` a `error` nevyjadřují vazbu mezi stavem a jeho daty. Následující typ například umožňuje současně nastavit `isLoading: true` a poskytnout `data`. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:5-25]

```ts
type Result = {
  isLoading: boolean;
  isError: boolean;
  data?: string[];
  error?: Error;
};
```

## Modelování platných variant

Pomocí [[Discriminated Unions]] lze výsledek rozdělit na tři varianty: načítání, úspěch s povinnými daty a chybu s povinným objektem `Error`. Vlastnost `status` rozlišuje jednotlivé varianty a union vylučuje neplatné kombinace původního modelu. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:16-25]

```ts
type Result =
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; error: Error };
```

Při kontrole návrhu typu je podstatné ověřit, zda union skutečně znemožňuje neplatné stavy. Pro [[Správa stavu API požadavků|správu stavu API požadavků]] tak model přímo vyjadřuje, které údaje patří k jednotlivým výsledkům. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:19-25, how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:76-82]

## Hranice typové bezpečnosti

Správně navržený union nenahrazuje ověření externích dat. Type assertion pouze umlčí compiler; data nezmění ani neověří. Na externím vstupu je proto potřeba parser, schema nebo skutečný type guard, jak popisuje [[Runtime validation versus type assertions]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-33]

## Sources

- [Patterns and Pitfalls](how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md)
