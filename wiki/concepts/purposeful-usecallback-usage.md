---
title: Purposeful useCallback Usage
summary: Use useCallback when stable callback identity matters for a passed dependency, rather than applying it automatically.
sources:
  - how-to/react-cheat-sheet/02-components.md
kind: concept
createdAt: "2026-11-11T10:58:00.569Z"
updatedAt: "2026-11-11T10:58:00.569Z"
tags:
  - react
  - hooks
  - referential-stability
aliases:
  - purposeful-usecallback-usage
  - PUU
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Purposeful useCallback Usage

`useCallback` používej tehdy, když je potřeba stabilní identita předávané závislosti, nikoli automaticky pro každý callback. Rozhodnutí o jeho použití má vycházet z této konkrétní potřeby. ^[how-to/react-cheat-sheet/02-components.md:57-62]

## Umístění a pojmenování callbacků

Stabilní identita callbacku je samostatná otázka vedle jeho odpovědnosti. Callback má zůstat u komponenty, která vlastní rozhodnutí; business rozhodnutí nepatří do obecného Buttonu nebo Inputu. Tuto hranici rozvíjí [[Event Callbacks and Decision Ownership]]. ^[how-to/react-cheat-sheet/02-components.md:57-62]

Event handlery pojmenovávej podle akce, například `onSubmit`, `onRemove` nebo `onChange`. Jsou součástí veřejného API komponenty, jehož props mají být malé a explicitní; souvisejícím tématem je [[Component Props as a Public Contract]]. ^[how-to/react-cheat-sheet/02-components.md:3-5, how-to/react-cheat-sheet/02-components.md:57-62]

## Sources

- [Components](how-to/react-cheat-sheet/02-components.md)
