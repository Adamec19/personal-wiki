---
title: Event Callbacks and Decision Ownership
summary: Name event handlers after actions and keep business decisions with the component that owns them, outside generic UI controls.
sources:
  - how-to/react-cheat-sheet/02-components.md
kind: concept
createdAt: "2026-11-11T10:58:02.699Z"
updatedAt: "2026-11-11T10:58:02.699Z"
tags:
  - components
  - events
  - separation-of-concerns
aliases:
  - event-callbacks-and-decision-ownership
  - Decision Ownership and Event Callbacks
  - ECADO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Event Callbacks and Decision Ownership

Event callbacky propojují uživatelské akce s komponentou, která vlastní příslušné rozhodnutí. Obecné komponenty, například Button nebo Input, nemají obsahovat business rozhodnutí; callback má zůstat u komponenty, která za ně odpovídá. ^[how-to/react-cheat-sheet/02-components.md:57-62]

## Pojmenování a veřejný kontrakt

Event handlery se pojmenovávají podle akce, například `onSubmit`, `onRemove` nebo `onChange`. Jako součást props tvoří [[Component Props as a Public Contract|veřejný kontrakt komponenty]], který má být malý a explicitní. Ukázkový `SaveButton` proto přijímá callback `onSave: () => void` a předává jej tlačítku jako `onClick`. ^[how-to/react-cheat-sheet/02-components.md:5-23, how-to/react-cheat-sheet/02-components.md:57-61]

## Vlastnictví rozhodnutí a stavu

Pokud rodič potřebuje hodnotu znát nebo řídit, použije se [[Controlled Components and State Ownership|controlled komponenta]]. Ukázkový `Toggle` přijímá hodnotu `isOn` a při kliknutí volá `onChange(!isOn)`: změnu oznamuje callbackem a aktuální hodnotu dostává přes props. Kopírování props do lokálního stavu pouze pro pohodlnější práci vytváří synchronizační problém. ^[how-to/react-cheat-sheet/02-components.md:25-39]

## Stabilita callbacků

`useCallback` se používá tehdy, když je potřeba stabilní identita předávané závislosti, nikoli automaticky pro každý handler. Toto pravidlo rozvíjí [[Purposeful useCallback Usage]]. ^[how-to/react-cheat-sheet/02-components.md:62-62]

## Sources

- [Components](how-to/react-cheat-sheet/02-components.md)
