---
title: Návrh znovupoužitelných komponent
summary: Znovupoužitelná komponenta má být jednoduchá na použití a nemá znát business pravidla svého konzumenta.
sources:
  - how-to/react-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:01:12.171Z"
updatedAt: "2026-11-11T11:01:12.171Z"
tags:
  - react
  - komponenty
aliases:
  - návrh-znovupoužitelných-komponent
  - NZK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Návrh znovupoužitelných komponent

Návrh znovupoužitelných komponent začíná vymezením hranic a datového toku; abstrakce přicházejí až potom. Komponenta má být jednoduchá na použití a nemá znát business pravidla svého konzumenta. S tím souvisí [[Hranice a datový tok v React aplikaci]] a [[Oddělení business logiky od generického UI]]. ^[how-to/react-cheat-sheet/README.md:31-33]

## Rozhodování o odpovědnosti

Pro čistě vizuální prvek je výchozím řešením komponenta. Stav jedné obrazovky patří do lokálního state; pokud jej sdílí více vzdálených částí aplikace, lze zvážit context nebo store. Hodnoty odvoditelné z props či state se počítají během renderu. `useEffect` slouží k synchronizaci s externím systémem. Tato rozhodnutí souvisejí s tématy [[Lokální a sdílený stav]] a [[Odvozené hodnoty během renderu]]. ^[how-to/react-cheat-sheet/README.md:24-28]

## Příklad: [[komponenta-prázdného-stavu|Komponenta prázdného stavu]]

Ukázková [[Komponenta prázdného stavu|komponenta prázdného stavu]] přijímá povinný `title`, volitelný `description` a volitelný `action` typu `React.ReactNode`. Vykresluje sekci s nadpisem, případným popisem a předanou akcí. Konzument tak dodává obsah prostřednictvím props. ^[how-to/react-cheat-sheet/README.md:40-54]

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

## Projektové konvence

Obecné React principy je potřeba odlišovat od projektových konvencí. Zdrojové ukázky používají pro komponenty a [[custom-hooks|Custom Hooks]] `const` arrow functions a pojmenované exporty na konci souboru; tyto konvence je třeba přizpůsobit konkrétnímu codebase. Viz [[Projektové konvence zápisu React kódu]]. ^[how-to/react-cheat-sheet/README.md:5-5, how-to/react-cheat-sheet/README.md:35-59]

Pokud se opakuje struktura souborů a pravidel, lze přidat [[Snippets a generátory|snippet nebo generátor]]. ^[how-to/react-cheat-sheet/README.md:29-29]

## Sources

- [React Cheat Sheet](how-to/react-cheat-sheet/README.md)
