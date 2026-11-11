---
title: Branded types
summary: Distinguish values sharing the same runtime type using compile-time brands, while recognizing that branding provides no runtime validation.
sources:
  - how-to/typescript-cheat-sheet/09-snippets.md
kind: concept
createdAt: "2026-11-11T11:05:50.824Z"
updatedAt: "2026-11-11T11:05:50.824Z"
tags:
  - typescript
  - branded-types
  - type-safety
aliases:
  - branded-types
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Branded types

Branded types rozlišují hodnoty, které mají stejný runtime typ, ale nesmějí se vzájemně zaměnit. Slouží jako ochrana při kontrole typů v době kompilace. ^[how-to/typescript-cheat-sheet/09-snippets.md:78-92]

## Příklad: identifikátor uživatele

Typ `UserId` kombinuje `string` se značkou `readonly __brand: "UserId"`. Funkce `toUserId` převádí řetězec pomocí typového přetypování a funkce `loadUser` přijímá parametr typu `UserId`. ^[how-to/typescript-cheat-sheet/09-snippets.md:83-89]

```ts
type UserId = string & { readonly __brand: "UserId" };

const toUserId = (value: string): UserId => value as UserId;

const loadUser = (id: UserId) => fetch(`/users/${id}`);

export { toUserId, loadUser };
```

## Omezení

Branding není runtime validace. Přetypování v `toUserId` poskytuje compile-time ochranu proti záměně hodnot, ale neověřuje platnost vstupního řetězce za běhu. S tím souvisí rozdíl mezi [[Compile-time typy versus runtime validace|compile-time typy a runtime validací]] a téma [[Runtime validation versus type assertions]]. ^[how-to/typescript-cheat-sheet/09-snippets.md:85-92]

## Sources

- [TypeScript Snippets](how-to/typescript-cheat-sheet/09-snippets.md)
