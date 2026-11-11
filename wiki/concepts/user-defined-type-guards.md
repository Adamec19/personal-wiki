---
title: User-Defined Type Guards
summary: Functions returning a type predicate such as value is SomeType enable narrowing through custom runtime checks, whose correctness the implementation must ensure.
sources:
  - how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md
kind: concept
createdAt: "2026-11-11T11:03:44.099Z"
updatedAt: "2026-11-11T11:03:44.099Z"
tags:
  - typescript
  - type-guards
  - runtime-validation
aliases:
  - user-defined-type-guards
  - UTG
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# User-Defined Type Guards

A user-defined type guard is a function with a type predicate such as `value is SomeType`. It tells TypeScript how a custom check narrows a broader type to a specific variant, supporting [[TypeScript Type Narrowing]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:3-3, how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:46-48]

## Defining and using a guard

The `isFish` guard checks whether an animal has a `swim` property. Its predicate, `animal is Fish`, lets TypeScript narrow `Fish | Bird` to `Fish` when the check succeeds. After that branch returns, the remaining animal is treated as `Bird`. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:50-65]

```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };

const isFish = (animal: Fish | Bird): animal is Fish => {
  return "swim" in animal;
};

const move = (animal: Fish | Bird): void => {
  if (isFish(animal)) {
    animal.swim();
    return;
  }

  animal.fly();
};
```

## Validating unknown values

A guard accepting `unknown` can combine several runtime checks. The following example verifies that the value is an object, is not `null`, contains `message`, and has a string value for that property. This combines [[typeof Type Guards]] with [[Property Validation with in and Null Checks]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:72-85]

```ts
const hasMessage = (value: unknown): value is { message: string } => {
  return (
    typeof value === "object" &&
    value !== null &&
    "message" in value &&
    typeof value.message === "string"
  );
};
```

## Correctness requirement

The predicate must match what the function actually verifies at runtime. An incorrect predicate can convince the compiler that a value has a particular type, but it does not change the runtime data. This distinction is central to [[Runtime validation versus type assertions]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:70-70]

## Sources

- [Narrowing and Type Guards](how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md)
