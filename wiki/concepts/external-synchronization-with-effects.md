---
title: External Synchronization with Effects
summary: useEffect synchronizes external systems; useLayoutEffect handles layout measurements or visual corrections before browser paint.
sources:
  - how-to/react-cheat-sheet/09-hooks-and-context.md
kind: concept
createdAt: "2026-11-11T11:00:18.640Z"
updatedAt: "2026-11-11T11:00:18.640Z"
tags:
  - react
  - effects
  - synchronization
aliases:
  - external-synchronization-with-effects
  - ESWE
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# External Synchronization with Effects

`useEffect` slouží k synchronizaci React komponenty s externím systémem, například se subscription, timerem, browser API, websocketem nebo imperativní knihovnou. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:57-59]

## Render a synchronizace

Render má zůstat čistý: nemá měnit DOM, volat API ani zapisovat do globálních proměnných. V popsaném modelu React po změně props, state nebo contextu zavolá komponentu, porovná její výstup s předchozím a aktualizuje DOM. Následně effect synchronizuje komponentu s externím systémem. Viz [[React Hooks and Render Purity]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:5-21]

## Příklad s cleanupem

Následující effect nastavuje titulek dokumentu podle hodnoty `title`, kterou uvádí v poli závislostí. Vrácená cleanup funkce nastaví titulek zpět na `"Aplikace"`. Souvisejícím tématem je [[Cleanup efektů]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:61-68]

```tsx
useEffect(() => {
  document.title = title;

  return () => {
    document.title = "Aplikace";
  };
}, [title]);
```

## Kdy effect nepotřebujete

Pokud pouze počítáte hodnotu z props nebo state, effect není potřeba. Taková hodnota patří mezi [[Odvozené hodnoty během renderu]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:70-70]

## Kdy použít `useLayoutEffect`

`useLayoutEffect` běží synchronně po změně DOM a před vykreslením browseru. Hodí se pro měření layoutu nebo vizuální opravu, která má zabránit viditelnému bliknutí. Pro síť, subscriptions a běžnou synchronizaci je vhodnější `useEffect`. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:115-117]

## Sources

- [Hooks and Context](how-to/react-cheat-sheet/09-hooks-and-context.md)
