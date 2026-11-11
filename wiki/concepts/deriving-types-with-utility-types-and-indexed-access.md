---
title: Deriving Types with Utility Types and Indexed Access
summary: Derive new types from existing types using utility types or indexed access instead of duplicating their structure.
sources:
  - how-to/typescript-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:06:09.365Z"
updatedAt: "2026-11-11T11:06:09.365Z"
tags:
  - typescript
  - utility-types
  - type-manipulation
aliases:
  - deriving-types-with-utility-types-and-indexed-access
  - Indexed Access and Deriving Types with Utility Types
  - DTWUTAIA
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Deriving Types with Utility Types and Indexed Access

Utility typy a indexed access types slouží k odvození nového typu z existujícího typu. Rozhodovací pravidlo je jednoduché: pokud potřebujete typ odvozený z jiného typu, použijte utility typ nebo indexed access type. ^[how-to/typescript-cheat-sheet/README.md:14-15, how-to/typescript-cheat-sheet/README.md:35-35]

## Jediný zdroj pravdy

Typy odvozujte ze schématu nebo jiného zdroje pravdy místo ručního duplikování stejného tvaru na více místech. Tento postup souvisí s principem [[Single source of truth for type contracts]]; pro formuláře je příbuzným tématem [[Schema-Derived Form Types]]. ^[how-to/typescript-cheat-sheet/README.md:27-27]

## Volba typového nástroje

Pro odvození z existujícího typu průvodce doporučuje utility typy nebo [[TypeScript Indexed Access Types]]. Pokud se má typ měnit podle podmínky, doporučuje [[Conditional Types|conditional type]] a současně upozorňuje na zachování čitelnosti. ^[how-to/typescript-cheat-sheet/README.md:35-36]

## Hranice typové kontroly

Odvozené typy jsou součástí kontroly kódu při buildu nebo v editoru. Automaticky nevalidují data přijatá z API, formuláře nebo localStorage. Pro externí hodnoty průvodce doporučuje začít s `unknown` a pro ověření za běhu použít runtime schéma nebo parser; viz [[Compile-time typy versus runtime validace]]. ^[how-to/typescript-cheat-sheet/README.md:5-5, how-to/typescript-cheat-sheet/README.md:32-37]

## Sources

- [TypeScript Cheat Sheet](how-to/typescript-cheat-sheet/README.md)
