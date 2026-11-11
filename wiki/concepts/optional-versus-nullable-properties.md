---
title: Optional Versus Nullable Properties
summary: Optional properties may be absent, while required nullable properties must exist but can contain null.
sources:
  - how-to/typescript-cheat-sheet/01-type-system-basics.md
kind: concept
createdAt: "2026-11-11T11:02:50.017Z"
updatedAt: "2026-11-11T11:02:50.017Z"
tags:
  - typescript
  - optional-properties
  - nullability
aliases:
  - optional-versus-nullable-properties
  - OVNP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Optional Versus Nullable Properties

Optional and nullable properties express different meanings in a TypeScript object contract: an optional property may be absent, while a nullable property exists but may contain an explicitly empty value, `null`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:51-60]

## Syntax and meaning

In this `Profile` type, `nickname?: string` allows the `nickname` property to be omitted. By contrast, `avatarUrl: string | null` requires the property to exist and allows its value to be either a string or `null`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:53-60]

```ts
type Profile = {
  nickname?: string;
  avatarUrl: string | null;
};
```

## Choosing the contract

Use an optional property to represent a property that may be missing, and a nullable property to represent a present property with an explicitly empty value. Keep these meanings distinct rather than mixing them without a reason, and distinguish `undefined` from `null` deliberately. The nullable form uses a [[Union and Literal Types|union]] to express the permitted value alternatives. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:49-60, how-to/typescript-cheat-sheet/01-type-system-basics.md:103-104]

## Sources

- [Type System Basics](how-to/typescript-cheat-sheet/01-type-system-basics.md)
