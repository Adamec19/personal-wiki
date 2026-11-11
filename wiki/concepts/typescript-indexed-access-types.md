---
title: TypeScript Indexed Access Types
summary: Extract property types with T[K] or an array element type with (typeof OPTIONS)[number].
sources:
  - how-to/typescript-cheat-sheet/05-advanced-types.md
kind: concept
createdAt: "2026-11-11T11:04:14.614Z"
updatedAt: "2026-11-11T11:04:14.614Z"
tags:
  - typescript
  - type-system
aliases:
  - typescript-indexed-access-types
  - TIAT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Indexed Access Types

Indexed access types umožňují získat typ konkrétní property z existujícího typu pomocí zápisu `Typ["klíč"]`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:3-14]

## Typ property objektu

Typ `Config` obsahuje properties `api` a `features`. Zápisy `Config["api"]` a `Config["features"]` z nich odvozují samostatné typy. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:5-14]

```ts
type Config = {
  api: { baseUrl: string; timeout: number };
  features: { payments: boolean };
};

type ApiConfig = Config["api"];
type FeatureFlags = Config["features"];
```

## Typ prvku pole

Zápis `(typeof OPTIONS)[number]` představuje typ jednoho prvku pole `OPTIONS`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:17-17]

## Použití v [[conditional-types|Conditional Types]]

Indexed access lze použít také uvnitř [[TypeScript Conditional Types|conditional types]]. V následujícím příkladu `MessageOf<T>` získá typ property `message`, pokud `T` odpovídá požadovanému tvaru; jinak je výsledkem `never`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:32-44]

```ts
type MessageOf<T> = T extends { message: unknown } ? T["message"] : never;

type Email = { message: string };
type User = { name: string };

type EmailMessage = MessageOf<Email>;
type UserMessage = MessageOf<User>;
```

## Sources

- [Advanced Types](how-to/typescript-cheat-sheet/05-advanced-types.md)
