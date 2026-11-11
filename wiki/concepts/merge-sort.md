---
title: Merge Sort
summary: Řazení metodou rozděl a panuj rekurzivně dělí pole a slučuje seřazené poloviny s časovou složitostí O(n log n).
sources:
  - how-to/algorithms/README.md
kind: concept
createdAt: "2026-11-11T10:53:48.090Z"
updatedAt: "2026-11-11T10:53:48.090Z"
tags:
  - algoritmy
  - řazení
  - rekurze
aliases:
  - merge-sort
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Merge Sort

Merge Sort je řadicí algoritmus založený na principu „rozděl a panuj“. Pole rozdělí na dvě poloviny, každou rekurzivně seřadí a poté obě seřazené části sloučí. Jeho časová složitost je **O(n log n)**; souvislosti vysvětluje [[Časová složitost algoritmů a notace O]]. ^[how-to/algorithms/README.md:133-135]

## Princip fungování

Rekurze končí u pole s nejvýše jedním prvkem, které je již seřazené. U většího pole se vypočítá střed `midIndex`, vytvoří se levá a pravá polovina a obě se zpracují stejným postupem. ^[how-to/algorithms/README.md:167-178]

Při slučování ukazují indexy `leftIndex` a `rightIndex` na první dosud nepřidané prvky obou polovin. Menší z porovnávaných hodnot se přidá do výsledku a příslušný index se posune. Jakmile se jedna polovina vyčerpá, připojí se zbývající prvky druhé poloviny. ^[how-to/algorithms/README.md:181-197]

## Příklad

Pole `[5, 3, 8, 1, 2]` se nejprve rozdělí na `[5, 3]` a `[8, 1, 2]` a dále až na jednotlivé prvky. Při návratu z rekurze vzniknou seřazené poloviny `[3, 5]` a `[1, 2, 8]`, jejichž sloučením dostaneme `[1, 2, 3, 5, 8]`. ^[how-to/algorithms/README.md:137-159]

## Implementace v TypeScriptu

Funkce `mergeSort` zajišťuje rozdělení a rekurzivní řazení, pomocná funkce `mergeSorted` slučuje dvě seřazená pole. ^[how-to/algorithms/README.md:167-198]

```typescript
function mergeSort(numbers: number[]): number[] {
  if (numbers.length <= 1) return numbers;

  const midIndex = Math.floor(numbers.length / 2);
  const leftHalf = mergeSort(numbers.slice(0, midIndex));
  const rightHalf = mergeSort(numbers.slice(midIndex));

  return mergeSorted(leftHalf, rightHalf);
}

function mergeSorted(leftHalf: number[], rightHalf: number[]): number[] {
  const merged: number[] = [];
  let leftIndex = 0;
  let rightIndex = 0;

  while (leftIndex < leftHalf.length && rightIndex < rightHalf.length) {
    if (leftHalf[leftIndex] <= rightHalf[rightIndex]) {
      merged.push(leftHalf[leftIndex++]);
    } else {
      merged.push(rightHalf[rightIndex++]);
    }
  }

  return [
    ...merged,
    ...leftHalf.slice(leftIndex),
    ...rightHalf.slice(rightIndex),
  ];
}

mergeSort([5, 3, 8, 1, 2]); // [1, 2, 3, 5, 8]
```

## Kdy jej použít

Zdroj doporučuje Merge Sort nebo [[Quick Sort]] pro řazení velkého pole vlastním způsobem. ^[how-to/algorithms/README.md:531-536]

## Sources

- [algorithms — přehled základních algoritmů pro vývojáře](how-to/algorithms/README.md)
