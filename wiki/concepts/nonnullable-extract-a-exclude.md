---
title: NonNullable, Extract a Exclude
summary: Filtrují členy union typů odstraněním null a undefined, výběrem odpovídajících členů nebo jejich vyloučením.
sources:
  - how-to/typescript-cheat-sheet/04-utility-types.md
kind: concept
createdAt: "2026-11-11T11:04:15.648Z"
updatedAt: "2026-11-11T11:04:15.648Z"
tags:
  - typescript
  - utility-types
  - union-types
aliases:
  - nonnullable-extract-a-exclude
  - NEAE
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# NonNullable, Extract a Exclude

`NonNullable`, `Extract` a `Exclude` jsou utility typy pro odvozování nových typů z existujících union typů. Pomáhají omezit duplicitu, aniž by měly zakrývat důležitý business kontrakt. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-3, how-to/typescript-cheat-sheet/04-utility-types.md:59-68]

## NonNullable

`NonNullable<T>` odstraní z typu `T` hodnoty `null` a `undefined`. V následujícím příkladu tak `UserOnly` odpovídá typu `User`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:62-63]

```ts
type User = {
  id: string;
  name: string;
  email: string;
};

type MaybeUser = User | null | undefined;
type UserOnly = NonNullable<MaybeUser>;
```

## Extract

`Extract<T, U>` vybere z union typu `T` členy odpovídající typu `U`. Z uvedených událostí tak `WriteEvents` obsahuje pouze `"created" | "updated"`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:65-66]

```ts
type Events = "created" | "updated" | "deleted";
type WriteEvents = Extract<Events, "created" | "updated">;
```

## Exclude

`Exclude<T, U>` odstraní z union typu `T` členy odpovídající typu `U`. V příkladu odebere `"deleted"`, takže `ReadOnlyEvents` odpovídá typu `"created" | "updated"`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:65-67]

```ts
type Events = "created" | "updated" | "deleted";
type ReadOnlyEvents = Exclude<Events, "deleted">;
```

## Použití a související koncepty

Před vytvářením vlastního utility typu je vhodné zvážit standardní utility, [[TypeScript Indexed Access Types|indexed access]] nebo [[The satisfies operator|satisfies]]. Vlastní typ má smysl, pokud se vzor opakuje a jeho pojmenování zlepší čitelnost; více viz [[Návrh vlastních utility typů]]. ^[how-to/typescript-cheat-sheet/04-utility-types.md:77-79]

## Sources

- [Utility Types](how-to/typescript-cheat-sheet/04-utility-types.md)
