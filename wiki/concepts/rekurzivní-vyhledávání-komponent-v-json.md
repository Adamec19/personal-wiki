---
title: Rekurzivní vyhledávání komponent v JSON
summary: Script rekurzivně prochází strukturu každé stránky a identifikuje komponenty podle klíče __component.
sources:
  - how-to/parse-json/README.md
kind: concept
createdAt: "2026-11-11T10:57:28.676Z"
updatedAt: "2026-11-11T10:57:28.676Z"
tags:
  - json
  - rekurze
  - strapi
aliases:
  - rekurzivní-vyhledávání-komponent-v-json
  - RVKVJ
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Rekurzivní vyhledávání komponent v JSON

Rekurzivní vyhledávání komponent je postup, při kterém script `index.py` prochází jednotlivé stránky exportované ze Strapi a hledá objekty s klíčem `__component`. Nalezené komponenty započítává do statistik napříč všemi stránkami. ^[how-to/parse-json/README.md:5-5, how-to/parse-json/README.md:17-22]

## Vstup a průběh zpracování

Vstupní JSON musí mít strukturu `{ "data": [ ...stránky... ] }`. Každá komponenta musí obsahovat klíč `__component`, podle kterého ji script při rekurzivním průchodu rozpozná. ^[how-to/parse-json/README.md:78-80]

Script načte export, rekurzivně projde každou stránku a pro každou nalezenou komponentu spočítá celkový počet výskytů i rozdělení podle hodnoty `publicWeb` do kategorií `true`, `false` a `unknown`. Výsledky uloží do výstupního JSON souboru; členění podrobněji souvisí s tématem [[Rozdělení výskytů komponent podle publicWeb]]. ^[how-to/parse-json/README.md:17-22]

## Spuštění a výstup

Vstupní a výstupní soubor se nastavují argumenty volání `count_components('strapi_pages.json', 'component_statistics.json')` na konci souboru `index.py`. Soubory mají být ve stejné složce jako script, případně je nutné zadat absolutní cesty. Script se spouští příkazem `python3 index.py`. ^[how-to/parse-json/README.md:28-37, how-to/parse-json/README.md:43-49]

Výstup obsahuje počet typů komponent (`total_component_types`), celkový počet zpracovaných výskytů (`total_components_processed`) a seznam `components`. U každé komponenty uvádí název, celkový počet a rozdělení podle `publicWeb`; podobu výsledku popisuje také [[Datový formát analýzy komponent]]. ^[how-to/parse-json/README.md:55-72]

## Využití

Výsledné statistiky pomáhají určit nejpoužívanější komponenty a získat přehled o datech před větší změnou. Jsou podkladem pro [[Analýza využití komponent ve Strapi|analýzu využití komponent]] a pro [[Statistiky komponent jako podklad pro refaktoring a migraci|plánování refaktoringu nebo migrace]]. ^[how-to/parse-json/README.md:7-11]

## Sources

- [Parse JSON — počítání komponent ve Strapi stránkách](how-to/parse-json/README.md)
