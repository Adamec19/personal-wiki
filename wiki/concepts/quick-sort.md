---
title: Quick Sort
summary: Řazení rozděluje prvky podle pivotu a rekurzivně třídí vzniklé části; průměrná složitost je O(n log n), nejhorší O(n²).
sources:
  - how-to/algorithms/README.md
kind: concept
createdAt: "2026-11-11T10:53:53.480Z"
updatedAt: "2026-11-11T10:53:53.480Z"
tags:
  - algoritmy
  - řazení
  - rekurze
aliases:
  - quick-sort
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Quick Sort

Quick Sort je řadicí algoritmus, který vybere referenční prvek zvaný **pivot** a rozdělí pole na tři skupiny: prvky menší než pivot, prvky rovné pivotu a prvky větší než pivot. Menší a větší skupinu rekurzivně seřadí a výsledky spojí v pořadí `smaller + equal + greater`. ^[how-to/algorithms/README.md:205-207]

## Princip a příklad

Pro vstup `[5, 3, 8, 1, 2]` zvolí uvedená implementace prostřední prvek `8` jako pivot. Vzniknou skupiny `smaller = [5, 3, 1, 2]`, `equal = [8]` a `greater = []`. Při dalším dělení menší skupiny je pivotem `3`, takže vzniknou `[1, 2]`, `[3]` a `[5]`. Po rekurzivním seřazení a spojení je výsledkem `[1, 2, 3, 5, 8]`. ^[how-to/algorithms/README.md:209-230]

Rekurze končí u pole s nejvýše jedním prvkem, které funkce vrací přímo. Skupina `equal` se dále neřadí; rekurzivní volání zpracovávají pouze `smaller` a `greater`. ^[how-to/algorithms/README.md:239-250]

## Implementace v TypeScriptu

Následující varianta vybírá pivot ze středu pole, vytváří tři skupiny pomocí `filter` a spojuje je pomocí spread syntaxe. ^[how-to/algorithms/README.md:238-254]

```typescript
function quickSort(numbers: number[]): number[] {
  if (numbers.length <= 1) return numbers;

  const pivot = numbers[Math.floor(numbers.length / 2)];

  const smaller = numbers.filter(item => item < pivot);
  const equal = numbers.filter(item => item === pivot);
  const greater = numbers.filter(item => item > pivot);

  return [...quickSort(smaller), ...equal, ...quickSort(greater)];
}

quickSort([5, 3, 8, 1, 2]); // [1, 2, 3, 5, 8]
```

## Časová složitost a použití

Průměrná časová složitost Quick Sortu je **O(n log n)**, zatímco v nejhorším případě dosahuje **O(n²)**. Volba pivotu ovlivňuje výkon. Význam těchto zápisů rozebírá [[Časová složitost algoritmů a notace O]]. ^[how-to/algorithms/README.md:205-207, how-to/algorithms/README.md:232-243]

Zdroj uvádí Quick Sort spolu s [[Merge Sort]] jako možnost pro vlastní řazení velkého pole. ^[how-to/algorithms/README.md:531-536]

## Sources

- [algorithms — přehled základních algoritmů pro vývojáře](how-to/algorithms/README.md)
