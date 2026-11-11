---
title: Cleanup efektů
summary: Cleanup musí přesně zrušit prostředky vytvořené effectem, například odpojit spojení, odstranit listener nebo zastavit timer.
sources:
  - how-to/react-cheat-sheet/03-state-and-effects.md
kind: concept
createdAt: "2026-11-11T10:58:22.606Z"
updatedAt: "2026-11-11T10:58:22.606Z"
tags:
  - react
  - effects
  - resource-lifecycle
aliases:
  - cleanup-efektů
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Cleanup efektů

Cleanup je úklidová funkce vrácená z `useEffect`. Musí zrušit přesně to, co effect vytvořil. Patří k [[Synchronizace s externími systémy pomocí useEffect|synchronizaci s externími systémy]], například při práci s připojením, subscriptions, event listenery nebo timery. ^[how-to/react-cheat-sheet/03-state-and-effects.md:23-41]

## Příklad připojení

Effect vytvoří připojení pro `roomId` a připojí ho. Vrácená cleanup funkce zavolá `disconnect()` na stejném připojení. ^[how-to/react-cheat-sheet/03-state-and-effects.md:32-39]

```tsx
useEffect(() => {
  const connection = createConnection(roomId);
  connection.connect();

  return () => connection.disconnect();
}, [roomId]);
```

## Časté chyby

Effect bez cleanup pro listener nebo timer je častou chybou. Další chybou je vynechávání závislostí pouze proto, aby effect běžel méně často. ^[how-to/react-cheat-sheet/03-state-and-effects.md:43-49]

Effect nemá sloužit pouze k přepočtu hodnot z props nebo state. [[Odvozené hodnoty během renderu|Odvozené hodnoty]] lze vypočítat přímo; jejich ukládání do dalšího state a aktualizace přes effect duplikuje zdroj pravdy. ^[how-to/react-cheat-sheet/03-state-and-effects.md:12-21, how-to/react-cheat-sheet/03-state-and-effects.md:43-45]

## Sources

- [State and Effects](how-to/react-cheat-sheet/03-state-and-effects.md)
