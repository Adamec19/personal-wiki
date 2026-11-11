---
title: TypeScript Function Overloads
summary: Describe multiple public call signatures for one implementation, using overloads when they improve the API over a simpler union.
sources:
  - how-to/typescript-cheat-sheet/05-advanced-types.md
kind: concept
createdAt: "2026-11-11T11:04:35.942Z"
updatedAt: "2026-11-11T11:04:35.942Z"
tags:
  - typescript
  - functions
  - api-design
aliases:
  - typescript-function-overloads
  - TFO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Function Overloads

Function overloads describe multiple public call signatures for a single function. The implementation must support every declared variant. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:86-88]

## Example

A user lookup can expose one signature for a single ID, returning `User | null`, and another for an array of IDs, returning `User[]`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:91-96]

```ts
type User = { id: string };

interface FindUser {
  (id: string): User | null;
  (ids: string[]): User[];
}
```

## When to use overloads

Use overloads when the separate signatures meaningfully improve the function’s API. Otherwise, a [[Union and Literal Types|union type]] is often simpler. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:106-106]

## Sources

- [Advanced Types](how-to/typescript-cheat-sheet/05-advanced-types.md)
