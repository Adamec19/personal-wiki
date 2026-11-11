---
title: Odvozené hodnoty a jediný zdroj pravdy
summary: Hodnoty odvoditelné z props nebo existujícího stavu se mají přímo vypočítat, protože samostatný state synchronizovaný effectem duplikuje zdroj pravdy.
sources:
  - how-to/react-cheat-sheet/03-state-and-effects.md
kind: concept
createdAt: "2026-11-11T10:58:16.827Z"
updatedAt: "2026-11-11T10:58:16.827Z"
tags:
  - react
  - derived-state
  - data-consistency
aliases:
  - odvozené-hodnoty-a-jediný-zdroj-pravdy
  - OHAJZP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Odvozené hodnoty a jediný zdroj pravdy

Odvozené hodnoty se počítají z existujících props nebo state. Nemají se ukládat jako další state ani aktualizovat pomocí `useEffect`, protože tím vzniká duplicitní zdroj pravdy. ^[how-to/react-cheat-sheet/03-state-and-effects.md:12-21]

## Výpočet během renderu

Pokud je celé jméno složené z křestního jména a příjmení, stačí ve state uchovávat tyto dvě vstupní hodnoty a `fullName` přímo vypočítat. Tento postup odpovídá principu [[Odvozené hodnoty během renderu]]. ^[how-to/react-cheat-sheet/03-state-and-effects.md:14-21]

```tsx
const [firstName, setFirstName] = useState("");
const [lastName, setLastName] = useState("");

const fullName = `${firstName} ${lastName}`.trim();
```

## Hranice mezi výpočtem a efektem

`useEffect` slouží k [[Synchronizace s externími systémy pomocí useEffect|synchronizaci s externími systémy]], například k práci se subscriptions, event listenery, timery nebo imperativními API. Effect, který pouze přepočítává hodnotu z props či state, je uveden mezi častými chybami. ^[how-to/react-cheat-sheet/03-state-and-effects.md:23-30, how-to/react-cheat-sheet/03-state-and-effects.md:43-45]

## Umístění zdrojového stavu

Zdrojový state má být na nejnižším místě komponentového stromu, které jej potřebuje. Jedné komponentě stačí `useState`; sourozenci sdílejí state ve společném rodiči a vzdálené části jedné oblasti mohou využít context nebo feature store. Podrobněji viz [[Umístění a sdílení stavu v komponentovém stromu]]. ^[how-to/react-cheat-sheet/03-state-and-effects.md:3-9]

Více zdrojů pravdy pro stejnou hodnotu patří mezi časté chyby správy stavu. U odvozených hodnot se této duplicitě předchází přímým výpočtem z původních dat. ^[how-to/react-cheat-sheet/03-state-and-effects.md:12-21, how-to/react-cheat-sheet/03-state-and-effects.md:43-48]

## Sources

- [State and Effects](how-to/react-cheat-sheet/03-state-and-effects.md)
