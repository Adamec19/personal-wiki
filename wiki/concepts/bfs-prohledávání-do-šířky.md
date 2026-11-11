---
title: BFS — prohledávání do šířky
summary: Průchod grafem používá frontu FIFO a množinu navštívených uzlů ke zpracování po úrovních a hledání nejkratších cest v neváženém grafu.
sources:
  - how-to/algorithms/README.md
kind: concept
createdAt: "2026-11-11T10:54:12.662Z"
updatedAt: "2026-11-11T10:54:12.662Z"
tags:
  - algoritmy
  - grafy
  - fronty
aliases:
  - bfs-prohledávání-do-šířky
  - B—PDŠ
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# BFS — prohledávání do šířky

BFS (Breadth-First Search) prochází graf po vrstvách: nejprve navštíví uzly ve vzdálenosti 1 od počátečního uzlu, poté ve vzdálenosti 2 a tak dále. Používá frontu s pravidlem FIFO — uzel přidaný dříve se také dříve zpracuje. ^[how-to/algorithms/README.md:362-364]

## Princip

Graf lze reprezentovat seznamem sousedů, kde má každý uzel uvedeny uzly, s nimiž je propojen hranami. BFS udržuje frontu uzlů čekajících na zpracování a množinu `visited`, která brání opakovaným návštěvám a zacyklení. ^[how-to/algorithms/README.md:336-357, how-to/algorithms/README.md:386-390]

Na začátku vložíme počáteční uzel do fronty a označíme jej jako navštívený. Poté opakovaně odebereme první uzel, zaznamenáme jej do výsledku a přidáme jeho dosud nenavštívené sousedy. Soused se označuje jako navštívený už při vložení do fronty, nikoli až při zpracování. Průchod končí vyprázdněním fronty. ^[how-to/algorithms/README.md:393-414]

## Příklad průchodu

V ukázkovém grafu má uzel `A` sousedy `B` a `C`, uzel `B` sousedy `D` a `E` a uzel `C` souseda `F`. BFS ze startu `A` zpracuje nejprve `A`, následně `B` a `C` a nakonec `D`, `E` a `F`. Výsledné pořadí je `A → B → C → D → E → F`. ^[how-to/algorithms/README.md:338-357, how-to/algorithms/README.md:366-384]

## Implementace v TypeScriptu

Typ `Graph` představuje mapu uzlů na seznamy sousedů. Funkce `bfs` vrací pořadí návštěv; frontu realizuje polem s operacemi `shift()` a `push()` a navštívené uzly ukládá do `Set`. ^[how-to/algorithms/README.md:347-348, how-to/algorithms/README.md:393-415]

```typescript
type Graph = Map<string, string[]>;

function bfs(graph: Graph, startNode: string): string[] {
  const visited = new Set<string>();
  const queue: string[] = [startNode];
  const visitOrder: string[] = [];

  visited.add(startNode);

  while (queue.length > 0) {
    const currentNode = queue.shift()!;
    visitOrder.push(currentNode);

    for (const neighbor of graph.get(currentNode) ?? []) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push(neighbor);
      }
    }
  }

  return visitOrder;
}
```

## Složitost a použití

Zdroj uvádí časovou složitost BFS jako `O(V + E)`. Souvislosti značení popisuje [[Časová složitost algoritmů a notace O]]. BFS se používá také pro hledání nejkratší cesty v neváženém grafu; uvedená implementace však vrací pouze pořadí návštěv. ^[how-to/algorithms/README.md:362-364, how-to/algorithms/README.md:393-415, how-to/algorithms/README.md:539-540]

Na rozdíl od BFS algoritmus [[DFS — prohledávání do hloubky]] postupuje co nejdále jednou cestou a teprve poté se vrací k dalším větvím. BFS naproti tomu zpracovává uzly po jednotlivých vrstvách. ^[how-to/algorithms/README.md:422-442]

## Sources

- [how-to/algorithms/README.md](how-to/algorithms/README.md)
