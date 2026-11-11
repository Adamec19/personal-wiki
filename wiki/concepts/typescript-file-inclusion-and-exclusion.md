---
title: TypeScript File Inclusion and Exclusion
summary: include selects project source files, while exclude does not prevent imported files from entering the TypeScript program.
sources:
  - how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md
kind: concept
createdAt: "2026-11-11T11:05:03.109Z"
updatedAt: "2026-11-11T11:05:03.109Z"
tags:
  - typescript
  - configuration
  - project-structure
aliases:
  - typescript-file-inclusion-and-exclusion
  - Exclusion and TypeScript File Inclusion
  - TFIAE
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript File Inclusion and Exclusion

Nastavení `include` v `tsconfig` určuje zdrojové soubory projektu. `exclude` však není bezpečnostní hranice: importovaný soubor se může do programu stále dostat, i když je vyloučený. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:44-46]

## Hranice projektu

Pro běžnou aplikaci je jednodušší jeden dobře nastavený `tsconfig`. [[TypeScript Project References|Project references]] mají smysl až ve chvíli, kdy existuje více samostatně buildovaných TypeScript projektů. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:44-48]

## Ověření konfigurace

Typovou kontrolu lze spustit příkazem `tsc --noEmit`; měla by běžet také v CI. Lint a formatter řeší jinou vrstvu a nenahrazují TypeScript compiler. Viz také [[Type Checking in Continuous Integration]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:54-60]

## Sources

- [tsconfig and Project Setup](how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md)
