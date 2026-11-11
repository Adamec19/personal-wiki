---
title: Rozdělení výskytů komponent podle publicWeb
summary: Pro každou komponentu se vedle celkového počtu výskytů sleduje rozdělení podle hodnot publicWeb true, false a unknown.
sources:
  - how-to/parse-json/README.md
kind: concept
createdAt: "2026-11-11T10:57:29.113Z"
updatedAt: "2026-11-11T10:57:29.113Z"
tags:
  - strapi
  - statistiky
  - publicWeb
aliases:
  - rozdělení-výskytů-komponent-podle-publicweb
  - RVKPP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Rozdělení výskytů komponent podle publicWeb

Rozdělení podle `publicWeb` je součástí statistik, které script `index.py` vytváří z exportovaného JSON ze Strapi. Pro každý typ komponenty počítá celkový počet výskytů a jejich rozdělení podle hodnoty `publicWeb` do kategorií `true`, `false` a `unknown`. ^[how-to/parse-json/README.md:17-22]

## Zpracování exportu

Script načte vstupní JSON a rekurzivně prochází každou stránku. Komponenty rozpoznává podle klíče `__component`; vstup přitom musí mít strukturu `{ "data": [ ...stránky... ] }`. S tímto postupem souvisí [[Rekurzivní vyhledávání komponent v JSON]]. ^[how-to/parse-json/README.md:17-21, how-to/parse-json/README.md:78-80]

## Podoba výsledků

Výsledky se ukládají do výstupního JSON souboru. Záznam komponenty obsahuje její název v `name`, celkový počet výskytů v `total_count` a rozdělení podle `publicWeb` v objektu `public_web_breakdown`. Podrobněji souvisí s tématem [[Datový formát analýzy komponent]]. ^[how-to/parse-json/README.md:22-22, how-to/parse-json/README.md:55-72]

Ukázkový výstup uvádí komponentu `sections.hero` s celkem 45 výskyty: 30 v kategorii `"true"` a 15 v kategorii `"false"`. Kategorie `unknown` je uvedena v popisu zpracování, ale v ukázkovém JSON není zastoupena; zdroj neupřesňuje, kdy se do ní výskyt zařazuje. ^[how-to/parse-json/README.md:19-21, how-to/parse-json/README.md:63-68]

## Využití

Statistiky slouží k přehledu o používání komponent a stavu dat před větší změnou, například při plánování refaktoringu nebo migrace. Rozdělení podle `publicWeb` doplňuje celkové počty v rámci [[Analýza využití komponent ve Strapi|analýzy využití komponent ve Strapi]]. ^[how-to/parse-json/README.md:5-11, how-to/parse-json/README.md:19-21]

## Sources

- [how-to/parse-json/README.md](how-to/parse-json/README.md)
