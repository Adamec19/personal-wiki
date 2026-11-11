---
title: Časová složitost algoritmů a notace O
summary: Notace O popisuje růst výpočetní náročnosti algoritmu podle velikosti vstupu, od konstantní po exponenciální složitost.
sources:
  - how-to/algorithms/README.md
kind: concept
createdAt: "2026-11-11T10:53:54.120Z"
updatedAt: "2026-11-11T10:53:54.120Z"
tags:
  - algoritmy
  - časová-složitost
aliases:
  - časová-složitost-algoritmů-a-notace-o
  - ČSAANO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Časová složitost algoritmů a notace O

Časová složitost umožňuje porovnat výpočetní náročnost algoritmů. Zdrojový přehled používá notaci O a rozlišuje konstantní, logaritmickou, lineární, linearitmickou, kvadratickou a exponenciální složitost. ^[how-to/algorithms/README.md:7-16]

## Přehled základních složitostí

| Notace | Název | Příklad |
|---|---|---|
| O(1) | konstantní | Přístup k prvku pole |
| O(log n) | logaritmická | [[Binary Search — binární vyhledávání]] |
| O(n) | lineární | [[Linear Search — lineární vyhledávání]] |
| O(n log n) | linearitmická | [[Merge Sort]], [[Quick Sort]] |
| O(n²) | kvadratická | Bubble Sort, Insertion Sort |
| O(2ⁿ) | exponenciální | Rekurzivní výpočet Fibonacciho čísel bez cache |

Tabulka shrnuje základní kategorie uvedené ve zdroji. U konkrétního algoritmu je důležité rozlišovat také podmínky použití a průměrný či nejhorší případ. Například [[quick-sort|Quick Sort]] má průměrnou složitost O(n log n), ale v nejhorším případě O(n²). ^[how-to/algorithms/README.md:7-16, how-to/algorithms/README.md:205-207]

## Jak se složitost projevuje v algoritmech

### Lineární a binární vyhledávání

Lineární vyhledávání prochází pole postupně a porovnává jednotlivé prvky s hledanou hodnotou. Má složitost O(n) a hodí se pro neseřazená nebo malá pole. Při prvním nalezení vrací index; pokud hodnotu nenajde, vrací `-1`. ^[how-to/algorithms/README.md:262-285]

Binární vyhledávání má složitost O(log n), ale vyžaduje **seřazené pole**. Porovná hledanou hodnotu s prostředním prvkem a pokračuje pouze v odpovídající polovině. Každý krok tak odstraní polovinu zbývajících kandidátů. ^[how-to/algorithms/README.md:290-303]

### Řazení

[[merge-sort|Merge Sort]] má složitost O(n log n). Pole rozdělí na poloviny, obě rekurzivně seřadí a následně sloučí porovnáváním aktuálních prvků obou částí. ^[how-to/algorithms/README.md:133-135, how-to/algorithms/README.md:166-198]

[[quick-sort|Quick Sort]] rozděluje prvky podle pivotu na menší, stejné a větší. Menší a větší skupinu rekurzivně seřadí. Jeho výkon ovlivňuje volba pivotu; průměrná složitost je O(n log n), nejhorší O(n²). ^[how-to/algorithms/README.md:205-207, how-to/algorithms/README.md:232-250]

### Vliv memoizace

[[Dynamické programování a memoizace]] ukazuje, že ukládání výsledků opakujících se podproblémů může změnit časovou složitost. Rekurzivní výpočet Fibonacciho čísel bez cache opakovaně počítá stejné hodnoty a má ve zdroji uvedenou složitost O(2ⁿ). S memoizací se každá pozice vypočítá jen jednou a složitost je O(n). ^[how-to/algorithms/README.md:471-488, how-to/algorithms/README.md:504-523]

## Použití při výběru algoritmu

Samotnou notaci je potřeba posuzovat spolu s vlastnostmi vstupu a řešeným úkolem. Pro hledání v neseřazeném poli zdroj doporučuje lineární vyhledávání, pro seřazené pole binární vyhledávání, pro vlastní řazení velkého pole [[merge-sort|Merge Sort]] nebo [[quick-sort|Quick Sort]] a pro opakující se podproblémy memoizaci. ^[how-to/algorithms/README.md:531-541]

## Sources

- [how-to/algorithms/README.md](how-to/algorithms/README.md)
