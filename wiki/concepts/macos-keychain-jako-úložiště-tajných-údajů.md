---
title: macOS Keychain jako úložiště tajných údajů
summary: Keychain umožňuje uchovávat hesla a jiné tajné údaje mimo soubor .zshrc a načítat je ze shellu.
sources:
  - how-to/macos-keychain/README.md
kind: concept
createdAt: "2026-11-11T10:57:03.129Z"
updatedAt: "2026-11-11T10:57:03.129Z"
tags:
  - macos
  - keychain
  - bezpečnost
aliases:
  - macos-keychain-jako-úložiště-tajných-údajů
  - MKJÚTÚ
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# macOS Keychain jako úložiště tajných údajů

macOS Keychain umožňuje uložit heslo nebo jiný tajný údaj a načítat jej v shellu bez zapsání jeho hodnoty přímo do `.zshrc`. Konfigurace shellu pak obsahuje příkaz pro získání hesla místo samotného hesla. ^[how-to/macos-keychain/README.md:3-17]

## Uložení a identifikace záznamu

Heslo se ukládá příkazem `security add-generic-password`. Parametr `-a` určuje account, tedy uživatelské jméno, `-s` určuje service, tedy libovolný identifikátor záznamu, a `-w` obsahuje hodnotu hesla. Podrobněji viz [[Identifikace záznamů Keychain pomocí account a service]]. ^[how-to/macos-keychain/README.md:21-31]

```bash
security add-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w "moje_heslo"
```

## Načítání do shellu

Uložené heslo lze přečíst pomocí `security find-generic-password` se stejnými hodnotami account a service a přepínačem `-w`. ^[how-to/macos-keychain/README.md:47-51]

```bash
security find-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w
```

Pro [[Dynamické načítání hesel do proměnných prostředí]] lze do `.zshrc` vložit následující příkaz. Jeho výstup se při provedení přiřadí do exportované proměnné `DIRECT_PASSWD`; změnu konfigurace lze v aktuálním shellu načíst příkazem `source ~/.zshrc`. ^[how-to/macos-keychain/README.md:55-64]

```bash
export DIRECT_PASSWD=$(security find-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w)
```

```bash
source ~/.zshrc
```

## Aktualizace hesla

Existující záznam lze přepsat přidáním přepínače `-U` k příkazu pro uložení. [[Aktualizace hesla v Keychain bez úpravy konfigurace shellu]] umožňuje ponechat `.zshrc` beze změny: nová hodnota se načte při příštím otevření terminálu. ^[how-to/macos-keychain/README.md:35-43]

```bash
security add-generic-password -U -a "martin.adamec" -s "DIRECT_PASSWD" -w "nove_heslo"
```

## Odstranění záznamu

Záznam lze odstranit příkazem `security delete-generic-password` s odpovídajícími hodnotami account a service. Další související operace shrnuje [[Správa hesel v Keychain pomocí příkazu security]]. ^[how-to/macos-keychain/README.md:76-80]

```bash
security delete-generic-password -a "martin.adamec" -s "DIRECT_PASSWD"
```

## Sources

- [macOS Keychain — ukládání hesel do terminálu](how-to/macos-keychain/README.md)
