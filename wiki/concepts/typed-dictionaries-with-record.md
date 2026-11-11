---
title: Typed dictionaries with Record
summary: Use satisfies Record<Status, string> to check that a label dictionary covers every member of a status union.
sources:
  - how-to/typescript-cheat-sheet/09-snippets.md
kind: concept
createdAt: "2026-11-11T11:05:44.583Z"
updatedAt: "2026-11-11T11:05:44.583Z"
tags:
  - typescript
  - mapped-types
  - dictionaries
aliases:
  - typed-dictionaries-with-record
  - TDWR
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Typed dictionaries with Record

A typed dictionary maps a defined set of keys to values of a specified type. The source uses `satisfies Record<Status, string>` to check an object containing a string label for each member of the `Status` union. ^[how-to/typescript-cheat-sheet/09-snippets.md:19-32]

## Status labels

Define the allowed keys as a [[Union and Literal Types|literal union]], then use [[The satisfies operator|satisfies]] with `Record<Status, string>` to check the dictionary. In this example, the keys are `idle`, `loading`, `success`, and `error`, and their values are Czech display labels. ^[how-to/typescript-cheat-sheet/09-snippets.md:22-29]

```ts
type Status = "idle" | "loading" | "success" | "error";

const statusLabels = {
  idle: "Čeká",
  loading: "Načítá se",
  success: "Hotovo",
  error: "Chyba"
} satisfies Record<Status, string>;

export { statusLabels };
```

## Configuration dictionaries

The source also combines `as const` with `satisfies Record<string, ProductConfig>` for a product configuration dictionary. Each entry has a `label` and an `enabled` flag, while `keyof typeof PRODUCTS` derives `ProductCode` from the object's keys. This pattern relates to [[Configuration Objects with as const satisfies]]. ^[how-to/typescript-cheat-sheet/09-snippets.md:3-17]

```ts
type ProductConfig = {
  label: string;
  enabled: boolean;
};

const PRODUCTS = {
  basic: { label: "Basic", enabled: true },
  premium: { label: "Premium", enabled: false }
} as const satisfies Record<string, ProductConfig>;

type ProductCode = keyof typeof PRODUCTS;
```

## Sources

- [TypeScript Snippets](how-to/typescript-cheat-sheet/09-snippets.md)
