---
title: Unknown Versus Any
summary: Unknown requires narrowing before use, while any disables type checking and should be isolated to unavoidable boundaries.
sources:
  - how-to/typescript-cheat-sheet/01-type-system-basics.md
kind: concept
createdAt: "2026-11-11T11:02:56.807Z"
updatedAt: "2026-11-11T11:02:56.807Z"
tags:
  - typescript
  - type-safety
  - type-narrowing
aliases:
  - unknown-versus-any
  - UVA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Unknown Versus Any

`unknown` a `any` se liší tím, jak zacházejí s typovou kontrolou. `unknown` je bezpečný typ pro data, kterým zatím nevěříme: před použitím je nutné jejich typ zúžit. `any` typovou kontrolu vypíná a přenáší případnou chybu dál. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:62-76]

## Použití `unknown`

Externí vstup má být nejprve reprezentován jako `unknown` a následně validován. Při práci s takovou hodnotou lze využít [[TypeScript Type Narrowing|zužování typů]], například kontrolu `typeof`, vyloučení `null` a ověření přítomnosti vlastnosti pomocí `in`. Pro ověření přesného kontraktu slouží schéma nebo [[Object type guards|type guard]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:64-74, how-to/typescript-cheat-sheet/01-type-system-basics.md:106-106]

```ts
const parseJson = (value: string): unknown => JSON.parse(value);

const data = parseJson('{"name":"Ada"}');

if (typeof data === "object" && data !== null && "name" in data) {
  // Use a schema or type guard for the exact contract.
}
```

Ukázka vrací výsledek parsování JSON jako `unknown` a před další prací kontroluje, zda jde o nenulový objekt s vlastností `name`. Přesný kontrakt vyžaduje další ověření. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:66-74]

## Použití `any`

`any` má být omezeno na skutečně nevyhnutelnou hranici a izolováno. Nemá sloužit jako prostředek k obejití typového problému, protože vypíná typovou kontrolu. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:76-76, how-to/typescript-cheat-sheet/01-type-system-basics.md:105-105]

## Sources

- [Type System Basics](how-to/typescript-cheat-sheet/01-type-system-basics.md)
