---
title: Linear Search — lineární vyhledávání
summary: Postupné porovnávání prvků vrací index prvního výskytu hledané hodnoty a funguje i na neseřazeném poli se složitostí O(n).
sources:
  - how-to/algorithms/README.md
kind: concept
createdAt: "2026-11-11T10:53:53.801Z"
updatedAt: "2026-11-11T10:53:53.801Z"
tags:
  - algoritmy
  - vyhledávání
aliases:
  - linear-search-lineární-vyhledávání
  - LS—LV
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Linear Search — lineární vyhledávání

Lineární vyhledávání prochází pole od začátku a každý prvek porovnává s hledanou hodnotou. Při první shodě vrátí index nalezeného prvku; pokud hodnota v poli není, vrátí `-1`. ^[how-to/algorithms/README.md:262-285]

## Kdy ho použít a jaká je složitost

Hodí se pro neseřazená nebo malá pole. Jeho časová složitost je **O(n)**, tedy lineární; souvislosti vysvětluje [[Časová složitost algoritmů a notace O]]. Pro velké seřazené pole zdroj doporučuje [[Binary Search — binární vyhledávání]], které má složitost O(log n). ^[how-to/algorithms/README.md:262-274, how-to/algorithms/README.md:290-292]

## Postup na příkladu

Při hledání hodnoty `8` v poli `[5, 3, 8, 1, 2]` algoritmus nejprve porovná `5`, potom `3` a nakonec `8`. Třetí porovnání najde shodu, takže vyhledávání skončí a vrátí index `2`. ^[how-to/algorithms/README.md:266-272]

## Implementace v TypeScriptu

Funkce prochází indexy pole ve smyčce a porovnává hodnoty pomocí `===`. Návrat při první shodě ukončí hledání; `-1` se vrací až po průchodu celým polem bez nalezení hodnoty. ^[how-to/algorithms/README.md:276-285]

```typescript
function linearSearch(numbers: number[], target: number): number {
  for (let index = 0; index < numbers.length; index++) {
    if (numbers[index] === target) return index;
  }
  return -1;
}

linearSearch([5, 3, 8, 1, 2], 8); // 2
linearSearch([5, 3, 8, 1, 2], 9); // -1
```

## Sources

- [algorithms — přehled základních algoritmů pro vývojáře](how-to/algorithms/README.md)
