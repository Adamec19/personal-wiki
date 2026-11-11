---
title: Dynamické programování a memoizace
summary: Ukládání výsledků opakujících se podproblémů omezuje zbytečné výpočty; u uvedeného Fibonacciho algoritmu snižuje složitost z O(2ⁿ) na O(n).
sources:
  - how-to/algorithms/README.md
kind: concept
createdAt: "2026-11-11T10:54:14.558Z"
updatedAt: "2026-11-11T10:54:14.558Z"
tags:
  - algoritmy
  - dynamické-programování
  - memoizace
aliases:
  - dynamické-programování-a-memoizace
  - DPAM
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Dynamické programování a memoizace

Dynamické programování řeší problémy, které lze rozložit na opakující se podproblémy. Výsledky těchto podproblémů se ukládají do cache, aby je při dalším použití nebylo nutné znovu počítat. Memoizace tento postup využívá při výpočtu: pokud už výsledek existuje, vrátí jej z cache. ^[how-to/algorithms/README.md:471-473, how-to/algorithms/README.md:491-502]

## Příklad: Fibonacciho posloupnost

Fibonacciho číslo na pozici `n` je součtem dvou předchozích čísel. Základní hodnoty jsou `fib(0) = 0` a `fib(1) = 1`; posloupnost pokračuje hodnotami `1, 2, 3, 5, 8, …`. ^[how-to/algorithms/README.md:475-478]

Přímočará rekurzivní implementace opakovaně řeší stejné podproblémy. Například `fib(5)` volá `fib(4)` i `fib(3)`, ale také výpočet `fib(4)` znovu vyvolá `fib(3)`. Bez cache tak vzniká mnoho zbytečných výpočtů; zdroj uvádí časovou složitost O(2ⁿ). ^[how-to/algorithms/README.md:480-488, how-to/algorithms/README.md:504-509]

S memoizací se každá pozice vypočítá pouze jednou a další požadavky využijí uloženou hodnotu. Časová složitost tohoto řešení je O(n); související zápis vysvětluje [[Časová složitost algoritmů a notace O]]. ^[how-to/algorithms/README.md:491-498, how-to/algorithms/README.md:511-522]

## Implementace v TypeScriptu

Funkce používá `Map<number, number>`, kde klíčem je pozice v posloupnosti a hodnotou vypočtené Fibonacciho číslo. Nejprve ošetří základní případy, poté zkontroluje cache. Chybějící výsledek vypočítá rekurzivně, uloží jej a vrátí. Obě rekurzivní volání sdílejí stejnou cache. ^[how-to/algorithms/README.md:500-523]

```typescript
function fib(
  position: number,
  cache: Map<number, number> = new Map()
): number {
  if (position <= 1) return position;

  if (cache.has(position)) return cache.get(position)!;

  const result =
    fib(position - 1, cache) + fib(position - 2, cache);

  cache.set(position, result);
  return result;
}

fib(10); // 55
fib(50); // 12586269025
```

## Kdy použít

Dynamické programování s memoizací se hodí pro výpočty s opakujícími se podproblémy, jejichž výsledky lze uložit a později znovu využít. Fibonacciho posloupnost ukazuje, jak odstranění opakovaných výpočtů mění exponenciální časovou složitost na lineární. ^[how-to/algorithms/README.md:471-475, how-to/algorithms/README.md:505-522, how-to/algorithms/README.md:541-541]

## Sources

- [algorithms — přehled základních algoritmů pro vývojáře](how-to/algorithms/README.md)
