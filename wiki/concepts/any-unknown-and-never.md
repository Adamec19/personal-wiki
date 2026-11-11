---
title: any, unknown, and never
summary: Distinguish unchecked any, check-before-use unknown, and uninhabited never; prefer unknown at application boundaries and contain justified uses of any.
sources:
  - how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md
kind: concept
createdAt: "2026-11-11T11:05:28.643Z"
updatedAt: "2026-11-11T11:05:28.643Z"
tags:
  - typescript
  - type-safety
  - application-boundaries
aliases:
  - any-unknown-and-never
  - never and any, unknown,
  - AUAN
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# any, unknown, and never

Typy `any`, `unknown` a `never` vyjadřují odlišný přístup k hodnotám v TypeScriptu: `any` vypíná kontrolu hodnoty, `unknown` vyžaduje kontrolu před použitím a `never` představuje stav, kdy neexistuje žádná možná hodnota. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:51-55]

## `any`

U hodnoty typu `any` compiler přestává provádět typovou kontrolu. Pokud je jeho použití nutné, důvod má být zdokumentovaný a rozsah použití co nejmenší. Při review je vhodné kontrolovat, zda `any` neuniká do zbytku aplikace. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:53-57, how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:76-80]

## `unknown`

Typ `unknown` vyžaduje kontrolu hodnoty před jejím použitím a je preferovanou volbou na hranicích aplikace. Související porovnání rozebírá [[Unknown Versus Any]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:54-57]

Externí vstup je potřeba ověřit parserem, runtime schématem nebo skutečným type guardem. Type assertion, například `response as User`, data nezmění ani neověří. Toto rozlišení popisuje [[Runtime validation versus type assertions]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-33]

## `never`

Typ `never` vyjadřuje, že neexistuje žádná možná hodnota. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:51-55]

## Sources

- [Patterns and Pitfalls](how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md)
