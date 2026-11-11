---
title: Generic Functions and Components
summary: Use generics when an algorithm, helper, or component needs to work with multiple types.
sources:
  - how-to/typescript-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:06:07.595Z"
updatedAt: "2026-11-11T11:06:07.595Z"
tags:
  - typescript
  - generics
  - reusability
aliases:
  - generic-functions-and-components
  - Components and Generic Functions
  - GFAC
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Generic Functions and Components

Generické funkce a komponenty patří mezi témata TypeScriptu pro typování funkcí, znovupoužitelných helperů a generic komponent. ^[how-to/typescript-cheat-sheet/README.md:11-12]

## Kdy zvažovat generika

Generika zvažuj tehdy, když se stejný algoritmus opakuje pro více typů. Rozhodovacím kritériem je tedy opakované použití algoritmu napříč typy. ^[how-to/typescript-cheat-sheet/README.md:30-34]

Při výběru typového nástroje rozlišuj účel: několik variant hodnoty řeší union s diskriminantem, odvození typu z existujícího typu řeší utility nebo indexed access type a změnu typu podle podmínky řeší conditional type. Souvisejí s tím [[Discriminated Unions]], [[Deriving Types with Utility Types and Indexed Access]] a [[Conditional Types]]. ^[how-to/typescript-cheat-sheet/README.md:32-36]

## Konvence zápisu

Ukázky funkcí mají používat `const` arrow functions a named exporty umístěné na konci ukázky. Typy se mají odvozovat ze schématu nebo jiného zdroje pravdy, aby se stejný tvar ručně neduplikoval na více místech; viz [[Single source of truth for type contracts]]. ^[how-to/typescript-cheat-sheet/README.md:24-27]

## Hranice typové kontroly

TypeScript kontroluje kód při buildu nebo v editoru, ale automaticky nevaliduje data přicházející za běhu z API, formuláře nebo localStorage. Pro externí hodnoty průvodce doporučuje začít s `unknown` a použít zúžení nebo runtime validaci. Tuto hranici rozebírají [[Unknown Versus Any]] a [[Compile-time typy versus runtime validace]]. ^[how-to/typescript-cheat-sheet/README.md:5-5, how-to/typescript-cheat-sheet/README.md:26-26, how-to/typescript-cheat-sheet/README.md:32-37]

## Sources

- [TypeScript Cheat Sheet](how-to/typescript-cheat-sheet/README.md)
