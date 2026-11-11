---
title: Odstranění symlinku bez smazání originálu
summary: Příkaz `rm` použitý na cestu samotného symlinku odstraní odkaz a ponechá původní soubor nedotčený.
sources:
  - how-to/symlink-shortcut/README.md
kind: concept
createdAt: "2026-11-11T11:02:38.232Z"
updatedAt: "2026-11-11T11:02:38.232Z"
tags:
  - symbolické-odkazy
  - správa-souborů
aliases:
  - odstranění-symlinku-bez-smazání-originálu
  - OSBSO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Odstranění symlinku bez smazání originálu

[[Symbolický odkaz (symlink)]] je zkratka odkazující na originální soubor, který fyzicky existuje na jiném místě. Odstraněním samotného symlinku se originál nesmaže. ^[how-to/symlink-shortcut/README.md:5-10, how-to/symlink-shortcut/README.md:71-77]

## Kontrola před odstraněním

Cíl odkazu lze ověřit výpisem obsahu složky. V příkladu se symlink nachází ve složce `~/.claude/`. ^[how-to/symlink-shortcut/README.md:57-65]

```bash
ls -la ~/.claude/
```

Výpis obsahuje řádek v následujícím tvaru; šipka `->` označuje, kam symlink ukazuje. Podrobněji viz [[Kontrola cíle symlinku]]. ^[how-to/symlink-shortcut/README.md:63-67]

```text
setup.sh -> /Users/martin.adamec/work/direct/setup/direct-ai-skills/setup.sh
```

## Odstranění odkazu

Pro odstranění použij `rm` s cestou k samotnému symlinku. Následující příkaz smaže `~/.claude/setup.sh`, zatímco originální skript v repozitáři `direct-ai-skills` zůstane nedotčen. ^[how-to/symlink-shortcut/README.md:71-77]

```bash
rm ~/.claude/setup.sh
```

Po smazání symlinku již tato zkratka nebude fungovat pro spouštění skriptu příkazem `bash ~/.claude/setup.sh`. ^[how-to/symlink-shortcut/README.md:49-53]

## Sources

- [Symlink Shortcut](how-to/symlink-shortcut/README.md)
