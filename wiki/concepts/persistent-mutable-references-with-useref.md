---
title: Persistent Mutable References with useRef
summary: useRef retains mutable values across renders without triggering rendering, making it suitable for DOM references and timer identifiers.
sources:
  - how-to/react-cheat-sheet/09-hooks-and-context.md
kind: concept
createdAt: "2026-11-11T11:00:21.051Z"
updatedAt: "2026-11-11T11:00:21.051Z"
tags:
  - react
  - hooks
  - references
aliases:
  - persistent-mutable-references-with-useref
  - PMRWU
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Persistent Mutable References with useRef

`useRef` uchovává hodnotu, která má přežít render komponenty, ale jejíž změna nemá vyvolat nový render. Typickými příklady jsou reference na DOM node, ID časovače nebo předchozí hodnota. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:72-74]

## Reference na DOM element

Reference vytvořená pomocí `useRef` může být připojena k inputu přes atribut `ref`. Obsluha pak přistupuje k elementu přes `inputRef.current` a může zavolat jeho metodu `focus()`. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:76-84]

```tsx
const inputRef = useRef<HTMLInputElement>(null);

const focusInput = () => {
  inputRef.current?.focus();
};

return <input ref={inputRef} />;
```

## Kdy použít ref a kdy state

Ref nemá nahrazovat state. Pokud se změna hodnoty musí projevit v UI, použije se [[State Management with useState and useReducer|state]]. `useRef` je vhodný pro mutable referenci, jejíž změna nový render nevyžaduje. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:74-86]

## Pravidla použití

Stejně jako ostatní hooks se `useRef` volá pouze na nejvyšší úrovni komponenty nebo custom hooku, nikoli v podmínce, smyčce nebo vnořeném callbacku. Render má zůstat čistý a nemá měnit DOM; související princip popisuje [[React Hooks and Render Purity]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:3-21]

## Sources

- [Hooks and Context](how-to/react-cheat-sheet/09-hooks-and-context.md)
