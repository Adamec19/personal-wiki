---
title: Snippets a generátory
summary: Opakující se struktury souborů a pravidla lze zachytit pomocí snippets nebo generátorů.
sources:
  - how-to/react-cheat-sheet/README.md
kind: concept
createdAt: "2026-11-11T11:01:22.396Z"
updatedAt: "2026-11-11T11:01:22.396Z"
tags:
  - scaffolding
  - automatizace
aliases:
  - snippets-a-generátory
  - SAG
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Snippets a generátory

Snippets a generátory pomáhají při opakování stejné struktury souborů a pravidel v React aplikaci. Jsou vhodné při vytváření scaffoldu; component snippets slouží k rychlému založení Contextu, Provideru, hooku nebo komponenty. ^[how-to/react-cheat-sheet/README.md:18-20, how-to/react-cheat-sheet/README.md:29-29]

## Kdy je použít

Snippet nebo generátor přidej, když se struktura a pravidla opakují. Ještě před zaváděním abstrakcí je však potřeba navrhnout hranice a datový tok. Znovupoužitelná komponenta má být jednoduchá na použití a nemá znát business pravidla svého konzumenta; souvisí s tím [[Návrh znovupoužitelných komponent]] a [[Oddělení business logiky od generického UI]]. ^[how-to/react-cheat-sheet/README.md:29-33]

## Konvence generovaného kódu

Ukázky a snippets v průvodci zapisují komponenty a [[custom-hooks|Custom Hooks]] jako `const` arrow functions. Používají pojmenované exporty umístěné na konci souboru. Tento styl představuje projektovou konvenci, kterou je potřeba přizpůsobit konkrétnímu codebase; viz [[Projektové konvence zápisu React kódu]]. ^[how-to/react-cheat-sheet/README.md:5-5, how-to/react-cheat-sheet/README.md:35-59]

Běžné pomocné funkce mohou mít vlastní projektovou konvenci. Ukázky průvodce u nich přesto preferují stejný arrow-function zápis kvůli konzistenci. ^[how-to/react-cheat-sheet/README.md:59-59]

## Sources

- [React Cheat Sheet](how-to/react-cheat-sheet/README.md)
