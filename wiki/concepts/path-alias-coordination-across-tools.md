---
title: Path Alias Coordination Across Tools
summary: Coordinate TypeScript path aliases with the bundler, test runner, and editor tooling because tsconfig aliases alone do not change runtime resolution.
sources:
  - how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md
kind: concept
createdAt: "2026-11-11T11:05:15.543Z"
updatedAt: "2026-11-11T11:05:15.543Z"
tags:
  - typescript
  - module-resolution
  - tooling
aliases:
  - path-alias-coordination-across-tools
  - PACAT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Path Alias Coordination Across Tools

Path aliasy je potřeba nastavit společně v TypeScriptu, bundleru, test runneru a nástrojích editoru. Samotný alias v `tsconfig` nemění způsob, jakým se importy vyhodnocují za běhu. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:50-52]

## Koordinace konfigurace

Při nastavování aliasů v rámci [[TypeScript Project Configuration]] zohledni konfiguraci bundleru i testů. Aliasy bez odpovídající konfigurace těchto nástrojů patří mezi postupy, kterým je vhodné se vyhnout. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:50-52, how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:62-67]

Také volby `target`, `module` a `moduleResolution` musí odpovídat runtime a bundleru. Konfiguraci proto nekopíruj bez pochopení prostředí; souvisejícím tématem je [[Runtime-Aligned TypeScript Configuration]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:19-34]

## Ověření

Typovou kontrolu lze spustit příkazem `tsc --noEmit` a měla by běžet také v CI, viz [[Type Checking in Continuous Integration]]. Její výsledek je však třeba posuzovat s vědomím, že alias v `tsconfig` sám nemění runtime resolution. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:50-60]

## Sources

- [tsconfig and Project Setup](how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md)
