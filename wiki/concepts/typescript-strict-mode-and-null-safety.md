---
title: TypeScript Strict Mode and Null Safety
summary: Enable strict mode to catch problems early; strictNullChecks prevents null and undefined from being automatically compatible with every type.
sources:
  - how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md
kind: concept
createdAt: "2026-11-11T11:05:02.827Z"
updatedAt: "2026-11-11T11:05:02.827Z"
tags:
  - typescript
  - type-safety
  - configuration
aliases:
  - typescript-strict-mode-and-null-safety
  - Null Safety and TypeScript Strict Mode
  - TSMANS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Strict Mode and Null Safety

Režim `strict` zapíná sadu kontrol, které pomáhají odhalit problémy dříve. Doporučeným výchozím nastavením projektu je `strict: true`. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:3-13]

```json
{
  "compilerOptions": {
    "strict": true
  }
}
```

## Bezpečnost hodnot `null` a `undefined`

Nejdůležitějším dopadem striktního režimu je `strictNullChecks`: hodnoty `null` a `undefined` přestávají být automaticky kompatibilní s každým typem. Typová kontrola tak rozlišuje mezi běžnou hodnotou a její možnou nepřítomností. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:15-15]

## Bezpečný přístup do polí

Další kontrolu poskytuje samostatná volba `noUncheckedIndexedAccess`. Bez ní TypeScript často považuje `items[0]` za existující prvek. Po jejím zapnutí má takový přístup typ `T | undefined`, takže je nutné zohlednit i prázdné pole. Podrobněji viz [[Checked Indexed Access]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:36-42]

```ts
const first = (items: string[]): string | undefined => items[0];
```

## Nastavení a ověřování projektu

Striktní kontroly patří do širšího [[TypeScript Project Configuration|nastavení TypeScript projektu]]. Volby `target`, `module` a `moduleResolution` musí odpovídat používanému runtime a bundleru; konfiguraci není vhodné kopírovat bez pochopení prostředí. Vypnutí kontrol pomocí `strict: false` nemá sloužit k plošnému potlačení chyb. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:19-34, how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:62-67]

Typovou kontrolu lze spustit příkazem `tsc --noEmit` a měla by běžet také v CI, viz [[Type Checking in Continuous Integration]]. Lint ani formatter nenahrazují TypeScript compiler, protože řeší jinou vrstvu kontroly. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:54-60]

## Sources

- [tsconfig and Project Setup](how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md)
