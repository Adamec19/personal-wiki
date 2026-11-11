---
title: Checked Indexed Access
summary: Enable noUncheckedIndexedAccess so potentially missing array elements include undefined in their type and require appropriate handling.
sources:
  - how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md
kind: concept
createdAt: "2026-11-11T11:05:05.288Z"
updatedAt: "2026-11-11T11:05:05.288Z"
tags:
  - typescript
  - type-safety
  - arrays
aliases:
  - checked-indexed-access
  - CIA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Checked Indexed Access

Volba `noUncheckedIndexedAccess` v TypeScriptu zpřesňuje typovou kontrolu přístupu k prvkům pole pomocí indexu. Bez ní TypeScript často považuje `items[0]` za jistě existující prvek. Se zapnutou volbou má takový přístup typ `T | undefined`, takže je nutné zohlednit i prázdné pole. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:36-42]

## Konfigurace

`noUncheckedIndexedAccess` lze zapnout v `compilerOptions` společně s `strict: true`, jak ukazuje praktický základ [[TypeScript Project Configuration|konfigurace projektu]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:19-32]

```json
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true
  }
}
```

## Typ návratové hodnoty

Funkce vracející první prvek pole řetězců vyjadřuje možnou nepřítomnost prvku návratovým typem `string | undefined`. Volající tak musí při použití výsledku počítat s hodnotou `undefined`. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:38-42]

```ts
const first = (items: string[]): string | undefined => items[0];
```

## Souvislost se strict mode

[[TypeScript Strict Mode and Null Safety|Strict mode]] zapíná sadu kontrol, mezi nimiž má zásadní dopad `strictNullChecks`: hodnoty `null` a `undefined` přestávají být automaticky kompatibilní s každým typem. `noUncheckedIndexedAccess` doplňuje kontrolu indexovaného přístupu o možnost chybějícího prvku. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:5-15, how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:36-42]

## Sources

- [tsconfig and Project Setup](how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md)
