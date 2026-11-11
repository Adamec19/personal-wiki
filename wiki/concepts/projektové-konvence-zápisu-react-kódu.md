---
title: Projektové konvence zápisu React kódu
summary: Ukázky používají const arrow functions pro komponenty a custom hooks a pojmenované exporty na konci souboru; jde o přizpůsobitelné projektové konvence.
sources:
  - how-to/react-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:01:20.313Z"
updatedAt: "2026-11-11T11:01:20.313Z"
tags:
  - react
  - konvence
  - styl-kodu
aliases:
  - projektové-konvence-zápisu-react-kódu
  - PKZRK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Projektové konvence zápisu React kódu

Projektové konvence určují jednotný styl zápisu v konkrétním codebase. Je potřeba je odlišovat od obecných React principů a přizpůsobit danému projektu. ^[how-to/react-cheat-sheet/README.md:3-5]

## Komponenty, hooks a exporty

Ukázky v React Cheat Sheet zapisují komponenty a [[custom-hooks|Custom Hooks]] jako `const` arrow functions. Používají pojmenované exporty umístěné na konci souboru. Tento styl sjednocuje také všechny snippets v dané složce. ^[how-to/react-cheat-sheet/README.md:35-59]

```tsx
type EmptyStateProps = {
  title: string;
  description?: string;
  action?: React.ReactNode;
};

const EmptyState = ({ title, description, action }: EmptyStateProps) => {
  return (
    <section aria-labelledby="empty-state-title">
      <h2 id="empty-state-title">{title}</h2>
      {description && <p>{description}</p>}
      {action}
    </section>
  );
};

export { EmptyState };
```

Ukázka komponenty [[Komponenta prázdného stavu|EmptyState]] předvádí tuto konvenci včetně typu props a pojmenovaného exportu. Stejný způsob deklarace se používá také pro [[Custom Hooks|custom hooks]]. ^[how-to/react-cheat-sheet/README.md:37-57]

## Pomocné funkce a snippets

Běžné pomocné funkce mohou mít vlastní konvenci podle konkrétního projektu. Ukázky však i pro ně preferují arrow-function zápis kvůli konzistenci. Opakující se strukturu souborů a pravidel lze zachytit pomocí [[Snippets a generátory|snippetů a generátorů]]. ^[how-to/react-cheat-sheet/README.md:29-29, how-to/react-cheat-sheet/README.md:59-59]

## Sources

- [React Cheat Sheet](how-to/react-cheat-sheet/README.md)
