---
title: Distributive Conditional Types
summary: Conditional types with a naked type parameter can distribute over union members, offering flexibility at a potential readability cost.
sources:
  - how-to/typescript-cheat-sheet/05-advanced-types.md
kind: concept
createdAt: "2026-11-11T11:04:31.064Z"
updatedAt: "2026-11-11T11:04:31.064Z"
tags:
  - typescript
  - conditional-types
  - union-types
aliases:
  - distributive-conditional-types
  - DCT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Distributive [[conditional-types|Conditional Types]]

Distributive [[conditional-types|Conditional Types]] v TypeScriptu umožňují vyhodnocovat podmíněný typ pro jednotlivé členy unionu. K distribuci může docházet, pokud podmíněný typ začíná přímo typovým parametrem, označovaným jako „naked type parameter“. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:56-56]

## Základní syntaxe

[[TypeScript Conditional Types|Conditional type]] má tvar `T extends U ? A : B`. Následující příklad získává typ property `message`, pokud ji vstupní typ obsahuje; jinak vrací `never`. Přístup `T["message"]` využívá [[TypeScript Indexed Access Types|indexed access type]]. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:34-44]

```ts
type MessageOf<T> = T extends { message: unknown }
  ? T["message"]
  : never;

type Email = { message: string };
type User = { name: string };

type EmailMessage = MessageOf<Email>;
type UserMessage = MessageOf<User>;
```

## Distribuce přes union

V uvedené definici stojí vlevo od `extends` přímo parametr `T`. Při použití unionu se proto podmínka může vyhodnocovat pro jeho jednotlivé členy. Tato distribuce je užitečná, ale u složitých typů může zhoršovat čitelnost. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:37-56]

## Sources

- [Advanced Types](how-to/typescript-cheat-sheet/05-advanced-types.md)
