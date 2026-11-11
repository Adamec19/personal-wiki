---
title: Abstrakce podle skutečných use cases
summary: Další abstrakce se mají přidávat až na základě dvou nebo tří skutečných případů použití.
sources:
  - how-to/react-cheat-sheet/07-snippets-and-generators.md
kind: concept
createdAt: "2026-11-11T10:59:44.850Z"
updatedAt: "2026-11-11T10:59:44.850Z"
tags:
  - abstraction
  - software-design
aliases:
  - abstrakce-podle-skutečných-use-cases
  - APSUC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Abstrakce podle skutečných use cases

Při tvorbě základu komponenty začni minimální verzí. Další abstrakci přidávej až ve chvíli, kdy existují dva nebo tři skutečné případy použití, o které lze její návrh opřít. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:48-62]

## Volba mezi snippetem a generátorem

[[Snippety pro opakovaný kód]] se hodí pro malé, stabilní a často opakované části, například field wrapper, loading/error state, typovaný dialog hook nebo testovací setup. Snippet nemá skrývat rozhodnutí, která musí vývojář udělat ručně. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:3-13]

[[Generátory struktury feature]] použij, když se opakuje více souborů a jejich vzájemná konfigurace. Generátor má vytvořit konzistentní základ a ponechat prostor pro další vývoj. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:15-28]

## Kontrola výsledku

Při použití šablon udržuj [[Explicitní placeholdery v šablonách|placeholdery explicitní a snadno vyhledatelné]]. Po generování ověř importy, názvy exportů, překlady, registraci rout, typy a lint i to, že v produkčním kódu nezůstaly placeholdery. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:30-46]

## Sources

- [Snippets and Generators](how-to/react-cheat-sheet/07-snippets-and-generators.md)
