---
title: React Hooks and Render Purity
summary: Hooks must be called at the top level of components or custom hooks, and rendering must remain free of side effects.
sources:
  - how-to/react-cheat-sheet/09-hooks-and-context.md
kind: concept
createdAt: "2026-11-11T11:00:21.620Z"
updatedAt: "2026-11-11T11:00:21.620Z"
tags:
  - react
  - hooks
  - rendering
aliases:
  - react-hooks-and-render-purity
  - Render Purity and React Hooks
  - RHARP
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# React Hooks and Render Purity

Hooks jsou funkce, které připojují komponentu ke konkrétní schopnosti Reactu. Volají se pouze na nejvyšší úrovni komponenty nebo custom hooku, nikoli v podmínkách, smyčkách nebo vnořených callbackách. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:3-3]

## Mentální model renderu

Změna props, state nebo contextu vede k zavolání komponenty, která vrátí JSX. React porovná nový výstup s předchozím a aktualizuje DOM. Následně effect synchronizuje komponentu s externím systémem. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:7-19]

Render má být čistý: nesmí přímo měnit DOM, volat API ani zapisovat do globálních proměnných. Synchronizaci s prostředím mimo React zajišťují efekty. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:21-21, how-to/react-cheat-sheet/09-hooks-and-context.md:57-59]

## Stav a odvozené hodnoty

Pro lokální hodnoty ovlivňující UI slouží `useState`. Aktualizace stavu je žádost o nový render, nikoli okamžitá změna aktuální proměnné. Pokud nová hodnota závisí na předchozí, použije se funkční updater. Složitější přechody lze centralizovat pomocí `useReducer`; samotný reducer nemá volat API ani měnit externí systém. Viz [[State Management with useState and useReducer]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:23-55]

Hodnotu, kterou lze pouze vypočítat z props nebo state, není potřeba synchronizovat efektem. Patří mezi [[Odvozené hodnoty během renderu]]. Pro drahý výpočet nebo důležitou stabilní referenci lze použít `useMemo`, ale jeho použití má mít konkrétní důvod. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:70-70, how-to/react-cheat-sheet/09-hooks-and-context.md:88-99]

## Synchronizace s externím systémem

`useEffect` slouží pro subscriptions, časovače, browser API, websockety nebo imperativní knihovny. Následující příklad aktualizuje titulek dokumentu a vrací funkci pro [[Cleanup efektů]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:57-68]

```tsx
useEffect(() => {
  document.title = title;
  return () => {
    document.title = "Aplikace";
  };
}, [title]);
```

`useLayoutEffect` běží synchronně po změně DOM a před vykreslením prohlížečem. Hodí se pro měření layoutu nebo vizuální opravu zabraňující bliknutí. Pro síťové operace, subscriptions a běžnou [[External Synchronization with Effects|synchronizaci s externím systémem]] se preferuje `useEffect`. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:115-117]

## Reference a sdílení logiky

`useRef` uchovává hodnotu mezi rendery, aniž její změna vyvolá nový render. Používá se například pro DOM uzel, identifikátor časovače nebo předchozí hodnotu. Pokud se změna musí projevit v UI, má být uložena ve state. Viz [[Persistent Mutable References with useRef]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:72-86]

[[Custom Hooks]] umožňují sdílet logiku, nikoli jednu společnou instanci stavu. Každá komponenta, která custom hook zavolá, má vlastní hook state. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:182-195]

## Sources

- [Hooks and Context](how-to/react-cheat-sheet/09-hooks-and-context.md)
