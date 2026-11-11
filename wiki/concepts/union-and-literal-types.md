---
title: Union and Literal Types
summary: Unions of literal types constrain values to specific permitted alternatives more precisely than broad primitive types.
sources:
  - how-to/typescript-cheat-sheet/01-type-system-basics.md
kind: concept
createdAt: "2026-11-11T11:02:51.171Z"
updatedAt: "2026-11-11T11:02:51.171Z"
tags:
  - typescript
  - union-types
  - literal-types
aliases:
  - union-and-literal-types
  - Literal Types and Union
  - UALT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Union and Literal Types

Union typ vyjadřuje „jednu z povolených variant“. Spojením konkrétních literálů lze omezit hodnotu na přesně vymezené možnosti, což je přesnější než obecný `string`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:41-49]

## Příklad

Typ `Status` povoluje čtyři řetězcové literály. Proměnná `status` má explicitně tento typ a obsahuje jednu z povolených hodnot. Pro definici union typů je vhodný [[Type Aliases and Interfaces|typový alias `type`]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:35-47]

```ts
type Status = "idle" | "loading" | "success" | "error";

const status: Status = "loading";
```

## Zachování literálů pomocí `as const`

Bez `as const` TypeScript často rozšíří hodnotu na obecný `string` nebo `number`. [[Const Assertions|`as const`]] zachová přesné literály a readonly vlastnosti. Následující příklad odvozuje typ `Direction` z hodnot pole pomocí [[TypeScript Indexed Access Types|indexed access typu]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:92-99]

```ts
const DIRECTIONS = ["up", "down", "left", "right"] as const;
type Direction = (typeof DIRECTIONS)[number];
```

## Praktické použití

Při návrhu typu zvaž, zda hodnota může být libovolný `string`, nebo má patřit do omezeného unionu literálů. Explicitní anotace pomáhá tam, kde dokumentuje kontrakt, chrání veřejné API nebo podporuje [[TypeScript Type Narrowing|narrowing]]; v ostatních případech lze obvykle nechat pracovat [[Type Inference and Explicit Annotations|typovou inferenci]]. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:13-20, how-to/typescript-cheat-sheet/01-type-system-basics.md:101-106]

## Sources

- [Type System Basics](how-to/typescript-cheat-sheet/01-type-system-basics.md)
