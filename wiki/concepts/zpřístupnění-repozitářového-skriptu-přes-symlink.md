---
title: Zpřístupnění repozitářového skriptu přes symlink
summary: Symlink v `~/.claude/setup.sh` umožňuje spouštět skript uložený v repozitáři příkazem `bash ~/.claude/setup.sh`.
sources:
  - how-to/symlink-shortcut/README.md
kind: concept
createdAt: "2026-11-11T11:02:29.448Z"
updatedAt: "2026-11-11T11:02:29.448Z"
tags:
  - skripty
  - organizace-souborů
aliases:
  - zpřístupnění-repozitářového-skriptu-přes-symlink
  - ZRSPS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Zpřístupnění repozitářového skriptu přes symlink

[[Symbolický odkaz (symlink)]] umožňuje zpouštět skript uložený v repozitáři z jiného umístění bez zadávání celé cesty k originálu. Skript fyzicky zůstává na jednom místě a jeho úpravy se automaticky projeví i při použití odkazu; není potřeba nic kopírovat. ^[how-to/symlink-shortcut/README.md:5-10, how-to/symlink-shortcut/README.md:25-27]

## Vytvoření odkazu

Příkaz má tvar `ln -s ORIGINÁL ZKRATKA`. Přepínač `-s` vytváří symbolický odkaz. Pro zpřístupnění skriptu z repozitáře `direct-ai-skills` ve složce `.claude` použijte následující příkaz. ^[how-to/symlink-shortcut/README.md:14-38]

```bash
ln -s /Users/martin.adamec/work/direct/setup/direct-ai-skills/setup.sh \
      /Users/martin.adamec/.claude/setup.sh
```

Skript pak můžete spouštět přes vytvořený odkaz. Vytvoření symlinku stačí provést jednou; při dalších spuštěních použijete stejný příkaz. ^[how-to/symlink-shortcut/README.md:40-50]

```bash
bash ~/.claude/setup.sh
```

## Kontrola a trvalost

Pro [[Kontrola cíle symlinku|kontrolu cíle symlinku]] vypište obsah složky pomocí `ls -la ~/.claude/`. Řádek se šipkou `->` ukazuje, na jakou cestu odkaz směřuje. ^[how-to/symlink-shortcut/README.md:57-67]

```text
setup.sh -> /Users/martin.adamec/work/direct/setup/direct-ai-skills/setup.sh
```

Odkaz zůstává zachovaný i pro další použití. Přesunutí nebo přejmenování původního skriptu jej však znefunkční; odstraněním samotného symlinku zmizí přístup přes tuto zkratku. Souvisejícím tématem je [[Trvalost a nefunkčnost symlinků]]. ^[how-to/symlink-shortcut/README.md:47-53]

## Odstranění odkazu

Příkaz `rm ~/.claude/setup.sh` odstraní pouze symlink. Originální skript v repozitáři `direct-ai-skills` zůstane nedotčen. Viz také [[Odstranění symlinku bez smazání originálu]]. ^[how-to/symlink-shortcut/README.md:71-77]

```bash
rm ~/.claude/setup.sh
```

## Sources

- [Symlink Shortcut](how-to/symlink-shortcut/README.md)
