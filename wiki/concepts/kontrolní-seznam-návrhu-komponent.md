---
title: Kontrolní seznam návrhu komponent
summary: Návrh komponenty ověřuje jeden účel, malý typovaný kontrakt, explicitní řízení stavu, přístupnost, oddělení business logiky a vhodnost Contextu oproti props a kompozici.
sources:
  - how-to/react-cheat-sheet/10-component-snippets.md
kind: concept
createdAt: "2026-11-11T11:01:04.115Z"
updatedAt: "2026-11-11T11:01:04.115Z"
tags:
  - components
  - api-design
  - accessibility
  - code-quality
aliases:
  - kontrolní-seznam-návrhu-komponent
  - KSNK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Kontrolní seznam návrhu komponent

Kontrolní seznam pomáhá posoudit účel komponenty, její veřejný kontrakt, správu stavu, přístupnost a oddělení odpovědností. Výchozí snippety je nutné přizpůsobit accessibility, design systému, zpracování chyb a datovému kontraktu konkrétní aplikace. ^[how-to/react-cheat-sheet/10-component-snippets.md:3-3, how-to/react-cheat-sheet/10-component-snippets.md:128-135]

## Otázky při návrhu

- **Jeden účel:** Má komponenta jednu jasnou odpovědnost?
- **Malý a typovaný kontrakt:** Jsou její veřejné props přehledné a typované? Viz [[Component Props as a Public Contract]].
- **Explicitní správa stavu:** Je zřejmé, zda se komponenta chová jako controlled, nebo uncontrolled? Viz [[Controlled Components and State Ownership]].
- **Přístupnost:** Je vyřešené ovládání klávesnicí a chování pro čtečky obrazovky?
- **Oddělení business logiky:** Neobsahuje generická komponenta logiku konkrétní aplikace? Viz [[Oddělení business logiky od generického UI]].
- **Přiměřené sdílení dat:** Je skutečně potřeba Context, nebo stačí props a composition? Viz [[React Context and Providers]] a [[Composition Through Children]].

Tyto otázky tvoří základní kontrolu návrhu komponenty před jejím použitím v aplikaci. ^[how-to/react-cheat-sheet/10-component-snippets.md:128-135]

## Praktické vodítko

U [[Controlled input|controlled inputu]] ukázka vyjadřuje veřejný kontrakt pomocí `value: string` a callbacku `onChange: (value: string) => void`. Komponenta přijímá hodnotu přes props a předává změnu volajícímu. ^[how-to/react-cheat-sheet/10-component-snippets.md:78-95]

Při rozhodování o composition jsou [[Compound components|compound components]] vhodné pro části se společným layoutem, jejichž obsah určuje konzument. Pokud části skutečně nepatří k sobě, stačí `children` a běžné komponenty. ^[how-to/react-cheat-sheet/10-component-snippets.md:27-47]

U komponent zobrazujících asynchronní data je vhodné zkontrolovat explicitní pořadí stavů: načítání, chyba, prázdný výsledek a data. Takové [[Explicitní vykreslování asynchronních stavů|vykreslování asynchronních stavů]] je čitelnější než mnoho vnořených ternárních výrazů. ^[how-to/react-cheat-sheet/10-component-snippets.md:98-108]

## Sources

- [Component Snippets](how-to/react-cheat-sheet/10-component-snippets.md)
