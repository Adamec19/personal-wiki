---
title: Conditional Types
summary: Use conditional types when a resulting type depends on a condition, while keeping the type definition readable.
sources:
  - how-to/typescript-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:06:15.697Z"
updatedAt: "2026-11-11T11:06:15.697Z"
tags:
  - typescript
  - conditional-types
  - readability
aliases:
  - conditional-types
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Conditional Types

Conditional types v TypeScriptu slouží ke změně typu podle podmínky. Jsou vhodné, když odvození výsledného typu vyžaduje podmíněné rozhodování; při jejich použití je potřeba hlídat čitelnost. ^[how-to/typescript-cheat-sheet/README.md:30-37]

## Kdy je použít

Volba typového nástroje závisí na zamýšlené operaci. Pro odvození typu z existujícího typu průvodce doporučuje utility types nebo [[TypeScript Indexed Access Types|indexed access types]]. Pokud se má typ měnit podle podmínky, doporučuje conditional type. ^[how-to/typescript-cheat-sheet/README.md:35-36]

## Hranice použití

Conditional types patří do typové kontroly při buildu nebo v editoru. Nenahrazují [[Compile-time typy versus runtime validace|runtime validaci]] dat z API, formulářů či localStorage. Pro ověření dat za běhu je potřeba runtime schema nebo parser. ^[how-to/typescript-cheat-sheet/README.md:5-5, how-to/typescript-cheat-sheet/README.md:37-37]

## Sources

- [TypeScript Cheat Sheet](how-to/typescript-cheat-sheet/README.md)
