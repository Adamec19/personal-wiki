---
title: Object type guards
summary: Use a type predicate and a non-null object check to narrow unknown values to Record<string, unknown>.
sources:
  - how-to/typescript-cheat-sheet/09-snippets.md
kind: concept
createdAt: "2026-11-11T11:05:48.227Z"
updatedAt: "2026-11-11T11:05:48.227Z"
tags:
  - typescript
  - type-narrowing
  - runtime-checks
aliases:
  - object-type-guards
  - OTG
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Object type guards

Object type guard ověřuje hodnotu typu `unknown` a pomocí typového predikátu ji zužuje na `Record<string, unknown>`. Ukázková funkce `isRecord` kontroluje, že hodnota má `typeof` rovné `"object"` a zároveň není `null`. Spojuje tak [[typeof Type Guards]] s explicitní kontrolou nenulové hodnoty. ^[how-to/typescript-cheat-sheet/09-snippets.md:48-56]

## Implementace

```ts
const isRecord = (value: unknown): value is Record<string, unknown> => {
  return typeof value === "object" && value !== null;
};

export { isRecord };
```

Návratový typ `value is Record<string, unknown>` vyjadřuje zúžení vstupu po úspěšné kontrole. Hodnoty jednotlivých vlastností zůstávají typu `unknown`; tento guard nekontroluje konkrétní klíče ani jejich datové typy. Souvisí proto s [[TypeScript Type Narrowing]] a dalšími kontrolami popsanými v [[Property Validation with in and Null Checks]]. ^[how-to/typescript-cheat-sheet/09-snippets.md:51-53]

## Sources

- [TypeScript Snippets](how-to/typescript-cheat-sheet/09-snippets.md)
