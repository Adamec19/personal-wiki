---
title: Compound components
summary: Vzor sdružuje související části komponenty se společným layoutem a ponechává obsah konzumentovi; pro nesouvisející části stačí běžná kompozice.
sources:
  - how-to/react-cheat-sheet/10-component-snippets.md
kind: concept
createdAt: "2026-11-11T11:00:46.254Z"
updatedAt: "2026-11-11T11:00:46.254Z"
tags:
  - react
  - composition
  - design-patterns
aliases:
  - compound-components
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Compound components

Compound components jsou vhodné pro komponentu, jejíž části sdílejí společný layout, zatímco konzument rozhoduje o jejich obsahu. Ukázkou je `Card` s přidruženými částmi `Card.Header` a `Card.Body`, které přijímají obsah přes `children`. ^[how-to/react-cheat-sheet/10-component-snippets.md:27-44]

## Typovaný příklad

`SlotProps` určuje společný kontrakt obsahu. Typ `CardComponent` propojuje samotnou komponentu s jejími částmi a `Object.assign` připojuje `Header` a `Body` ke komponentě `Card`. Výsledný tvar ověřuje operátor [[The satisfies operator|satisfies]]. ^[how-to/react-cheat-sheet/10-component-snippets.md:32-44]

```tsx
type SlotProps = { children: React.ReactNode };

type CardComponent = ((props: SlotProps) => React.ReactNode) & {
  Header: (props: SlotProps) => React.ReactNode;
  Body: (props: SlotProps) => React.ReactNode;
};

const Card = Object.assign(
  ({ children }: SlotProps) => <article className="card">{children}</article>,
  {
    Header: ({ children }: SlotProps) => <header>{children}</header>,
    Body: ({ children }: SlotProps) => <div>{children}</div>
  }
) satisfies CardComponent;
```

## Kdy vzor použít

Tento vzor používej pouze tehdy, když jednotlivé části opravdu patří k sobě. Jinak stačí [[Composition Through Children|kompozice přes children]] a běžné komponenty. ^[how-to/react-cheat-sheet/10-component-snippets.md:47-47]

Ukázka je výchozí kostra: je třeba ji přizpůsobit přístupnosti, design systému, zpracování chyb a datovému kontraktu konkrétní aplikace. Při návrhu pomáhá také [[Kontrolní seznam návrhu komponent]], který zahrnuje jeden účel komponenty, malý typovaný veřejný kontrakt a vyřešené ovládání klávesnicí i chování pro čtečky obrazovky. ^[how-to/react-cheat-sheet/10-component-snippets.md:3-3, how-to/react-cheat-sheet/10-component-snippets.md:128-135]

## Sources

- [Component Snippets](how-to/react-cheat-sheet/10-component-snippets.md)
