---
title: Správa stavu API požadavků
summary: Udržuj data, loading a chybu pohromadě, rozlišuj initial loading, refetch a mutation a nevydávej stará data za čerstvá po selhání.
sources:
  - how-to/react-cheat-sheet/06-api-and-data.md
kind: concept
createdAt: "2026-11-11T10:59:24.640Z"
updatedAt: "2026-11-11T10:59:24.640Z"
tags:
  - správa-stavu
  - api
aliases:
  - správa-stavu-api-požadavků
  - SSAP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Správa stavu API požadavků

Správa stavu API požadavků udržuje data, průběh načítání a chybu pohromadě. Rozlišuje počáteční načítání, opakované načtení (refetch) a mutaci. Pokud požadavek selže, stará data se nemají zobrazovat jako čerstvá. ^[how-to/react-cheat-sheet/06-api-and-data.md:25-37]

## Společný model stavu

Stav jedné akce lze vyjádřit typem `RequestState<T>`, který sdružuje data typu `T` nebo `null`, příznak načítání a chybu nebo `null`. ^[how-to/react-cheat-sheet/06-api-and-data.md:27-35]

```tsx
type RequestState<T> = {
  data: T | null;
  isLoading: boolean;
  error: Error | null;
};
```

## [[ochrana-před-závodícími-požadavky|Ochrana před závodícími požadavky]]

Pokud se požadavky spouštějí rychle za sebou, starší odpověď nesmí přepsat novější stav. Ukázka pro [[Ochrana před závodícími požadavky|ochranu před závodícími požadavky]] ruší předchozí požadavek pomocí `AbortController`, před aktualizací dat ověřuje totožnost aktuálního controlleru a chybu `AbortError` ignoruje. ^[how-to/react-cheat-sheet/06-api-and-data.md:39-54]

## Validace dat a cache

Externí data jsou `unknown`, dokud je neověří schéma nebo bezpečný parser. [[Compile-time typy versus runtime validace|Runtime validace]] tak ověřuje odpověď před jejím dalším použitím v datovém toku. ^[how-to/react-cheat-sheet/06-api-and-data.md:11-23]

Při [[Správa serverových dat pomocí query/cache vrstvy|správě serverových dat pomocí query/cache vrstvy]] musí klíč cache obsahovat všechny parametry, které mění výsledek. Jinak může komponenta zobrazit data z jiné varianty dotazu; příkladem je klíč zahrnující organizaci, hledaný výraz a stránku. ^[how-to/react-cheat-sheet/06-api-and-data.md:57-63]

```tsx
queryKey: ["users", { organizationId, search, page }]
```

## Sources

- [API and Data](how-to/react-cheat-sheet/06-api-and-data.md)
