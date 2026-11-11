---
title: Kontrola cíle symlinku
summary: Výpis `ls -la` zobrazuje symbolické odkazy ve tvaru `název -> cíl`, což umožňuje ověřit jejich přítomnost a cílovou cestu.
sources:
  - how-to/symlink-shortcut/README.md
kind: concept
createdAt: "2026-11-11T11:02:37.199Z"
updatedAt: "2026-11-11T11:02:37.199Z"
tags:
  - terminál
  - diagnostika
aliases:
  - kontrola-cíle-symlinku
  - KCS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Kontrola cíle symlinku

Cíl [[Symbolický odkaz (symlink)|symlinku]] lze zkontrolovat ve výpisu adresáře pomocí `ls -la`. Symlink odkazuje na originální soubor uložený na jiném místě; není jeho kopií. ^[how-to/symlink-shortcut/README.md:5-10, how-to/symlink-shortcut/README.md:57-67]

## Zobrazení cíle

Pro kontrolu symlinku ve složce `.claude` použij následující příkaz. ^[how-to/symlink-shortcut/README.md:57-61]

```bash
ls -la ~/.claude/
```

Ve výpisu vyhledej řádek s názvem symlinku. Pro odkaz `setup.sh` může vypadat takto. ^[how-to/symlink-shortcut/README.md:63-66]

```text
setup.sh -> /Users/martin.adamec/work/direct/setup/direct-ai-skills/setup.sh
```

Název vlevo označuje symlink a cesta za šipkou `->` ukazuje jeho cíl. V tomto příkladu odkazuje `setup.sh` ve složce `.claude` na skript v repozitáři `direct-ai-skills`. ^[how-to/symlink-shortcut/README.md:29-38, how-to/symlink-shortcut/README.md:63-67]

## Souvislost s funkčností odkazu

Přesunutí nebo přejmenování originálního skriptu způsobí, že symlink přestane fungovat. Zobrazená cílová cesta je proto důležitá při kontrole [[Trvalost a nefunkčnost symlinků|nefunkčního odkazu]]. ^[how-to/symlink-shortcut/README.md:49-53, how-to/symlink-shortcut/README.md:63-67]

## Sources

- [Symlink Shortcut](how-to/symlink-shortcut/README.md)
