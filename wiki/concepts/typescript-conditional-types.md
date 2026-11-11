---
title: TypeScript Conditional Types
summary: "Select a resulting type using the condition T extends U ? A : B."
sources:
  - how-to/typescript-cheat-sheet/05-advanced-types.md
kind: concept
createdAt: "2026-11-11T11:04:25.353Z"
updatedAt: "2026-11-11T11:04:25.353Z"
tags:
  - typescript
  - conditional-types
aliases:
  - typescript-conditional-types
  - TCT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript [[conditional-types|Conditional Types]]

[[conditional-types|Conditional Types]] v TypeScriptu vybírají výsledný typ podle podmínky ve tvaru `T extends U ? A : B`. Umožňují například získat typ property, pokud ji vstupní typ obsahuje, a jinak vrátit `never`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:32-44]

## Podmíněný přístup k property

Typ `MessageOf<T>` ověřuje, zda `T` odpovídá typu s property `message`. Pokud ano, získá její typ pomocí [[TypeScript Indexed Access Types|indexed access typu]] `T["message"]`; jinak vrátí `never`. Pro `Email` je výsledkem `string`, zatímco pro `User` je výsledkem `never`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:34-44]

```ts
type MessageOf<T> = T extends { message: unknown } ? T["message"] : never;

type Email = { message: string };
type User = { name: string };

type EmailMessage = MessageOf<Email>;
type UserMessage = MessageOf<User>;
```

## Odvození části typu pomocí `infer`

Klíčové slovo [[TypeScript infer Keyword|infer]] pojmenuje část typu uvnitř conditional type. V následujícím příkladu `TValue` představuje typ hodnoty zabalené v `Promise`. Pokud vstupní typ není `Promise`, výsledkem zůstává původní `T`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:46-54]

```ts
type UnwrapPromise<T> = T extends Promise<infer TValue> ? TValue : T;

type User = UnwrapPromise<Promise<{ id: string }>>;
```

## Distribuce přes union

Pokud conditional type začíná přímo typovým parametrem bez dalšího obalení, označovaným jako „naked type parameter“, může se vyhodnocení distribuovat přes jednotlivé členy unionu. Toto chování popisují [[Distributive Conditional Types]]. Distribuce je užitečná, ale u složitých typů může zhoršovat čitelnost. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:56-56]

## Sources

- how-to/typescript-cheat-sheet/05-advanced-types.md
