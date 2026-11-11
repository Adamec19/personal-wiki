---
title: Úplnost závislostí useEffect
summary: Závislosti effectu se nemají vynechávat pouze za účelem omezení četnosti jeho spouštění.
sources:
  - how-to/react-cheat-sheet/03-state-and-effects.md
kind: concept
createdAt: "2026-11-11T10:58:25.705Z"
updatedAt: "2026-11-11T10:58:25.705Z"
tags:
  - react
  - effects
  - dependencies
aliases:
  - úplnost-závislostí-useeffect
  - ÚZU
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Úplnost závislostí useEffect

Závislosti `useEffect` se nemají vynechávat jen proto, aby se efekt spouštěl méně často. Efekt slouží k [[Synchronizace s externími systémy pomocí useEffect|synchronizaci s externím systémem]], například subscription, event listenerem, timerem, browser API nebo síťovým API. ^[how-to/react-cheat-sheet/03-state-and-effects.md:23-30, how-to/react-cheat-sheet/03-state-and-effects.md:43-49]

## Závislosti a cleanup

Následující efekt vytváří připojení podle `roomId` a uvádí tuto hodnotu v poli závislostí. Vrácený cleanup připojení odpojí; obecně musí zrušit přesně to, co efekt vytvořil. ^[how-to/react-cheat-sheet/03-state-and-effects.md:32-41]

```tsx
useEffect(() => {
  const connection = createConnection(roomId);
  connection.connect();

  return () => connection.disconnect();
}, [roomId]);
```

## Kdy efekt není potřeba

Pokud efekt pouze přepočítává hodnotu z props nebo state, jde o chybné použití. Například `fullName` lze odvodit přímo z `firstName` a `lastName` během renderu. Samostatný state aktualizovaný efektem by duplikoval zdroj pravdy; souvisejícím principem jsou [[Odvozené hodnoty během renderu]]. ^[how-to/react-cheat-sheet/03-state-and-effects.md:12-21, how-to/react-cheat-sheet/03-state-and-effects.md:43-48]

## Sources

- [State and Effects](how-to/react-cheat-sheet/03-state-and-effects.md)
