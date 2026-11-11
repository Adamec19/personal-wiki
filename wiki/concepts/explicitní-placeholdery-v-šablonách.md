---
title: Explicitní placeholdery v šablonách
summary: Placeholdery v šablonách mají být explicitní a snadno vyhledatelné, například {{FEATURE_NAME}} nebo {{API_RESOURCE}}.
sources:
  - how-to/react-cheat-sheet/07-snippets-and-generators.md
kind: concept
createdAt: "2026-11-11T10:59:34.722Z"
updatedAt: "2026-11-11T10:59:34.722Z"
tags:
  - templates
  - placeholders
aliases:
  - explicitní-placeholdery-v-šablonách
  - EPVŠ
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Explicitní placeholdery v šablonách

Placeholdery v šablonách mají být explicitní a snadno vyhledatelné. Zdroj uvádí zápis s dvojitými složenými závorkami, například `{{FEATURE_NAME}}`, `{{FEATURE_TITLE}}` a `{{API_RESOURCE}}`. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:30-38]

## Použití v generátorech

[[Generátory struktury feature]] se hodí pro opakované vytváření více souborů a jejich vzájemné konfigurace. Mají poskytnout konzistentní základ a ponechat prostor pro další vývoj. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:15-28]

## Kontrola po generování

Součástí [[Kontrola vygenerovaného kódu|kontroly vygenerovaného kódu]] je ověření importních cest, názvů exportů, překladů, registrace rout, typů a lintu. Vždy je také potřeba zkontrolovat, že v produkčním kódu nezůstaly žádné placeholdery. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:40-46]

## Sources

- how-to/react-cheat-sheet/07-snippets-and-generators.md
