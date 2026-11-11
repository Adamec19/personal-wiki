---
title: Ochrana před závodícími požadavky
summary: Ruš předchozí požadavky pomocí AbortController a ověřuj aktuálnost odpovědi, aby starší výsledek nepřepsal novější stav.
sources:
  - how-to/react-cheat-sheet/06-api-and-data.md
kind: concept
createdAt: "2026-11-11T10:59:25.954Z"
updatedAt: "2026-11-11T10:59:25.954Z"
tags:
  - souběh
  - api
aliases:
  - ochrana-před-závodícími-požadavky
  - OPZP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Ochrana před závodícími požadavky

Pokud se API požadavky spouštějí rychle za sebou, starší odpověď nesmí přepsat novější stav. Ochrana před závodícími požadavky spojuje zrušení předchozího požadavku s kontrolou, zda odpověď patří stále aktuálnímu požadavku. ^[how-to/react-cheat-sheet/06-api-and-data.md:39-55]

## Zrušení a kontrola aktuálnosti

Pro nový požadavek se vytvoří `AbortController`, předchozí controller se zruší pomocí `abort()` a nový se uloží jako aktuální. Jeho `signal` se předá funkci `fetch`. Před aktualizací dat se ověří, že controller dokončeného požadavku odpovídá aktuálně uloženému controlleru. ^[how-to/react-cheat-sheet/06-api-and-data.md:44-50]

```tsx
const controller = new AbortController();
previousController?.abort();
previousController = controller;

try {
  const result = await fetch(url, { signal: controller.signal });
  if (controller === previousController) setData(result);
} catch (error) {
  if (error instanceof DOMException && error.name === "AbortError") return;
  throw error;
}
```

Zrušený požadavek se v obsluze chyb rozpozná jako `DOMException` s názvem `"AbortError"` a jeho zpracování se ukončí. Ostatní chyby se předají dál pomocí `throw`. ^[how-to/react-cheat-sheet/06-api-and-data.md:51-54]

## Souvislost se stavem požadavku

Ochrana před závodícími odpověďmi souvisí se [[Správa stavu API požadavků|správou stavu API požadavků]]. Data, příznak načítání a chyba mají být udržovány pohromadě. Je potřeba rozlišovat počáteční načítání, opakované načítání a mutaci a při selhání požadavku neprezentovat stará data jako čerstvá. ^[how-to/react-cheat-sheet/06-api-and-data.md:25-37]

## Sources

- [API and Data](how-to/react-cheat-sheet/06-api-and-data.md)
