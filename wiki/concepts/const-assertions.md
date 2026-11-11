---
title: Const Assertions
summary: The as const assertion preserves literal types and readonly properties, enabling unions derived from constant tuples.
sources:
  - how-to/typescript-cheat-sheet/01-type-system-basics.md
kind: concept
createdAt: "2026-11-11T11:02:58.328Z"
updatedAt: "2026-11-11T11:02:58.328Z"
tags:
  - typescript
  - const-assertions
  - literal-types
aliases:
  - const-assertions
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Const Assertions

Const assertion pomocí `as const` zachovává přesné literálové typy a readonly vlastnosti. Bez ní TypeScript často rozšíří typ hodnoty na obecný `string` nebo `number`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:92-99]

## Odvození typu z hodnot

Pomocí `as const` lze zachovat konkrétní hodnoty v poli a následně z nich odvodit typ přes [[TypeScript Indexed Access Types|indexed access]]. V příkladu níže odpovídá `Direction` typu `"up" | "down" | "left" | "right"`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:94-99]

```ts
const DIRECTIONS = ["up", "down", "left", "right"] as const;
type Direction = (typeof DIRECTIONS)[number];
```

Takto odvozený [[Union and Literal Types|union literálů]] vyjadřuje jednu z povolených variant a je přesnější než obecný `string`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:41-49, how-to/typescript-cheat-sheet/01-type-system-basics.md:94-99]

## Sources

- [Type System Basics](how-to/typescript-cheat-sheet/01-type-system-basics.md)
