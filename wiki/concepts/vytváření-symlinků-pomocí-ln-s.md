---
title: Vytváření symlinků pomocí ln -s
summary: Příkaz `ln -s ORIGINÁL ZKRATKA` vytvoří symbolický odkaz na zadaný cíl.
sources:
  - how-to/symlink-shortcut/README.md
kind: concept
createdAt: "2026-11-11T11:02:26.299Z"
updatedAt: "2026-11-11T11:02:26.299Z"
tags:
  - terminál
  - symbolické-odkazy
aliases:
  - vytváření-symlinků-pomocí-ln-s
  - VSPL-
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Vytváření symlinků pomocí ln -s

[[Symbolický odkaz (symlink)|Symlink]] je zkratka na soubor, který fyzicky existuje na jiném místě. Nevytváří kopii: úpravy originálu se automaticky projeví i při přístupu přes symlink. ^[how-to/symlink-shortcut/README.md:5-10]

## Základní syntaxe

Symlink vytvoříš příkazem `ln -s ORIGINÁL ZKRATKA`. První cesta určuje originál, druhá umístění vytvářeného odkazu. Volba `-s` znamená symbolický odkaz. ^[how-to/symlink-shortcut/README.md:14-21]

```bash
ln -s ORIGINÁL ZKRATKA
```

## Příklad: zpřístupnění skriptu ze složky .claude

Skript uložený v repozitáři `direct-ai-skills` lze zpřístupnit jako `~/.claude/setup.sh`, aby jej bylo možné spouštět bez zadávání celé původní cesty. ^[how-to/symlink-shortcut/README.md:25-38]

```bash
ln -s /Users/martin.adamec/work/direct/setup/direct-ai-skills/setup.sh \
      /Users/martin.adamec/.claude/setup.sh
```

Po vytvoření odkazu lze skript spustit následujícím příkazem. Symlink stačí vytvořit jednou; pro další spuštění se příkaz `ln -s` neopakuje. ^[how-to/symlink-shortcut/README.md:40-50]

```bash
bash ~/.claude/setup.sh
```

## Kontrola a odstranění

Pro [[Kontrola cíle symlinku|kontrolu cíle symlinku]] zobraz obsah složky příkazem `ls -la ~/.claude/`. Řádek ve tvaru `setup.sh -> /cesta/k/setup.sh` ukazuje, kam odkaz směřuje. ^[how-to/symlink-shortcut/README.md:57-67]

Přesunutí nebo přejmenování originálního skriptu způsobí, že odkaz přestane fungovat; souvisí s tím [[Trvalost a nefunkčnost symlinků]]. Samotný symlink lze odstranit příkazem `rm ~/.claude/setup.sh`, přičemž originál zůstane nedotčen. Podrobněji viz [[Odstranění symlinku bez smazání originálu]]. ^[how-to/symlink-shortcut/README.md:49-53, how-to/symlink-shortcut/README.md:71-77]

## Sources

- [Symlink Shortcut](how-to/symlink-shortcut/README.md)
