---
title: DFS — prohledávání do hloubky
summary: Průchod grafem pomocí rekurze nebo zásobníku prozkoumá větev do hloubky před návratem k dalším sousedům.
sources:
  - how-to/algorithms/README.md
kind: concept
createdAt: "2026-11-11T10:54:19.013Z"
updatedAt: "2026-11-11T10:54:19.013Z"
tags:
  - algoritmy
  - grafy
  - rekurze
aliases:
  - dfs-prohledávání-do-hloubky
  - D—PDH
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# DFS — prohledávání do hloubky

DFS (Depth-First Search) je algoritmus pro průchod grafem, který postupuje co nejdál jednou cestou a teprve potom se vrací k dalším větvím. Používá rekurzi nebo zásobník. Na rozdíl od [[BFS — prohledávání do šířky]] nemusí nejprve navštívit nejbližší uzly. ^[how-to/algorithms/README.md:422-424]

## Princip a průběh

Při návštěvě uzlu jej algoritmus označí jako navštívený a přidá do výsledného pořadí. Poté postupně prochází jeho sousedy a pro každého dosud nenavštíveného souseda rekurzivně pokračuje do hloubky. Po návratu z rekurze zpracuje dalšího souseda. Množina `visited` zabraňuje opakovanému navštěvování uzlů. ^[how-to/algorithms/README.md:445-463]

V ukázkovém grafu má uzel A sousedy B a C, uzel B dále sousedy D a E a uzel C souseda F. Při startu z A a uvedeném pořadí sousedů navštíví DFS uzly v pořadí `A → B → D → E → C → F`. BFS by tentýž graf prošel po úrovních v pořadí `A → B → C → D → E → F`. ^[how-to/algorithms/README.md:336-357, how-to/algorithms/README.md:426-442]

## Implementace v TypeScriptu

Graf je reprezentován jako seznam sousedů typu `Map<string, string[]>`. Funkce `dfs` přijímá graf a počáteční uzel a vrací pořadí návštěv. Vnořená funkce `traverse` provádí rekurzivní průchod; výraz `graph.get(currentNode) ?? []` umožňuje zpracovat i uzel bez seznamu sousedů. ^[how-to/algorithms/README.md:336-357, how-to/algorithms/README.md:445-464]

```typescript
type Graph = Map<string, string[]>;

function dfs(graph: Graph, startNode: string): string[] {
  const visited = new Set<string>();
  const visitOrder: string[] = [];

  function traverse(currentNode: string): void {
    visited.add(currentNode);
    visitOrder.push(currentNode);

    for (const neighbor of graph.get(currentNode) ?? []) {
      if (!visited.has(neighbor)) {
        traverse(neighbor);
      }
    }
  }

  traverse(startNode);
  return visitOrder;
}
```

## Složitost a použití

Časová složitost DFS je **O(V + E)**, kde V označuje počet uzlů a E počet hran grafu. Zdroj uvádí DFS jako vhodný algoritmus pro průchod stromem a detekci cyklů. Pro hledání nejkratší cesty v neváženém grafu uvádí BFS. Související téma je [[Časová složitost algoritmů a notace O]]. ^[how-to/algorithms/README.md:336-336, how-to/algorithms/README.md:422-424, how-to/algorithms/README.md:531-541]

## Sources

- [algorithms — přehled základních algoritmů pro vývojáře](how-to/algorithms/README.md)
