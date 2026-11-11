---
title: Custom Hooks
summary: Custom hooks reuse stateful logic while giving each calling component its own independent hook state.
sources:
  - how-to/react-cheat-sheet/09-hooks-and-context.md
kind: concept
createdAt: "2026-11-11T11:00:40.495Z"
updatedAt: "2026-11-11T11:00:40.495Z"
tags:
  - react
  - hooks
  - code-reuse
aliases:
  - custom-hooks
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Custom Hooks

Custom hook je funkce, která sdílí opakovanou logiku využívající state nebo efekty. Sdílí logiku, nikoli instanci stavu: každá komponenta, která hook zavolá, má vlastní hook state. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:182-195, how-to/react-cheat-sheet/09-hooks-and-context.md:197-208]

## Příklad: `useToggle`

Hook `useToggle` zapouzdřuje boolean stav a operaci pro jeho přepnutí. Vrací aktuální hodnotu, funkci `toggle` a setter `setValue`, takže volající komponenta může hodnotu přepínat i přímo nastavovat. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:186-195]

```tsx
const useToggle = (initialValue = false) => {
  const [value, setValue] = useState(initialValue);
  const toggle = () => setValue((current) => !current);

  return { value, toggle, setValue };
};

export { useToggle };
```

Funkční updater v `toggle` počítá novou hodnotu z předchozí. Aktualizace stavu představuje žádost o nový render, nikoli okamžitou změnu aktuální proměnné. Dvě komponenty používající `useToggle` mají každá vlastní hodnotu. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:34-34, how-to/react-cheat-sheet/09-hooks-and-context.md:184-191]

## Pravidla použití

Hooky se volají pouze na nejvyšší úrovni komponenty nebo custom hooku, nikdy v podmínce, smyčce ani vnořeném callbacku. Také při zapouzdření logiky platí princip [[React Hooks and Render Purity|čistého renderu]]: render nemá měnit DOM, volat API ani zapisovat do globálních proměnných. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:3-21]

Pro [[External Synchronization with Effects|synchronizaci s externím systémem]] slouží `useEffect`, například při práci se subscription, timerem nebo browser API. Pokud hook pouze počítá hodnotu z props nebo state, efekt nepotřebuje. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:57-70]

## Vztah ke sdílenému stavu

Custom hook s vlastním stavem nezajišťuje společnou instanci stavu mezi komponentami. Pro předávání hodnoty hluboko komponentovým stromem slouží [[React Context and Providers|Context a Provider]]; vlastní hook může čtení contextu zapouzdřit a ověřit přítomnost příslušného Provideru, jako v ukázce `useAuth`. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:150-175, how-to/react-cheat-sheet/09-hooks-and-context.md:182-184]

## Sources

- [Hooks and Context](how-to/react-cheat-sheet/09-hooks-and-context.md)
