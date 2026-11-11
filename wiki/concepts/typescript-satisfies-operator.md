---
title: TypeScript satisfies Operator
summary: Validate a value against a target type while preserving its specific inferred type, including concrete keys and literals in the shown as const pattern.
sources:
  - how-to/typescript-cheat-sheet/05-advanced-types.md
kind: concept
createdAt: "2026-11-11T11:04:31.163Z"
updatedAt: "2026-11-11T11:04:31.163Z"
tags:
  - typescript
  - type-inference
  - type-checking
aliases:
  - typescript-satisfies-operator
  - TSO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript satisfies Operator

Operátor `satisfies` ověřuje, že hodnota odpovídá požadovanému typu, a přitom zachovává její konkrétní odvozený typ. Umožňuje tak kontrolovat strukturu hodnoty bez ztráty přesnějších typových informací. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:69-84]

## Použití s `as const` a `Record`

Následující konfigurace kombinuje [[Const Assertions|as const]] a `satisfies Record<string, Route>`. Každá položka musí odpovídat typu `Route`, zatímco výsledný typ zachovává konkrétní klíče a literální hodnoty. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:71-84]

```ts
type Route = { title: string; authRequired: boolean };

const routes = {
  home: { title: "Domů", authRequired: false },
  account: { title: "Účet", authRequired: true }
} as const satisfies Record<string, Route>;

const accountTitle = routes.account.title;
```

## Rozdíl oproti typové anotaci

Při anotaci `const routes: Record<string, Route>` se nezachovají konkrétní klíče a literály stejně jako v uvedené kombinaci `as const satisfies`. Ta proto umožňuje ověřit společný tvar položek a současně zachovat přesné informace o konfiguraci. Související použití popisují [[Record v kombinaci se satisfies]] a [[Configuration Objects with as const satisfies]]. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:71-84]

## Sources

- how-to/typescript-cheat-sheet/05-advanced-types.md
