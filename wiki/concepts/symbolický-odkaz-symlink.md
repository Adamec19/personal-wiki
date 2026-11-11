---
title: Symbolický odkaz (symlink)
summary: Odkaz na soubor na jiném místě souborového systému, který zpřístupňuje originál bez kopírování a odráží jeho změny.
sources:
  - how-to/symlink-shortcut/README.md
kind: concept
createdAt: "2026-11-11T11:02:23.643Z"
updatedAt: "2026-11-11T11:02:23.643Z"
tags:
  - souborový-systém
  - symbolické-odkazy
aliases:
  - symbolický-odkaz-symlink
  - SO(
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Symbolický odkaz (symlink)

Symbolický odkaz neboli symlink je zástupce na úrovni souborového systému. Soubor fyzicky existuje na jednom místě a symlink na něj odkazuje z jiného místa. Úpravy originálu se automaticky projeví i při přístupu přes symlink, takže není potřeba soubor kopírovat. ^[how-to/symlink-shortcut/README.md:5-10]

## Vytvoření

Symlink se vytváří příkazem `ln -s ORIGINÁL ZKRATKA`. Příkaz `ln` vytváří odkaz a přepínač `-s` určuje, že jde o symbolický odkaz. První cesta označuje originál, druhá umístění symlinku. ^[how-to/symlink-shortcut/README.md:14-21]

```bash
ln -s ORIGINÁL ZKRATKA
```

Například skript uložený v repozitáři `direct-ai-skills` lze zpřístupnit ze složky `.claude` a následně jej spouštět přes tuto kratší cestu. ^[how-to/symlink-shortcut/README.md:25-43]

```bash
ln -s /Users/martin.adamec/work/direct/setup/direct-ai-skills/setup.sh \
      /Users/martin.adamec/.claude/setup.sh

bash ~/.claude/setup.sh
```

## Trvalost a dostupnost cíle

Symlink stačí vytvořit jednou a zůstává na místě pro další použití. Přesunutí nebo přejmenování původního skriptu způsobí, že odkaz přestane fungovat; odstraněním samotného symlinku zanikne přístup přes tuto zkratku. Podrobněji viz [[Trvalost a nefunkčnost symlinků]]. ^[how-to/symlink-shortcut/README.md:47-53]

## Kontrola cíle

Existenci symlinku a cestu, na kterou ukazuje, lze ověřit výpisem `ls -la`. Šipka `->` ve výpisu odděluje název odkazu od jeho cíle. Viz také [[Kontrola cíle symlinku]]. ^[how-to/symlink-shortcut/README.md:57-67]

```bash
ls -la ~/.claude/
```

Příklad řádku ve výpisu:

```text
setup.sh -> /Users/martin.adamec/work/direct/setup/direct-ai-skills/setup.sh
```

## Odstranění

Příkaz `rm` použitý na cestu symlinku odstraní pouze odkaz; původní soubor zůstane nedotčen. Viz [[Odstranění symlinku bez smazání originálu]]. ^[how-to/symlink-shortcut/README.md:71-77]

```bash
rm ~/.claude/setup.sh
```

## Sources

- [Symlink Shortcut](how-to/symlink-shortcut/README.md)
