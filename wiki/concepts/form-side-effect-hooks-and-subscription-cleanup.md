---
title: Form Side-Effect Hooks and Subscription Cleanup
summary: Isolate reactions to field changes in hooks and unsubscribe from field-change subscriptions during effect cleanup.
sources:
  - how-to/react-cheat-sheet/04-forms.md
kind: concept
createdAt: "2026-11-11T10:58:37.961Z"
updatedAt: "2026-11-11T10:58:37.961Z"
tags:
  - forms
  - react-hooks
  - side-effects
aliases:
  - form-side-effect-hooks-and-subscription-cleanup
  - Subscription Cleanup and Form Side-Effect Hooks
  - FSHASC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Form Side-Effect Hooks and Subscription Cleanup

Reakce na změny formulářových polí odděluj do vlastního hooku a při použití subscription vždy zajisti její úklid. V navržené struktuře formuláře patří side effects spolu se submit logikou do adresáře `hooks/`. ^[how-to/react-cheat-sheet/04-forms.md:5-12, how-to/react-cheat-sheet/04-forms.md:52-65]

## Sledování změn polí

Následující příklad v `useEffect` vytvoří subscription pomocí `watch`. Při změně pole `country` resetuje pole `postalCode`. Cleanup funkce zavolá `subscription.unsubscribe()`; závislostmi efektu jsou `resetField` a `watch`. Tento postup propojuje reakci na změny s [[Cleanup efektů|úklidem efektu]]. ^[how-to/react-cheat-sheet/04-forms.md:54-65]

```tsx
useEffect(() => {
  const subscription = watch((value, { name }) => {
    if (name === "country") {
      resetField("postalCode");
    }
  });

  return () => subscription.unsubscribe();
}, [resetField, watch]);
```

## Oddělení odpovědností

V rámci [[Layered Form Architecture|vrstvené architektury formuláře]] má [[Form Field Wrappers|field wrapper]] zajišťovat napojení formuláře na UI primitive, nikoli business rozhodnutí celé feature. Reakce na změny polí proto patří do samostatného hooku. ^[how-to/react-cheat-sheet/04-forms.md:50-54]

## Sources

- [Forms](how-to/react-cheat-sheet/04-forms.md)
