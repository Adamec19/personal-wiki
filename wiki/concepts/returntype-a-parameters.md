---
title: ReturnType a Parameters
summary: Odvozují návratový typ a typ parametrů z funkce, jejíž signatura slouží jako zdroj pravdy.
sources:
  - how-to/typescript-cheat-sheet/04-utility-types.md
kind: concept
createdAt: "2026-11-11T11:04:03.579Z"
updatedAt: "2026-11-11T11:04:03.579Z"
tags:
  - typescript
  - utility-types
  - funkce
aliases:
  - returntype-a-parameters
  - RAP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# ReturnType a Parameters

`ReturnType` a `Parameters` odvozují typy ze signatury existující funkce. Jsou užitečné, když je funkce zdrojem pravdy a ruční přepisování její signatury by vedlo k duplicitě. ^[how-to/typescript-cheat-sheet/04-utility-types.md:44-57]

## Použití

`ReturnType<typeof funkce>` odvodí typ návratové hodnoty, zatímco `Parameters<typeof funkce>` odvodí typ jejích parametrů. V následujícím příkladu tak vzniknou typy `CreatedUser` a `CreateUserArgs` přímo z funkce `createUser`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:46-55]

```ts
const createUser = (name: string, role: string) => ({
  id: crypto.randomUUID(),
  name,
  role
});

type CreatedUser = ReturnType<typeof createUser>;
type CreateUserArgs = Parameters<typeof createUser>;
```

Tento postup podporuje [[Single source of truth for type contracts|jediný zdroj pravdy pro typové kontrakty]]. Odvozování typů snižuje duplicitu, nemělo by však skrýt důležitý business kontrakt. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-3, how-to/typescript-cheat-sheet/04-utility-types.md:57-57]

## Asynchronní návratová hodnota

Pro odvození typu výsledku asynchronní funkce lze `ReturnType` zkombinovat s [[Awaited]]. Zdroj ukazuje tuto kombinaci na funkci `loadUser`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:70-75]

```ts
const loadUser = async () => ({ id: "1", name: "Ada" });
type LoadedUser = Awaited<ReturnType<typeof loadUser>>;
```

## Sources

- [Utility Types](how-to/typescript-cheat-sheet/04-utility-types.md)
