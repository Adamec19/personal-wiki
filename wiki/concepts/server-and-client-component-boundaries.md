---
title: Server and client component boundaries
summary: "Keep client boundaries deep in the component tree: server components load data and compose pages, while client components handle interactivity and browser APIs."
sources:
  - how-to/react-cheat-sheet/01-architecture.md
kind: concept
createdAt: "2026-11-11T10:57:47.325Z"
updatedAt: "2026-11-11T10:57:47.325Z"
tags:
  - server-components
  - client-components
  - architecture
aliases:
  - server-and-client-component-boundaries
  - client component boundaries and Server
  - SACCB
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Server and client component boundaries

Hranice mezi serverovými a klientskými komponentami rozděluje přípravu dat a skládání stránky od interaktivity. Ve frameworku, který toto rozdělení podporuje, má být klientská hranice co nejhlouběji v komponentovém stromu, pouze tam, kde je interaktivita potřeba. ^[how-to/react-cheat-sheet/01-architecture.md:33-39,58-64]

## Rozdělení odpovědností

Serverová komponenta připravuje data a skládá stránku. Klientská komponenta vlastní interaktivitu, obsluhu událostí a práci s browser API. Direktivu `"use client"` proto nepřidávej automaticky do celé feature; umísti ji do komponenty, která klientské chování potřebuje. Toto rozdělení lze uplatnit v rámci [[Feature-based code organization|organizace kódu podle feature]]. ^[how-to/react-cheat-sheet/01-architecture.md:3-21,33-39]

## Příklad předání dat

V následujícím příkladu serverová komponenta `Page` načte data a předá je komponentě `InteractivePanel` přes prop `initialData`. Direktiva `"use client"` je umístěna až v souboru panelu. ^[how-to/react-cheat-sheet/01-architecture.md:41-56]

```tsx
// page.tsx
export default async function Page() {
  const data = await loadData();
  return <InteractivePanel initialData={data} />;
}

// interactive-panel.tsx
"use client";

const InteractivePanel = ({ initialData }: Props) => {
  return <section>{initialData.title}</section>;
};

export { InteractivePanel };
```

## Kontrola návrhu

Při kontrole ověř, že klientská hranice zahrnuje pouze místa vyžadující interaktivitu a každý modul má jasnou odpovědnost. Souvisejícími hledisky jsou [[Separation of business logic from routing|oddělení business logiky od routování]] a [[Independent feature testability|samostatná testovatelnost feature]]. ^[how-to/react-cheat-sheet/01-architecture.md:58-64]

## Sources

- [Architecture](how-to/react-cheat-sheet/01-architecture.md)
