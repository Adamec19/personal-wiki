---
title: Exhaustive switches with never
summary: Pass an unhandled discriminated-union value to an assertNever helper to enforce exhaustive switch handling.
sources:
  - how-to/typescript-cheat-sheet/09-snippets.md
kind: concept
createdAt: "2026-11-11T11:05:52.101Z"
updatedAt: "2026-11-11T11:05:52.101Z"
tags:
  - typescript
  - discriminated-unions
  - exhaustiveness
aliases:
  - exhaustive-switches-with-never
  - ESWN
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Exhaustive switches with never

Vyčerpávající `switch` zpracovává všechny varianty union typu. Pomocná funkce `assertNever` přijímá hodnotu typu `never` a v `default` větvi slouží ke kontrole, že nezůstala žádná nezpracovaná varianta. Tento vzor souvisí s [[Discriminated Unions]] a [[Never and Exhaustiveness Checking]]. ^[how-to/typescript-cheat-sheet/09-snippets.md:58-73]

## Příklad

Typ `Action` rozlišuje dvě varianty pomocí vlastnosti `type`. Funkce `getActionLabel` každé variantě přiřazuje popisek a zbývající větev předává do `assertNever`. ^[how-to/typescript-cheat-sheet/09-snippets.md:61-73]

```ts
type Action = { type: "save" } | { type: "cancel" };

const assertNever = (value: never): never => {
  throw new Error(`Unhandled action: ${String(value)}`);
};

const getActionLabel = (action: Action): string => {
  switch (action.type) {
    case "save": return "Uložit";
    case "cancel": return "Zrušit";
    default: return assertNever(action);
  }
};

export { getActionLabel };
```

Pokud do typu `Action` přibude další varianta bez odpovídající větve `case`, zbývající hodnota nebude při volání `assertNever(action)` odpovídat parametru typu `never`. Kontrola tak upozorní na neúplné zpracování unionu. Pokud se funkce `assertNever` skutečně zavolá za běhu, vyhodí chybu s informací o nezpracované akci. ^[how-to/typescript-cheat-sheet/09-snippets.md:61-73]

## Sources

- [TypeScript Snippets](how-to/typescript-cheat-sheet/09-snippets.md)
