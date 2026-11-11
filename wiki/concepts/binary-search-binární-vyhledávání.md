---
title: Binary Search — binární vyhledávání
summary: Vyhledávání v seřazeném poli opakovaně půlí prohledávaný interval a dosahuje časové složitosti O(log n).
sources:
  - how-to/algorithms/README.md
kind: concept
createdAt: "2026-11-11T10:53:58.032Z"
updatedAt: "2026-11-11T10:53:58.032Z"
tags:
  - algoritmy
  - vyhledávání
aliases:
  - binary-search-binární-vyhledávání
  - BS—BV
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Binary Search — binární vyhledávání

Binární vyhledávání hledá hodnotu v **seřazeném poli**. Porovnává hledanou hodnotu s prostředním prvkem a podle výsledku pokračuje v levé nebo pravé polovině. Každým krokem tak vyřadí polovinu zbývajících prvků. Jeho [[Časová složitost algoritmů a notace O|časová složitost]] je **O(log n)**. ^[how-to/algorithms/README.md:290-292]

## Princip

Aktuální oblast hledání vymezují indexy `lowerBound` a `upperBound`. Index `midIndex` označuje její prostřední prvek. Pokud se jeho hodnota rovná hledané hodnotě, algoritmus vrátí index. Je-li menší, posune levou hranici na `midIndex + 1`; je-li větší, posune pravou hranici na `midIndex - 1`. Hledání končí neúspěchem, když levá hranice překročí pravou; implementace tehdy vrací `-1`. ^[how-to/algorithms/README.md:306-325]

## Příklad

Při hledání hodnoty `5` v poli `[1, 2, 3, 5, 8]` jsou počáteční hranice `0` a `4`. Prostřední prvek na indexu `2` má hodnotu `3`, takže hledání pokračuje vpravo s levou hranicí `3`. Nový prostřední index je `3`, kde leží hledaná hodnota `5`; výsledkem je tedy index `3`. ^[how-to/algorithms/README.md:294-304]

## Implementace v TypeScriptu

Následující funkce přijímá seřazené číselné pole a hledanou hodnotu. Vrací index nalezeného prvku, případně `-1`, pokud hodnota v poli není. ^[how-to/algorithms/README.md:311-329]

```typescript
function binarySearch(sortedNumbers: number[], target: number): number {
  let lowerBound = 0;
  let upperBound = sortedNumbers.length - 1;

  while (lowerBound <= upperBound) {
    const midIndex = Math.floor((lowerBound + upperBound) / 2);
    const midValue = sortedNumbers[midIndex];

    if (midValue === target) return midIndex;

    if (midValue < target) {
      lowerBound = midIndex + 1;
    } else {
      upperBound = midIndex - 1;
    }
  }

  return -1;
}

binarySearch([1, 2, 3, 5, 8], 5); // 3
binarySearch([1, 2, 3, 5, 8], 4); // -1
```

## Kdy použít

Binární vyhledávání je vhodné pro seřazená pole, zejména velká. Pro neseřazené nebo malé pole zdroj doporučuje [[Linear Search — lineární vyhledávání]], které postupně porovnává jednotlivé prvky a má složitost O(n). ^[how-to/algorithms/README.md:262-274]

## Sources

- [algorithms — přehled základních algoritmů pro vývojáře](how-to/algorithms/README.md)
