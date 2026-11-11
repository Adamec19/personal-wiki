---
title: Generátory struktury feature
summary: Generator vytváří konzistentní základ opakující se struktury více souborů a jejich konfigurace, přičemž zachovává volnost dalšího vývoje.
sources:
  - how-to/react-cheat-sheet/07-snippets-and-generators.md
kind: concept
createdAt: "2026-11-11T10:59:32.434Z"
updatedAt: "2026-11-11T10:59:32.434Z"
tags:
  - generators
  - scaffolding
aliases:
  - generátory-struktury-feature
  - GSF
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Generátory struktury feature

Generátor struktury feature se hodí tehdy, když se opakuje více souborů a jejich vzájemná konfigurace. Oproti [[Snippety pro opakovaný kód|snippetům]] pro malé, stabilní kusy kódu vytváří základ celé feature. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:5-17]

## Struktura a rozsah

Generátor může vytvořit následující adresářovou strukturu. Jeho cílem je zajistit konzistentní základ, který ponechává prostor pro další vývoj. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:17-28]

```text
feature-name/
├── components/
├── hooks/
├── models/schema.ts
├── services/api/
└── page.tsx
```

Začínat je vhodné minimální verzí. Další abstrakce mají vznikat až na základě dvou nebo tří skutečných případů použití; viz [[Abstrakce podle skutečných use cases]]. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:62-62]

## Placeholdery a kontrola výstupu

Šablony mají používat [[Explicitní placeholdery v šablonách|explicitní a snadno vyhledatelné placeholdery]], například `{{FEATURE_NAME}}`, `{{FEATURE_TITLE}}` nebo `{{API_RESOURCE}}`. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:30-38]

Po generování je vždy nutná [[Kontrola vygenerovaného kódu]]: ověřit import paths, názvy exportů, překlady, registraci rout, typy a lint. Součástí kontroly je také ověření, že v produkčním kódu nezůstaly žádné placeholdery. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:40-46]

## Sources

- [Snippets and Generators](how-to/react-cheat-sheet/07-snippets-and-generators.md)
