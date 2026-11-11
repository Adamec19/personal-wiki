---
title: TypeScript Mapped Types
summary: Create new types by iterating over the keys of an existing type and transforming their property types.
sources:
  - how-to/typescript-cheat-sheet/05-advanced-types.md
kind: concept
createdAt: "2026-11-11T11:04:16.432Z"
updatedAt: "2026-11-11T11:04:16.432Z"
tags:
  - typescript
  - type-transformations
aliases:
  - typescript-mapped-types
  - TMT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Mapped Types

Mapped types v TypeScriptu vytvářejí nový typ procházením klíčů existujícího typu. Umožňují tak odvodit strukturu nového typu ze struktury původního. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:19-30]

## Základní syntaxe

Zápis `[K in keyof T]` projde klíče typu `T`. V následujícím příkladu přiřadí mapped type `Flags<T>` každému klíči typ `boolean`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:21-26]

```ts
type Flags<T> = {
  [K in keyof T]: boolean;
};
```

## Příklad: příznaky formuláře

Typ `FormTouched` odvozený pomocí `Flags<Form>` zachovává klíče `email` a `phone`, ale jejich původní typ `string` nahrazuje typem `boolean`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:24-30]

```ts
type Form = { email: string; phone: string };
type FormTouched = Flags<Form>;

// Výsledná struktura:
// { email: boolean; phone: boolean }
```

## Související koncepty

Zatímco mapped types vytvářejí nový typ procházením klíčů, [[TypeScript Indexed Access Types]] získávají typ konkrétní vlastnosti existujícího typu, například pomocí `Config["api"]`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:3-30]

## Sources

- [Advanced Types](how-to/typescript-cheat-sheet/05-advanced-types.md)
