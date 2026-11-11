---
title: Never and Exhaustiveness Checking
summary: Never represents impossible values or functions that cannot return successfully and supports exhaustive switch checks.
sources:
  - how-to/typescript-cheat-sheet/01-type-system-basics.md
kind: concept
createdAt: "2026-11-11T11:02:57.468Z"
updatedAt: "2026-11-11T11:02:57.468Z"
tags:
  - typescript
  - never
  - exhaustiveness
aliases:
  - never-and-exhaustiveness-checking
  - Exhaustiveness Checking and Never
  - NAEC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Never and Exhaustiveness Checking

In TypeScript, `never` describes a value that cannot occur or a function that never returns successfully. A common use is exhaustiveness checking in a `switch`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:78-90]

## The `assertNever` helper

An `assertNever` helper accepts a value of type `never` and throws an error. Its return type is also `never`, reflecting that it cannot return successfully. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:80-88]

```ts
const assertNever = (value: never): never => {
  throw new Error(`Unhandled value: ${String(value)}`);
};

export { assertNever };
```

## Exhaustiveness and unions

[[Union and Literal Types]] define a set of permitted variants, such as `"idle" | "loading" | "success" | "error"`. This gives a precise set of possibilities to handle, while `never` is commonly used to check exhaustiveness in a `switch`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:41-49, how-to/typescript-cheat-sheet/01-type-system-basics.md:78-90]

Unlike `never`, [[Unknown Versus Any|unknown]] represents data that must be narrowed before use, while `any` disables type checking. These types serve different purposes: untrusted input, bypassed checking, and impossible values respectively. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:62-90]

## Sources

- [Type System Basics](how-to/typescript-cheat-sheet/01-type-system-basics.md)
