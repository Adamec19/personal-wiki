---
title: Analýza využití komponent ve Strapi
summary: Script index.py počítá výskyty jednotlivých komponent napříč stránkami exportovanými ze Strapi a ukládá statistiky do JSON.
sources:
  - how-to/parse-json/README.md
kind: concept
createdAt: "2026-11-11T10:57:22.528Z"
updatedAt: "2026-11-11T10:57:22.528Z"
tags:
  - strapi
  - analýza-dat
  - python
aliases:
  - analýza-využití-komponent-ve-strapi
  - AVKVS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Analýza využití komponent ve Strapi

Analýza využití komponent ve Strapi zjišťuje, kolikrát se jednotlivé komponenty vyskytují napříč stránkami exportovanými do JSON. Skript `index.py` export zpracuje a uloží souhrnné statistiky do nového JSON souboru. ^[how-to/parse-json/README.md:3-5]

## Účel analýzy

Statistiky pomáhají určit nejpoužívanější komponenty a získat přehled o datech před větší změnou. Slouží také jako podklad pro plánování refaktoringu nebo migrace; souvisejícím tématem jsou [[Statistiky komponent jako podklad pro refaktoring a migraci]]. ^[how-to/parse-json/README.md:7-11]

## Způsob zpracování

Skript načte vstupní JSON a rekurzivně prochází každou stránku. Vyhledává objekty s klíčem `__component`, pro jednotlivé komponenty počítá celkový počet výskytů a rozděluje je podle hodnoty `publicWeb` do kategorií `true`, `false` a `unknown`. Postup rozvíjejí témata [[Rekurzivní vyhledávání komponent v JSON]] a [[Rozdělení výskytů komponent podle publicWeb]]. ^[how-to/parse-json/README.md:15-22]

## Vstup a spuštění

Skript vyžaduje Python 3 a export ve struktuře `{ "data": [ ...stránky... ] }`. Každá komponenta musí obsahovat klíč `__component`. ^[how-to/parse-json/README.md:76-80]

Na konci `index.py` se nastavuje volání `count_components`: první argument označuje vstupní export a druhý výstupní soubor se statistikami. Soubory mají být ve stejné složce jako skript, případně je potřeba zadat absolutní cesty. ^[how-to/parse-json/README.md:26-37]

```python
count_components('strapi_pages.json', 'component_statistics.json')
```

Po přípravě exportu a případné úpravě názvu vstupního souboru se skript spouští příkazem `python3 index.py` ze složky se skriptem. Při uvedeném nastavení vznikne soubor `component_statistics.json`. ^[how-to/parse-json/README.md:41-51]

## Výstupní statistiky

Výstup obsahuje počet typů komponent (`total_component_types`), celkový počet zpracovaných výskytů (`total_components_processed`) a seznam `components`. U každé komponenty uvádí název (`name`), počet výskytů (`total_count`) a rozdělení podle `publicWeb` (`public_web_breakdown`). Strukturu popisuje také [[Datový formát analýzy komponent]]. ^[how-to/parse-json/README.md:55-72]

## Sources

- [Parse JSON — počítání komponent ve Strapi stránkách](how-to/parse-json/README.md)
