---
title: Statistiky komponent jako podklad pro refaktoring a migraci
summary: Přehled využití komponent pomáhá plánovat refaktoring či migraci a posoudit stav dat před větší změnou.
sources:
  - how-to/parse-json/README.md
kind: concept
createdAt: "2026-11-11T10:57:33.826Z"
updatedAt: "2026-11-11T10:57:33.826Z"
tags:
  - refaktoring
  - migrace
  - analýza-dat
aliases:
  - statistiky-komponent-jako-podklad-pro-refaktoring-a-migraci
  - SKJPPRAM
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Statistiky komponent jako podklad pro refaktoring a migraci

Statistiky využití komponent poskytují přehled o datech ve Strapi před refaktoringem, migrací nebo jinou větší změnou. Skript `index.py` zpracovává exportovaný JSON a počítá výskyty jednotlivých komponent napříč stránkami. Výsledky ukládá do samostatného JSON souboru. ^[how-to/parse-json/README.md:5-11]

## Co statistiky zachycují

Skript rekurzivně prochází stránky a hledá objekty s klíčem `__component`. Pro každý typ komponenty zaznamenává celkový počet výskytů a jejich rozdělení podle hodnoty `publicWeb` do kategorií `true`, `false` a `unknown`. Postup souvisí s [[Rekurzivní vyhledávání komponent v JSON|rekurzivním vyhledáváním komponent v JSON]] a s [[Rozdělení výskytů komponent podle publicWeb|rozdělením výskytů podle publicWeb]]. ^[how-to/parse-json/README.md:17-22]

Výstup obsahuje počet typů komponent (`total_component_types`), počet zpracovaných výskytů (`total_components_processed`) a seznam `components`. U jednotlivých komponent uvádí název (`name`), počet výskytů (`total_count`) a rozdělení podle `publicWeb` (`public_web_breakdown`); podrobněji viz [[Datový formát analýzy komponent]]. ^[how-to/parse-json/README.md:55-72]

## Využití při plánování změn

[[Analýza využití komponent ve Strapi]] pomáhá zjistit, které komponenty jsou nejpoužívanější, a získat přehled o stavu dat před větší změnou. Zdroj výslovně uvádí plánování refaktoringu a migrace komponent jako jeden z účelů skriptu. ^[how-to/parse-json/README.md:7-11]

## Získání statistik

Vstupem je Strapi JSON export se strukturou `{ "data": [ ...stránky... ] }`, jehož komponenty obsahují klíč `__component`. Skript vyžaduje Python 3. V závěrečném volání `count_components` se nastavuje cesta ke vstupnímu exportu a výstupnímu souboru; soubory mají být ve složce skriptu, případně lze zadat absolutní cesty. ^[how-to/parse-json/README.md:26-37, how-to/parse-json/README.md:76-80]

Po nastavení vstupu se skript spouští příkazem `python3 index.py`. Při uvedené konfiguraci jsou výsledky dostupné v souboru `component_statistics.json`. ^[how-to/parse-json/README.md:41-51]

## Sources

- [Parse JSON — počítání komponent ve Strapi stránkách](how-to/parse-json/README.md)
