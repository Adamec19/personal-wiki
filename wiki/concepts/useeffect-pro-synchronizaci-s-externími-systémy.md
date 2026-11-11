---
title: useEffect pro synchronizaci s externími systémy
summary: useEffect slouží k synchronizaci s externími systémy, například subscriptions, časovači, browser API nebo síťovými API.
sources:
  - how-to/react-cheat-sheet/03-state-and-effects.md
kind: concept
createdAt: "2026-11-11T10:58:15.728Z"
updatedAt: "2026-11-11T10:58:15.728Z"
tags:
  - react
  - effects
  - external-systems
aliases:
  - useeffect-pro-synchronizaci-s-externími-systémy
  - UPSSES
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# useEffect pro synchronizaci s externími systémy

`useEffect` slouží k synchronizaci komponenty s externím systémem. Používá se pro subscriptions, event listenery, timery, browser API nebo síťová a jiná imperativní API. ^[how-to/react-cheat-sheet/03-state-and-effects.md:23-30]

## Synchronizace a cleanup

Effect může vytvořit připojení podle aktuálního `roomId` a vrátit funkci, která toto připojení ukončí. [[Cleanup efektů|Cleanup]] musí zrušit přesně to, co effect vytvořil. ^[how-to/react-cheat-sheet/03-state-and-effects.md:32-41]

```tsx
useEffect(() => {
  const connection = createConnection(roomId);
  connection.connect();

  return () => connection.disconnect();
}, [roomId]);
```

U listenerů a timerů je chybějící cleanup častou chybou. Další chybou je vynechávání závislostí pouze proto, aby effect běžel méně často. ^[how-to/react-cheat-sheet/03-state-and-effects.md:43-49]

## Kdy effect nepoužívat

Hodnoty, které lze vypočítat z props nebo state, patří mezi [[Odvozené hodnoty během renderu|odvozené hodnoty během renderu]]. Například `fullName` lze sestavit přímo z `firstName` a `lastName`; samostatný state aktualizovaný effectem by pouze duplikoval zdroj pravdy. ^[how-to/react-cheat-sheet/03-state-and-effects.md:12-21]

```tsx
const [firstName, setFirstName] = useState("");
const [lastName, setLastName] = useState("");

const fullName = `${firstName} ${lastName}`.trim();
```

## Sources

- [State and Effects](how-to/react-cheat-sheet/03-state-and-effects.md)
