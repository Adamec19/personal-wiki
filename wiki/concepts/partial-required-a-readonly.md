---
title: Partial, Required a Readonly
summary: Upravují volitelnost nebo zapisovatelnost vlastností; Partial se hodí pro patch requesty, ale nenahrazuje přesný typ formuláře.
sources:
  - how-to/typescript-cheat-sheet/04-utility-types.md
kind: concept
createdAt: "2026-11-11T11:03:59.582Z"
updatedAt: "2026-11-11T11:03:59.582Z"
tags:
  - typescript
  - utility-types
aliases:
  - partial-required-a-readonly
  - PRAR
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Partial, Required a Readonly

`Partial`, `Required` a `Readonly` jsou utility typy, které odvozují nové typy z existujícího kontraktu. Pomáhají omezit duplicitu, ale neměly by zakrývat důležitý business kontrakt. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-16]

## Použití

Společným základem může být typ `User`, ze kterého vzniknou varianty pro částečná data, povinné vlastnosti a vlastnosti pouze pro čtení. ^[how-to/typescript-cheat-sheet/04-utility-types.md:5-16]

```ts
type User = {
  id: string;
  name: string;
  email: string;
};

type UserPatch = Partial<User>;
type CompleteUser = Required<User>;
type ImmutableUser = Readonly<User>;
```

`Partial<User>` vytváří variantu s volitelnými vlastnostmi, `Required<User>` variantu se všemi vlastnostmi povinnými a `Readonly<User>` variantu s vlastnostmi pouze pro čtení. V uvedeném příkladu už má `User` všechny vlastnosti povinné, takže `Required<User>` tento požadavek nemění. ^[how-to/typescript-cheat-sheet/04-utility-types.md:5-16]

## Kdy je použít

`Partial` se hodí například pro patch request. Neměl by však nahrazovat přesný typ formuláře: konkrétní kontrakt má přednost před pouhým omezením duplicity. S tím souvisí [[Single source of truth for type contracts]]. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-19]

Před vytvářením vlastního utility typu je vhodné zvážit standardní utility, [[TypeScript Indexed Access Types|indexed access]] nebo [[The satisfies operator|satisfies]]. Vlastní typ má smysl, pokud se vzor opakuje a jeho pojmenování zlepší čitelnost; viz [[Návrh vlastních utility typů]]. ^[how-to/typescript-cheat-sheet/04-utility-types.md:77-79]

## Sources

- [Utility Types](how-to/typescript-cheat-sheet/04-utility-types.md)
