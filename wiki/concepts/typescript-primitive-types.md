---
title: TypeScript Primitive Types
summary: TypeScript provides primitive types such as string, number, boolean, null, and undefined.
sources:
  - how-to/typescript-cheat-sheet/01-type-system-basics.md
kind: concept
createdAt: "2026-11-11T11:02:42.121Z"
updatedAt: "2026-11-11T11:02:42.121Z"
tags:
  - typescript
  - type-system
aliases:
  - typescript-primitive-types
  - TPT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Primitive Types

TypeScript uses primitive type annotations to describe values such as strings, numbers, booleans, `null`, and `undefined`. The source illustrates each with an explicitly typed declaration. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:3-11]

```ts
const name: string = "Ada";
const age: number = 37;
const isActive: boolean = true;
const nothing: null = null;
const missing: undefined = undefined;
```

## Inference and explicit annotations

In most cases, let TypeScript infer the type from the assigned value. Add an explicit annotation when it documents a contract, protects a public API, or helps with narrowing. See [[Type Inference and Explicit Annotations]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:13-20]

```ts
const name = "Ada";
const age = 37;
```

## Choosing precise types

An unrestricted `string` may be too broad when only specific values are valid. A union of literals expresses the permitted alternatives more precisely, as described in [[Union and Literal Types]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:41-49]

```ts
type Status = "idle" | "loading" | "success" | "error";

const status: Status = "loading";
```

TypeScript often widens values to general types such as `string` or `number`. Using `as const` preserves exact literals and readonly properties. See [[Const Assertions]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:92-99]

## Missing and explicitly empty values

Distinguish a property that may be absent from a required property whose value may be `null`. In the following example, `nickname` may be missing, while `avatarUrl` must exist but may hold an explicitly empty value. See [[Optional Versus Nullable Properties]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:51-60]

```ts
type Profile = {
  nickname?: string;
  avatarUrl: string | null;
};
```

## Sources

- [Type System Basics](how-to/typescript-cheat-sheet/01-type-system-basics.md)
