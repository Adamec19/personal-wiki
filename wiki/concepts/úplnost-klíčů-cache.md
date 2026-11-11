---
title: Úplnost klíčů cache
summary: Zahrň do klíče cache všechny parametry ovlivňující výsledek, aby se nezaměňovala data různých variant dotazu.
sources:
  - how-to/react-cheat-sheet/06-api-and-data.md
kind: concept
createdAt: "2026-11-11T10:59:25.967Z"
updatedAt: "2026-11-11T10:59:25.967Z"
tags:
  - cache
  - dotazy
aliases:
  - úplnost-klíčů-cache
  - ÚKC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Úplnost klíčů cache

Klíč cache musí obsahovat všechny parametry, které mění výsledek dotazu. Pokud některý chybí, komponenta může zobrazit data z jiné varianty dotazu. ^[how-to/react-cheat-sheet/06-api-and-data.md:57-62]

## Příklad

Pro dotaz na uživatele, jehož výsledek závisí na organizaci, vyhledávání a stránce, zahrnuje klíč všechny tři parametry: ^[how-to/react-cheat-sheet/06-api-and-data.md:59-62]

```tsx
queryKey: ["users", { organizationId, search, page }]
```

Úplnost klíče souvisí se [[Správa serverových dat pomocí query/cache vrstvy|správou serverových dat pomocí query/cache vrstvy]]: různé varianty dotazu musí být v cache rozlišitelné podle všech parametrů ovlivňujících výsledek. ^[how-to/react-cheat-sheet/06-api-and-data.md:57-62]

## Sources

- [API and Data](how-to/react-cheat-sheet/06-api-and-data.md)
