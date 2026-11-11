---
title: Type Inference and Explicit Annotations
summary: Prefer type inference by default and add explicit annotations to document contracts, protect public APIs, or support narrowing.
sources:
  - how-to/typescript-cheat-sheet/01-type-system-basics.md
kind: concept
createdAt: "2026-11-11T11:02:44.185Z"
updatedAt: "2026-11-11T11:02:44.185Z"
tags:
  - typescript
  - type-inference
aliases:
  - type-inference-and-explicit-annotations
  - Explicit Annotations and Type Inference
  - TIAEA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Type Inference and Explicit Annotations

TypeScript can infer types from assigned values, so explicit annotations are unnecessary in many cases. A practical default is to let inference work and add annotations where they document a contract, protect a public API, or help with [[TypeScript Type Narrowing|type narrowing]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:13-20]

## Inferred types

Simple declarations can rely on inference without writing a type after the variable name. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:13-18]

```ts
const name = "Ada";
const age = 37;
```

## Explicit annotations

Explicit annotations state the intended type directly. The source demonstrates this syntax with primitive types such as `string`, `number`, and `boolean`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:3-11]

```ts
const name: string = "Ada";
const age: number = 37;
const isActive: boolean = true;
```

Annotations are useful when the type communicates a meaningful constraint. For example, a [[Union and Literal Types|union of literals]] expresses a fixed set of allowed statuses more precisely than a general `string`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:20-20, how-to/typescript-cheat-sheet/01-type-system-basics.md:41-49]

```ts
type Status = "idle" | "loading" | "success" | "error";

const status: Status = "loading";
```

## Preserving literal types

Without `as const`, TypeScript often widens values to general types such as `string` or `number`. [[Const Assertions|Const assertions]] preserve exact literals and readonly properties, allowing a type to be derived from the declared values. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:92-99]

```ts
const DIRECTIONS = ["up", "down", "left", "right"] as const;
type Direction = (typeof DIRECTIONS)[number];
```

The guiding rule is to use inference for ordinary declarations and explicit annotations where they clarify or protect a contract. When exact literal values matter, consider `as const`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:13-20, how-to/typescript-cheat-sheet/01-type-system-basics.md:92-99]

## Sources

- [Type System Basics](how-to/typescript-cheat-sheet/01-type-system-basics.md)
