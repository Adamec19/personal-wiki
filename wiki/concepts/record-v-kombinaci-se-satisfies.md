---
title: Record v kombinaci se satisfies
summary: Kontroluje úplnost klíčů objektového literálu a odhaluje překlepy v klíčích podle zadaného typu.
sources:
  - how-to/typescript-cheat-sheet/04-utility-types.md
kind: concept
createdAt: "2026-11-11T11:03:59.705Z"
updatedAt: "2026-11-11T11:03:59.705Z"
tags:
  - typescript
  - utility-types
  - typová-kontrola
aliases:
  - record-v-kombinaci-se-satisfies
  - RVKSS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Record v kombinaci se satisfies

`Record` v kombinaci s [[The satisfies operator|operátorem satisfies]] kontroluje, že objekt obsahuje všechny požadované klíče a nepřidává klíče s překlepem. ^[how-to/typescript-cheat-sheet/04-utility-types.md:30-42]

## Příklad

Typ `Permission` vymezuje klíče mapy popisků. Objekt `permissionLabels` používá `satisfies Record<Permission, string>`, aby hlídal úplnost klíčů a jejich správný zápis. ^[how-to/typescript-cheat-sheet/04-utility-types.md:33-42]

```ts
type Permission = "read" | "write" | "delete";

const permissionLabels = {
  read: "Číst",
  write: "Upravovat",
  delete: "Mazat"
} satisfies Record<Permission, string>;
```

## Souvislosti

[[Typed dictionaries with Record|Record]] patří mezi utility typy, které odvozují nové typy z existujících a snižují duplicitu. Jejich použití by však nemělo skrýt důležitý business kontrakt. Před zavedením vlastního utility typu je vhodné zvážit standardní utility, indexed access nebo `satisfies`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-3, how-to/typescript-cheat-sheet/04-utility-types.md:77-79]

## Sources

- how-to/typescript-cheat-sheet/04-utility-types.md
