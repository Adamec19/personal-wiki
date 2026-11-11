---
title: State Management with useState and useReducer
summary: useState manages local UI values, while useReducer centralizes complex state transitions in a pure reducer.
sources:
  - how-to/react-cheat-sheet/09-hooks-and-context.md
kind: concept
createdAt: "2026-11-11T11:00:22.327Z"
updatedAt: "2026-11-11T11:00:22.327Z"
tags:
  - react
  - state-management
  - hooks
aliases:
  - state-management-with-usestate-and-usereducer
  - useReducer and State Management with useState
  - SMWUAU
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# State Management with useState and useReducer

React nabízí `useState` pro lokální hodnoty ovlivňující UI a `useReducer` pro složitější stav s více akcemi a přechody. Oba hooky se volají pouze na nejvyšší úrovni komponenty nebo custom hooku, nikoli v podmínkách, smyčkách či vnořených callbackách. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:3-3, how-to/react-cheat-sheet/09-hooks-and-context.md:23-38]

## `useState`: lokální stav

`useState` uchovává lokální hodnotu, jejíž změna má ovlivnit UI. Následující příklad ukazuje stav otevření a dva způsoby jeho aktualizace. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:23-32]

```tsx
const [isOpen, setIsOpen] = useState(false);

setIsOpen(true);
setIsOpen((previous) => !previous);
```

Pokud nová hodnota závisí na předchozí, použije se funkční updater, například `setIsOpen((previous) => !previous)`. Aktualizace stavu představuje žádost o nový render, nikoli okamžitou mutaci aktuální proměnné. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:28-34]

## `useReducer`: explicitní přechody stavu

`useReducer` je vhodný pro složitější stav s více akcemi a přechody. Reducer centralizuje pravidla přechodů; v příkladu akce `submit`, `success` a `error` určují následující hodnotu `status`. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:36-55]

```tsx
type State = { status: "idle" | "loading" | "success" | "error" };
type Action = { type: "submit" } | { type: "success" } | { type: "error" };

const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case "submit": return { status: "loading" };
    case "success": return { status: "success" };
    case "error": return { status: "error" };
  }
};

const [state, dispatch] = useReducer(reducer, { status: "idle" });
```

Reducer nemá volat API ani měnit externí systém. Pro synchronizaci mimo React slouží [[External Synchronization with Effects|useEffect]], například při práci se subscription, časovačem nebo browser API. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:55-59]

## Volba hooku a hranice odpovědnosti

Základním vodítkem je povaha aktualizací: pro hodnotu měnící UI slouží `useState`, pro více explicitních přechodů `useReducer`. Render přitom musí zůstat čistý — nesmí měnit DOM, volat API ani zapisovat do globálních proměnných; podrobněji viz [[React Hooks and Render Purity]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:21-21, how-to/react-cheat-sheet/09-hooks-and-context.md:197-203]

Pokud změna hodnoty nemusí vyvolat render, lze použít [[Persistent Mutable References with useRef|useRef]]. Jestliže se změna musí projevit v UI, patří hodnota do stavu. Hodnoty pouze vypočítané z props nebo stavu samy o sobě nevyžadují effect; souvisejí s tématem [[Odvozené hodnoty během renderu]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:70-86]

Opakovanou logiku lze vyčlenit do [[Custom Hooks|custom hooku]]. Tím se sdílí logika, nikoli instance stavu: každá komponenta, která hook zavolá, má vlastní hook state. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:182-195]

## Sources

- [Hooks and Context](how-to/react-cheat-sheet/09-hooks-and-context.md)
