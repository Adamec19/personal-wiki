---
title: Pick a Omit
summary: Vytvářejí typy výběrem nebo vynecháním vlastností, pokud výsledný kontrakt skutečně představuje podmnožinu původního.
sources:
  - how-to/typescript-cheat-sheet/04-utility-types.md
kind: concept
createdAt: "2026-11-11T11:04:01.710Z"
updatedAt: "2026-11-11T11:04:01.710Z"
tags:
  - typescript
  - utility-types
aliases:
  - pick-a-omit
  - PAO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Pick a Omit

`Pick` a `Omit` jsou utility typy v TypeScriptu, které odvozují nový typ jako podmnožinu existujícího kontraktu. Pomáhají omezit duplicitu, ale neměly by zakrývat důležitý business kontrakt. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-28]

## Výběr a vynechání vlastností

`Pick<T, K>` vybírá z typu `T` uvedené vlastnosti. V příkladu vzniká `UserPreview`, který obsahuje pouze `id` a `name`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:21-25]

```ts
type User = {
  id: string;
  name: string;
  email: string;
};

type UserPreview = Pick<User, "id" | "name">;
```

`Omit<T, K>` vytváří typ bez uvedených vlastností. Typ `UserWithoutEmail` tak vychází z `User`, ale vynechává `email`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:8-12, how-to/typescript-cheat-sheet/04-utility-types.md:21-26]

```ts
type UserWithoutEmail = Omit<User, "email">;
```

## Kdy je použít

Oba typy jsou vhodné, pokud nový typ skutečně představuje podmnožinu původního kontraktu. Před tvorbou vlastní utility je vhodné zvážit standardní utility, [[TypeScript Indexed Access Types|indexed access]] nebo [[The satisfies operator|satisfies]]. Vlastní typ má smysl, když se vzor opakuje a jeho pojmenování zlepší čitelnost. ^[how-to/typescript-cheat-sheet/04-utility-types.md:28-28, how-to/typescript-cheat-sheet/04-utility-types.md:77-79]

## Sources

- [Utility Types](how-to/typescript-cheat-sheet/04-utility-types.md)
