---
title: Memoization with useMemo and useCallback
summary: useMemo caches calculations and useCallback stabilizes function references when a concrete performance or identity requirement exists.
sources:
  - how-to/react-cheat-sheet/09-hooks-and-context.md
kind: concept
createdAt: "2026-11-11T11:00:31.538Z"
updatedAt: "2026-11-11T11:00:31.538Z"
tags:
  - react
  - memoization
  - performance
aliases:
  - memoization-with-usememo-and-usecallback
  - useCallback and Memoization with useMemo
  - MWUAU
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Memoization with useMemo and useCallback

React nabízí `useMemo` pro memoizaci výpočtu a `useCallback` pro memoizaci funkce. Jejich použití má mít konkrétní důvod: drahý výpočet nebo potřebu stabilní reference. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:88-111]

## `useMemo`: memoizace výpočtu

`useMemo` se hodí pro drahý výpočet nebo pro hodnotu, jejíž stabilní reference je důležitá. Následující příklad vytváří seřazenou kopii pole `items` a uvádí `items` jako závislost. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:88-97]

```tsx
const sortedItems = useMemo(
  () => [...items].sort(compareItems),
  [items]
);
```

Memoizace nemá být výchozí součástí každé proměnné. Nejdříve musí existovat skutečný důvod pro její použití. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:99-99]

## `useCallback`: memoizace funkce

`useCallback` memoizuje funkci především tehdy, když její identitu potřebuje memoizovaná child komponenta nebo když funkce slouží jako závislost jiného hooku. V příkladu je callback závislý na `removeItem`. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:101-109]

```tsx
const handleRemove = useCallback((id: string) => {
  removeItem(id);
}, [removeItem]);
```

Samotné použití `useCallback` neopraví špatně navržený state a nezrychlí automaticky každou komponentu. Související téma rozvádí [[Purposeful useCallback Usage]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:103-111]

## Souvislosti s renderem a efekty

Memoizované výpočty musí respektovat čistotu renderu: render nemá měnit DOM, volat API ani zapisovat do globálních proměnných. Tento princip popisuje [[React Hooks and Render Purity]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:5-21]

Pokud pouze počítáš hodnotu z props nebo state, nepotřebuješ k tomu effect. Pro drahý výpočet může být vhodný `useMemo`; `useEffect` slouží k synchronizaci s externím systémem. Viz také [[Odvozené hodnoty během renderu]] a [[External Synchronization with Effects]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:57-70, how-to/react-cheat-sheet/09-hooks-and-context.md:88-99]

Stejně jako ostatní hooks se `useMemo` a `useCallback` volají pouze na nejvyšší úrovni komponenty nebo custom hooku, nikoli v podmínkách, smyčkách či vnořených callbackách. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:3-3]

## Sources

- [Hooks and Context](how-to/react-cheat-sheet/09-hooks-and-context.md)
