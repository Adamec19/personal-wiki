---
title: TypeScript Types and Runtime Validation
summary: TypeScript checks code during development or builds; external data requires a runtime schema or parser, and types should be derived from that source of truth.
sources:
  - how-to/typescript-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:06:21.729Z"
updatedAt: "2026-11-11T11:06:21.729Z"
tags:
  - typescript
  - runtime-validation
aliases:
  - typescript-types-and-runtime-validation
  - Runtime Validation and TypeScript Types
  - TTARV
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Types and Runtime Validation

TypeScript kontroluje kód při buildu nebo v editoru. Data přicházející z API, formuláře nebo localStorage však automaticky za běhu nevaliduje. Compile-time typy a runtime validace proto představují odlišné úlohy. ^[how-to/typescript-cheat-sheet/README.md:5-5]

## Práce s externími daty

Pro hodnoty přicházející zvenčí je výchozím typem `unknown`. Před jejich použitím je potřeba data zúžit nebo validovat; `any` nemá sloužit jako zkratka, která tento krok obejde. Související témata jsou [[Unknown Versus Any]] a [[TypeScript Type Narrowing]]. ^[how-to/typescript-cheat-sheet/README.md:26-26, how-to/typescript-cheat-sheet/README.md:32-32]

Pokud je nutné ověřit data za běhu, samotný TypeScript nestačí: je potřeba runtime schema nebo parser. Toto rozlišení je podstatné při typování API, formulářů a dalších externích dat; dále jej rozvíjí [[Compile-time typy versus runtime validace]]. ^[how-to/typescript-cheat-sheet/README.md:16-16, how-to/typescript-cheat-sheet/README.md:37-37]

## Jediný zdroj typového kontraktu

Typy je vhodné odvozovat ze schématu nebo jiného zdroje pravdy, místo ručního duplikování stejného tvaru na více místech. Tento přístup souvisí s [[Single source of truth for type contracts]] a u formulářů se [[Schema-Derived Form Types]]. ^[how-to/typescript-cheat-sheet/README.md:27-27]

## Sources

- [TypeScript Cheat Sheet](how-to/typescript-cheat-sheet/README.md)
