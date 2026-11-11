---
title: Komponenta prázdného stavu
summary: Typovaná komponenta EmptyState zobrazuje nadpis, volitelný popis a akci a propojuje sekci s nadpisem pomocí aria-labelledby.
sources:
  - how-to/react-cheat-sheet/10-component-snippets.md
kind: concept
createdAt: "2026-11-11T11:00:36.474Z"
updatedAt: "2026-11-11T11:00:36.474Z"
tags:
  - react
  - components
  - accessibility
aliases:
  - komponenta-prázdného-stavu
  - KPS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Komponenta prázdného stavu

Komponenta prázdného stavu (`EmptyState`) zobrazuje sdělení při absenci dat, například když hledání nevrátí žádné výsledky. Ukázka ji vykresluje až po vyhodnocení načítání a chyby, pokud `data` neobsahují žádné položky. Souvisí s tématem [[Explicitní vykreslování asynchronních stavů]]. ^[how-to/react-cheat-sheet/10-component-snippets.md:98-108]

## Veřejný kontrakt

Ukázkový kontrakt `EmptyStateProps` obsahuje povinný nadpis `title: string`, volitelný popis `description?: string` a volitelný obsah pro akci `action?: React.ReactNode`. Konzument tak určuje text i případný ovládací prvek prostřednictvím props; viz [[Component Props as a Public Contract]]. ^[how-to/react-cheat-sheet/10-component-snippets.md:8-14]

## Vykreslení a přístupnost

Komponenta používá element `<section>` propojený pomocí `aria-labelledby="empty-state-title"` s nadpisem `<h2 id="empty-state-title">`. Popis vykresluje podmíněně a za ním vkládá předanou akci. ^[how-to/react-cheat-sheet/10-component-snippets.md:14-22]

Ukázka je výchozí kostra, kterou je potřeba přizpůsobit požadavkům konkrétní aplikace na přístupnost, design systém, zpracování chyb a datový kontrakt. Při návrhu pomáhá také [[Kontrolní seznam návrhu komponent]], zejména ověření jednoho účelu, malého typovaného kontraktu a chování pro klávesnici a čtečky obrazovky. ^[how-to/react-cheat-sheet/10-component-snippets.md:3-3, how-to/react-cheat-sheet/10-component-snippets.md:128-135]

## Sources

- [Component Snippets](how-to/react-cheat-sheet/10-component-snippets.md)
