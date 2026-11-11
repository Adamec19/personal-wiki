---
title: Kontrola vygenerovaného kódu
summary: Po generování je nutné ověřit importy, exporty, překlady, registraci rout, typy, lint a nepřítomnost nevyplněných placeholderů.
sources:
  - how-to/react-cheat-sheet/07-snippets-and-generators.md
kind: concept
createdAt: "2026-11-11T10:59:40.284Z"
updatedAt: "2026-11-11T10:59:40.284Z"
tags:
  - code-generation
  - validation
aliases:
  - kontrola-vygenerovaného-kódu
  - KVK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Kontrola vygenerovaného kódu

Po generování kódu je potřeba ověřit jeho zapojení do projektu, typy a lint i odstranění zbylých placeholderů. Kontrola zahrnuje import paths, názvy exportů, překlady a registraci rout. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:40-46]

## Co ověřit

Při kontrole projdi následující oblasti: ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:40-46]

- **Import paths:** ověř cesty v importech.
- **Exporty:** zkontroluj názvy exportů.
- **Překlady a routy:** ověř překlady a registraci rout.
- **Typy a lint:** proveď typovou a lintovou kontrolu.
- **Placeholdery:** ověř, že v produkčním kódu nezůstaly nevyplněné značky ze šablony.

## Placeholdery a rozsah generování

[[Explicitní placeholdery v šablonách]] mají být snadno vyhledatelné, například `{{FEATURE_NAME}}`, `{{FEATURE_TITLE}}` nebo `{{API_RESOURCE}}`. Po generování je nutné ověřit, že žádné nezůstaly v produkčním kódu. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:30-46]

[[Generátory struktury feature]] mají vytvářet konzistentní základ a ponechat prostor pro další vývoj. Ani snippet nemá skrývat rozhodnutí, která musí vývojář udělat ručně. Výchozí kód má zůstat minimální; další abstrakce se přidávají až na základě dvou nebo tří skutečných případů použití. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:13-28, how-to/react-cheat-sheet/07-snippets-and-generators.md:62-62]

## Sources

- [Snippets and Generators](how-to/react-cheat-sheet/07-snippets-and-generators.md)
