---
title: Key-constrained generic property updates
summary: Combine K extends keyof T with T[K] to constrain a property-update helper to valid keys and their corresponding value types.
sources:
  - how-to/typescript-cheat-sheet/09-snippets.md
kind: concept
createdAt: "2026-11-11T11:05:55.371Z"
updatedAt: "2026-11-11T11:05:55.371Z"
tags:
  - typescript
  - generics
  - indexed-access-types
aliases:
  - key-constrained-generic-property-updates
  - KGPU
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Key-constrained generic property updates

A generic property update helper connects an object's type, the selected key, and the replacement value. The constraint `K extends keyof T` restricts the key to a property of `T`, while `T[K]` requires a value of that property's type. ^[how-to/typescript-cheat-sheet/09-snippets.md:94-99]

## Implementation

```ts
const setProperty = <T, K extends keyof T>(
  object: T,
  key: K,
  value: T[K]
): T => {
  return { ...object, [key]: value };
};

export { setProperty };
```

The helper returns a new object by spreading the original properties and assigning the supplied value to the computed key. Its declared return type is `T`. ^[how-to/typescript-cheat-sheet/09-snippets.md:97-101]

## Related concepts

The helper combines [[Generic Functions and Components]] with [[Omezení generických typů pomocí extends|generic constraints]] and [[TypeScript Indexed Access Types|indexed access types]] to express the relationship between a property key and its value type. ^[how-to/typescript-cheat-sheet/09-snippets.md:94-99]

## Sources

- [TypeScript Snippets](how-to/typescript-cheat-sheet/09-snippets.md)
