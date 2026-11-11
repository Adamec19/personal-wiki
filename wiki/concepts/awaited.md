---
title: Awaited
summary: Odvozuje typ výsledku asynchronní operace a lze jej kombinovat s ReturnType pro získání výsledného typu async funkce.
sources:
  - how-to/typescript-cheat-sheet/04-utility-types.md
kind: concept
createdAt: "2026-11-11T11:04:10.129Z"
updatedAt: "2026-11-11T11:04:10.129Z"
tags:
  - typescript
  - utility-types
  - asynchronní-programování
aliases:
  - awaited
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Awaited

`Awaited` lze použít společně s `ReturnType` k odvození typu výsledku asynchronní funkce. V následujícím příkladu `ReturnType<typeof loadUser>` získá návratový typ funkce a `Awaited` z něj odvodí typ načteného uživatele. ^[how-to/typescript-cheat-sheet/04-utility-types.md:70-75]

```ts
const loadUser = async () => ({ id: "1", name: "Ada" });
type LoadedUser = Awaited<ReturnType<typeof loadUser>>;
```

Tento způsob odvozování je užitečný, když je funkce zdrojem pravdy a její typ se nemá ručně duplikovat. Související utility popisuje stránka [[ReturnType a Parameters]]. Odvozené typy snižují duplicitu, ale neměly by skrývat důležitý business kontrakt. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-3, how-to/typescript-cheat-sheet/04-utility-types.md:57-57, how-to/typescript-cheat-sheet/04-utility-types.md:70-75]

## Sources

- how-to/typescript-cheat-sheet/04-utility-types.md
