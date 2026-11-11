---
title: Aktualizace hesla v Keychain bez úpravy konfigurace shellu
summary: Parametr -U u add-generic-password umožňuje přepsat existující heslo, které se při dalším načtení .zshrc převezme bez změny konfigurace.
sources:
  - how-to/macos-keychain/README.md
kind: concept
createdAt: "2026-11-11T10:57:14.404Z"
updatedAt: "2026-11-11T10:57:14.404Z"
tags:
  - keychain
  - správa-hesel
  - zsh
aliases:
  - aktualizace-hesla-v-keychain-bez-úpravy-konfigurace-shellu
  - AHVKBÚKS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Aktualizace hesla v Keychain bez úpravy konfigurace shellu

Heslo uložené v [[macOS Keychain jako úložiště tajných údajů|macOS Keychain]] lze aktualizovat bez změny `.zshrc`, pokud ho konfigurace shellu načítá dynamicky příkazem `security find-generic-password`. Nová hodnota se projeví při příštím otevření terminálu. ^[how-to/macos-keychain/README.md:35-43]

## Aktualizace existujícího záznamu

Existující heslo přepíše příkaz `security add-generic-password` s příznakem `-U`. Parametr `-a` určuje account, `-s` service a `-w` novou hodnotu hesla. Pro aktualizaci použij stejné account a service jako při načítání záznamu; podrobnosti popisuje [[Identifikace záznamů Keychain pomocí account a service]]. ^[how-to/macos-keychain/README.md:27-40, how-to/macos-keychain/README.md:47-50]

    security add-generic-password -U -a "martin.adamec" -s "DIRECT_PASSWD" -w "nove_heslo"

## Dynamické načítání v shellu

Konfigurace `.zshrc` obsahuje příkaz pro načtení hesla z Keychain do proměnné prostředí místo samotného hesla. Tento způsob popisuje také [[Dynamické načítání hesel do proměnných prostředí]]. ^[how-to/macos-keychain/README.md:9-17, how-to/macos-keychain/README.md:55-59]

    export DIRECT_PASSWD=$(security find-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w)

Po aktualizaci záznamu není potřeba tento řádek upravovat. Pro načtení hodnoty v aktuálním shellu lze konfiguraci znovu aplikovat příkazem `source ~/.zshrc`; jinak se změna projeví při příštím otevření terminálu. ^[how-to/macos-keychain/README.md:43-43, how-to/macos-keychain/README.md:61-64]

## Sources

- [macOS Keychain — ukládání hesel do terminálu](how-to/macos-keychain/README.md)
