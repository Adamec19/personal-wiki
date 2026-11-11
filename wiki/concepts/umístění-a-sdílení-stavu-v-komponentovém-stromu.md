---
title: Umístění a sdílení stavu v komponentovém stromu
summary: "State patří na nejnižší potřebnou úroveň: lokálně do useState, pro sourozence do společného rodiče a pro vzdálené části oblasti do contextu nebo feature storu."
sources:
  - how-to/react-cheat-sheet/03-state-and-effects.md
kind: concept
createdAt: "2026-11-11T10:58:12.657Z"
updatedAt: "2026-11-11T10:58:12.657Z"
tags:
  - react
  - state-management
  - component-architecture
aliases:
  - umístění-a-sdílení-stavu-v-komponentovém-stromu
  - UASSVKS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Umístění a sdílení stavu v komponentovém stromu

Stav patří do nejnižšího místa v komponentovém stromu, které jej potřebuje. Jeho umístění a způsob sdílení se řídí tím, které komponenty jej využívají a zda jde o lokální stav, nebo serverová data. ^[how-to/react-cheat-sheet/03-state-and-effects.md:3-10]

## Volba umístění

- **Jedna komponenta:** použij `useState`.
- **Více sourozenců:** přesuň stav do jejich společného rodiče.
- **Vzdálené části jedné oblasti:** použij context nebo feature store.
- **Serverová data:** použij query/cache vrstvu.

Tato pravidla propojují [[Lokální a sdílený stav]], [[React Context and Providers]] a [[Správa serverových dat pomocí query/cache vrstvy|správu serverových dat pomocí query/cache vrstvy]]. Serverová data nemají být spravována jako ruční globální stav. ^[how-to/react-cheat-sheet/03-state-and-effects.md:5-10]

## Jediný zdroj pravdy

Hodnotu, kterou lze odvodit z existujících props nebo stavu, neukládej jako další stav. Například celé jméno lze vypočítat během renderu z `firstName` a `lastName`; samostatný stav `fullName` aktualizovaný pomocí `useEffect` by duplikoval zdroj pravdy. Viz [[Odvozené hodnoty a jediný zdroj pravdy]]. ^[how-to/react-cheat-sheet/03-state-and-effects.md:12-21]

```tsx
const [firstName, setFirstName] = useState("");
const [lastName, setLastName] = useState("");

const fullName = `${firstName} ${lastName}`.trim();
```

## Časté chyby

Globální store pro krátkodobý stav dialogu jedné komponenty umisťuje stav zbytečně vysoko. Dalšími chybami jsou více zdrojů pravdy pro stejnou hodnotu a effect, který pouze přepočítává hodnotu z props nebo stavu. Pro dialog používaný jedinou komponentou souvisí tato zásada s konceptem [[Local dialog state]]. ^[how-to/react-cheat-sheet/03-state-and-effects.md:43-48]

## Sources

- [State and Effects](how-to/react-cheat-sheet/03-state-and-effects.md)
