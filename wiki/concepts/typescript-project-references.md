---
title: TypeScript Project References
summary: Use project references for multiple independently built TypeScript projects; a single well-configured tsconfig is simpler for an ordinary application.
sources:
  - how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md
kind: concept
createdAt: "2026-11-11T11:05:12.473Z"
updatedAt: "2026-11-11T11:05:12.473Z"
tags:
  - typescript
  - builds
  - project-structure
aliases:
  - typescript-project-references
  - TPR
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# TypeScript Project References

Project references slouží pro situace, kdy máš více samostatně buildovaných TypeScript projektů. Pro běžnou aplikaci je jednodušší použít jeden dobře nastavený `tsconfig`. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:44-48]

## Kdy je použít

Rozhodujícím kritériem je potřeba samostatně buildovat více TypeScript projektů. Project references proto zaváděj až ve chvíli, kdy takové rozdělení potřebuješ; pro běžnou aplikaci upřednostni jednodušší [[TypeScript Project Configuration|konfiguraci projektu]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:48-48]

## Související nastavení

Při vymezení projektu určuje `include` jeho zdrojové soubory. `exclude` není bezpečnostní hranice: importovaný soubor se může do programu stále dostat. Podrobněji viz [[TypeScript File Inclusion and Exclusion]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:44-46]

Součástí ověřování projektu má být typová kontrola v CI, například příkazem `tsc --noEmit`. Lint a formatter řeší jinou vrstvu a nenahrazují TypeScript compiler; viz [[Type Checking in Continuous Integration]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:54-60]

## Sources

- [tsconfig and Project Setup](how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md)
