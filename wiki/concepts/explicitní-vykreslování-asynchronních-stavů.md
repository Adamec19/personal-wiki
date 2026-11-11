---
title: Explicitní vykreslování asynchronních stavů
summary: Postupné podmíněné návraty rozlišují načítání, chybu, prázdná data a výsledky a zpřehledňují pořadí stavů.
sources:
  - how-to/react-cheat-sheet/10-component-snippets.md
kind: concept
createdAt: "2026-11-11T11:00:54.225Z"
updatedAt: "2026-11-11T11:00:54.225Z"
tags:
  - react
  - async-state
  - conditional-rendering
aliases:
  - explicitní-vykreslování-asynchronních-stavů
  - EVAS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Explicitní vykreslování asynchronních stavů

Asynchronní stavy komponenty lze vykreslovat pomocí samostatných podmínek s časným návratem. Ukázka postupně vyhodnocuje načítání, chybu a prázdný výsledek; seznam výsledků vykreslí až po těchto kontrolách. Explicitní pořadí stavů je čitelnější než mnoho vnořených ternárních výrazů. ^[how-to/react-cheat-sheet/10-component-snippets.md:98-108]

## Pořadí vykreslování

Podmínky určují prioritu jednotlivých stavů: při `isLoading` se zobrazí `Loading`, při chybě `ErrorMessage` a při chybějících datech nebo prázdném seznamu [[Komponenta prázdného stavu|EmptyState]]. Pokud žádná z podmínek neplatí, komponenta vrátí `ResultList`. ^[how-to/react-cheat-sheet/10-component-snippets.md:100-106]

```tsx
if (isLoading) return <Loading />;
if (error) return <ErrorMessage error={error} />;
if (!data?.length) return <EmptyState title="Nic nenalezeno" />;

return <ResultList items={data} />;
```

## Přizpůsobení aplikaci

Ukázka slouží jako výchozí kostra. Při použití je třeba přizpůsobit accessibility, design systému, zpracování chyb a datový kontrakt konkrétní aplikace. ^[how-to/react-cheat-sheet/10-component-snippets.md:3-3]

## Sources

- [Component Snippets](how-to/react-cheat-sheet/10-component-snippets.md)
