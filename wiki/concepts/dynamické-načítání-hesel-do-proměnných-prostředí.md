---
title: Dynamické načítání hesel do proměnných prostředí
summary: Soubor .zshrc může pomocí substituce příkazu načíst heslo z Keychain a exportovat je do proměnné prostředí při svém spuštění.
sources:
  - how-to/macos-keychain/README.md
kind: concept
createdAt: "2026-11-11T10:57:15.586Z"
updatedAt: "2026-11-11T10:57:15.586Z"
tags:
  - shell
  - zsh
  - proměnné-prostředí
aliases:
  - dynamické-načítání-hesel-do-proměnných-prostředí
  - DNHDPP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Dynamické načítání hesel do proměnných prostředí

Heslo uložené v [[macOS Keychain jako úložiště tajných údajů|macOS Keychain]] lze při inicializaci shellu načíst do proměnné prostředí. Konfigurace `.zshrc` tak obsahuje příkaz pro získání hesla místo jeho pevně zapsané hodnoty. ^[how-to/macos-keychain/README.md:3-17]

## Uložení hesla

Nejprve vytvoř záznam pomocí příkazu `security add-generic-password`. Parametr `-a` určuje account, `-s` označuje service neboli identifikátor záznamu a `-w` předává hodnotu hesla. Podrobnosti popisuje [[Identifikace záznamů Keychain pomocí account a service]]. ^[how-to/macos-keychain/README.md:21-31]

```bash
security add-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w "moje_heslo"
```

## Načítání v `.zshrc`

Do `.zshrc` přidej následující řádek. Příkaz `security find-generic-password` přečte heslo ze záznamu a jeho výstup se přiřadí do exportované proměnné `DIRECT_PASSWD`. ^[how-to/macos-keychain/README.md:47-59]

```bash
export DIRECT_PASSWD=$(security find-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w)
```

Po uložení konfigurace lze změnu použít v aktuálním shellu opětovným načtením `.zshrc`. ^[how-to/macos-keychain/README.md:61-64]

```bash
source ~/.zshrc
```

Hodnotu proměnné lze ověřit následujícím příkazem, který heslo vypíše do terminálu. ^[how-to/macos-keychain/README.md:68-72]

```bash
echo $DIRECT_PASSWD
```

## Změna hesla

Existující záznam lze aktualizovat přidáním parametru `-U`. Konfiguraci `.zshrc` není třeba upravovat: nové heslo se načte při příštím otevření terminálu. Tento postup rozvádí [[Aktualizace hesla v Keychain bez úpravy konfigurace shellu]]. ^[how-to/macos-keychain/README.md:35-43]

```bash
security add-generic-password -U -a "martin.adamec" -s "DIRECT_PASSWD" -w "nove_heslo"
```

## Sources

- [macOS Keychain — ukládání hesel do terminálu](how-to/macos-keychain/README.md)
