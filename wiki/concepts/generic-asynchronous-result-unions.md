---
title: Generic asynchronous result unions
summary: Represent idle, loading, success, and error states with a discriminated union whose success variant carries generic data.
sources:
  - how-to/typescript-cheat-sheet/09-snippets.md
kind: concept
createdAt: "2026-11-11T11:05:48.545Z"
updatedAt: "2026-11-11T11:05:48.545Z"
tags:
  - typescript
  - generics
  - async-state
aliases:
  - generic-asynchronous-result-unions
  - GARU
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Generic asynchronous result unions

Generický typ `AsyncResult<T>` představuje výsledek asynchronní operace jako [[Discriminated Unions|diskriminovanou unii]] se společným polem `status`. Rozlišuje čtyři stavy: `idle`, `loading`, `success` a `error`. Úspěšný stav obsahuje `data` typu `T`, chybový stav obsahuje `error` typu `Error`; zbývající dva stavy mají pouze diskriminátor. ^[how-to/typescript-cheat-sheet/09-snippets.md:34-41]

## Definice a pomocná funkce

Parametr `T` určuje typ úspěšných dat. Generická funkce `success` přijímá hodnotu tohoto typu a vrací ji zabalenou do úspěšné varianty `AsyncResult<T>`. Ukázka používá zápis `<T,>` a named export na konci. ^[how-to/typescript-cheat-sheet/09-snippets.md:37-45]

```ts
type AsyncResult<T> =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: Error };

const success = <T,>(data: T): AsyncResult<T> => ({
  status: "success",
  data,
});

export { success };
```

## Sources

- [TypeScript Snippets](how-to/typescript-cheat-sheet/09-snippets.md)
