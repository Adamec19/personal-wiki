---
title: TypeScript Template Literal Types
summary: Construct string types from literal combinations to model event names, route patterns, and configuration keys.
sources:
  - how-to/typescript-cheat-sheet/05-advanced-types.md
kind: concept
createdAt: "2026-11-11T11:04:25.879Z"
updatedAt: "2026-11-11T11:04:25.879Z"
tags:
  - typescript
  - literal-types
aliases:
  - typescript-template-literal-types
  - TTLT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Template Literal Types

Template literal types skládají řetězcové typy pomocí zápisu s backticky a interpolací `${...}`. V následujícím příkladu typ `EventName` kombinuje členy [[Union and Literal Types|union typu]] `Entity` s příponami `:created` a `:updated`. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:58-65]

```ts
type Entity = "user" | "order";
type EventName = `${Entity}:created` | `${Entity}:updated`;

const eventName: EventName = "user:created";
```

Výsledný typ připouští hodnoty `"user:created"`, `"order:created"`, `"user:updated"` a `"order:updated"`. Template literal types se hodí pro typování názvů událostí, vzorů cest nebo konfiguračních klíčů. ^[how-to/typescript-cheat-sheet/05-advanced-types.md:60-67]

## Sources

- how-to/typescript-cheat-sheet/05-advanced-types.md
