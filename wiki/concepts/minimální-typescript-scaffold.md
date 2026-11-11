---
title: Minimální TypeScript scaffold
summary: Výchozí scaffold komponenty má obsahovat jen nezbytný základ, například typované props, jednoduché vykreslení a pojmenovaný export.
sources:
  - how-to/react-cheat-sheet/07-snippets-and-generators.md
kind: concept
createdAt: "2026-11-11T10:59:40.872Z"
updatedAt: "2026-11-11T10:59:40.872Z"
tags:
  - typescript
  - scaffolding
aliases:
  - minimální-typescript-scaffold
  - MTS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Minimální TypeScript scaffold

Minimální TypeScript scaffold je jednoduchý výchozí základ komponenty s typovanými props a explicitním exportem. Ukázka definuje `FeatureProps` s hodnotou `initialData` typu `FeatureData` a komponentu `Feature`, která vykresluje `initialData.title` v elementu `<section>`. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:48-60]

```tsx
type FeatureProps = {
  initialData: FeatureData;
};

const Feature = ({ initialData }: FeatureProps) => {
  return <section>{initialData.title}</section>;
};

export { Feature };
```

## Rozšiřování podle skutečných potřeb

Začíná se minimální verzí. Další abstrakce se přidávají až ve chvíli, kdy existují dva nebo tři skutečné případy použití; tento přístup rozvíjí [[Abstrakce podle skutečných use cases]]. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:62-62]

## Použití v šablonách

Malý, stabilní a často opakovaný kus kódu lze zachytit jako snippet, který nesmí skrývat rozhodnutí vyžadující ruční posouzení vývojáře. Pokud se opakuje více souborů a jejich vzájemná konfigurace, hodí se generátor. Jeho cílem je vytvořit konzistentní základ a ponechat prostor pro další vývoj. Související témata jsou [[Snippety pro opakovaný kód]] a [[Generátory struktury feature]]. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:3-28]

Po generování je potřeba provést [[Kontrola vygenerovaného kódu|kontrolu vygenerovaného kódu]]: ověřit cesty importů, názvy exportů, překlady a registraci rout, typy a lint i nepřítomnost zbylých placeholderů v produkčním kódu. ^[how-to/react-cheat-sheet/07-snippets-and-generators.md:40-46]

## Sources

- [Snippets and Generators](how-to/react-cheat-sheet/07-snippets-and-generators.md)
