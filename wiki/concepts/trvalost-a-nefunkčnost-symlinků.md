---
title: Trvalost a nefunkčnost symlinků
summary: Vytvořený symlink přetrvává pro opakované použití; přesunutí nebo přejmenování cílového skriptu může způsobit jeho nefunkčnost.
sources:
  - how-to/symlink-shortcut/README.md
kind: concept
createdAt: "2026-11-11T11:02:35.194Z"
updatedAt: "2026-11-11T11:02:35.194Z"
tags:
  - symbolické-odkazy
  - životní-cyklus
aliases:
  - trvalost-a-nefunkčnost-symlinků
  - TANS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Trvalost a nefunkčnost symlinků

[[Symbolický odkaz (symlink)]] je zástupce, který odkazuje na originální soubor na jiném místě. Soubor fyzicky existuje pouze jednou; jeho úpravy se automaticky projeví i při přístupu přes symlink, bez kopírování. ^[how-to/symlink-shortcut/README.md:5-10]

## Trvalost odkazu

Symlink se vytváří příkazem `ln -s ORIGINÁL ZKRATKA`. Příkaz stačí provést jednou a vytvořený odkaz zůstává trvale k dispozici. Pro opakované spuštění odkazovaného skriptu není nutné symlink vytvářet znovu. ^[how-to/symlink-shortcut/README.md:14-21, how-to/symlink-shortcut/README.md:49-50]

Například skript zpřístupněný symlinkem v adresáři `.claude` lze opakovaně spouštět tímto příkazem: ^[how-to/symlink-shortcut/README.md:40-43, how-to/symlink-shortcut/README.md:49-50]

```bash
bash ~/.claude/setup.sh
```

## Kdy odkaz přestane fungovat

Přesunutí nebo přejmenování originálního skriptu způsobí, že symlink přestane fungovat. Přístup přes zkratku přestane být dostupný také tehdy, když samotný symlink smažeme. ^[how-to/symlink-shortcut/README.md:51-53]

## Kontrola a odstranění

Pro [[Kontrola cíle symlinku|kontrolu cíle symlinku]] lze vypsat obsah adresáře příkazem `ls -la ~/.claude/`. Zápis ve tvaru `setup.sh -> /cesta/k/originálu/setup.sh` ukazuje, kam odkaz směřuje; šipka `->` označuje symlink a jeho cíl. ^[how-to/symlink-shortcut/README.md:57-67]

[[Odstranění symlinku bez smazání originálu]] lze provést příkazem `rm ~/.claude/setup.sh`. Odstraní se pouze zkratka, zatímco původní skript zůstane nedotčen. ^[how-to/symlink-shortcut/README.md:71-77]

## Sources

- [how-to/symlink-shortcut/README.md](how-to/symlink-shortcut/README.md)
