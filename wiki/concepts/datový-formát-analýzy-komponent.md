---
title: Datový formát analýzy komponent
summary: Vstup obsahuje stránky v poli data; výstup uvádí počet typů komponent, počet zpracovaných výskytů a statistiky jednotlivých komponent.
sources:
  - how-to/parse-json/README.md
kind: concept
createdAt: "2026-11-11T10:57:32.805Z"
updatedAt: "2026-11-11T10:57:32.805Z"
tags:
  - json
  - datový-formát
  - statistiky
aliases:
  - datový-formát-analýzy-komponent
  - DFAK
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Datový formát analýzy komponent

Analýza komponent pracuje s JSON exportem stránek ze Strapi a vytváří samostatný JSON soubor se statistikami. Skript `index.py` počítá výskyty jednotlivých komponent napříč stránkami. ^[how-to/parse-json/README.md:3-5]

## Vstupní struktura

Vstupní JSON musí obsahovat objekt s polem `data`, které představuje jednotlivé stránky: `{ "data": [ ...stránky... ] }`. Každá komponenta musí mít klíč `__component`, podle kterého ji skript při rekurzivním průchodu rozpoznává. Viz [[Rekurzivní vyhledávání komponent v JSON]]. ^[how-to/parse-json/README.md:17-18, how-to/parse-json/README.md:78-80]

## Výstupní struktura

Výstup obsahuje souhrnné počty a pole `components` se statistikami jednotlivých typů komponent. Ukázka uvádí tento formát: ^[how-to/parse-json/README.md:55-72]

```json
{
  "total_component_types": 12,
  "total_components_processed": 347,
  "components": [
    {
      "name": "sections.hero",
      "total_count": 45,
      "public_web_breakdown": {
        "true": 30,
        "false": 15
      }
    }
  ]
}
```

Pole `total_component_types` udává počet typů komponent a `total_components_processed` celkový počet zpracovaných výskytů. Každý záznam v poli `components` obsahuje název komponenty v `name`, počet jejích výskytů v `total_count` a rozdělení podle hodnoty `publicWeb` v `public_web_breakdown`. ^[how-to/parse-json/README.md:19-21, how-to/parse-json/README.md:59-68]

Rozdělení podle `publicWeb` počítá s kategoriemi `true`, `false` a `unknown`. Ukázkový výstup obsahuje pouze klíče `"true"` a `"false"`; podobu záznamu pro `unknown` zdroj neukazuje. Podrobněji viz [[Rozdělení výskytů komponent podle publicWeb]]. ^[how-to/parse-json/README.md:19-21, how-to/parse-json/README.md:65-68]

## Soubory a konfigurace

Vstupní a výstupní soubor se zadávají jako první a druhý argument funkce `count_components`, například `count_components('strapi_pages.json', 'component_statistics.json')`. Oba soubory mají být ve stejné složce jako skript, případně lze zadat absolutní cesty. ^[how-to/parse-json/README.md:28-37]

Výsledná data slouží k přehledu o využití komponent a jako podklad pro plánování refaktoringu nebo migrace. Viz [[Statistiky komponent jako podklad pro refaktoring a migraci]]. ^[how-to/parse-json/README.md:7-11]

## Sources

- [how-to/parse-json/README.md](how-to/parse-json/README.md)
