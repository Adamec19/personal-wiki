---
title: Správa hesel v Keychain pomocí příkazu security
summary: Příkaz security poskytuje operace add-generic-password, find-generic-password a delete-generic-password pro ukládání, čtení a mazání hesel.
sources:
  - how-to/macos-keychain/README.md
kind: concept
createdAt: "2026-11-11T10:57:13.334Z"
updatedAt: "2026-11-11T10:57:13.334Z"
tags:
  - keychain
  - cli
  - správa-hesel
aliases:
  - správa-hesel-v-keychain-pomocí-příkazu-security
  - SHVKPPS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Správa hesel v Keychain pomocí příkazu security

Příkaz `security` umožňuje ukládat, číst, aktualizovat a mazat hesla v [[macOS Keychain jako úložiště tajných údajů|macOS Keychain]]. Shell může uložené heslo načítat dynamicky, takže jeho hodnota nemusí být zapsaná přímo v `.zshrc`. ^[how-to/macos-keychain/README.md:3-17]

## Identifikace záznamu

Záznam určují parametry `-a` (account, uživatelské jméno) a `-s` (service, libovolný identifikátor). Při ukládání se hodnota hesla předává parametrem `-w`. Podrobnosti shrnuje [[Identifikace záznamů Keychain pomocí account a service]]. ^[how-to/macos-keychain/README.md:21-31]

## Uložení hesla

Nový záznam vytvoří příkaz `security add-generic-password` s účtem, identifikátorem služby a heslem. ^[how-to/macos-keychain/README.md:21-31]

```bash
security add-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w "moje_heslo"
```

## Aktualizace hesla

Pokud záznam již existuje, přidá se přepínač `-U`. Při dynamickém načítání není nutné upravovat `.zshrc`; nové heslo se načte při příštím otevření terminálu. Viz [[Aktualizace hesla v Keychain bez úpravy konfigurace shellu]]. ^[how-to/macos-keychain/README.md:35-43]

```bash
security add-generic-password -U -a "martin.adamec" -s "DIRECT_PASSWD" -w "nove_heslo"
```

## Čtení a použití v shellu

Heslo lze získat příkazem `security find-generic-password`, který vyhledá záznam podle účtu a služby a s přepínačem `-w` vypíše jeho hodnotu. ^[how-to/macos-keychain/README.md:47-51]

```bash
security find-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w
```

Pro [[Dynamické načítání hesel do proměnných prostředí]] lze do `.zshrc` vložit následující přiřazení. Změnu konfigurace v aktuálním shellu aplikuje `source ~/.zshrc`. ^[how-to/macos-keychain/README.md:55-64]

```bash
export DIRECT_PASSWD=$(security find-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w)
source ~/.zshrc
```

## Smazání záznamu

Záznam odstraní příkaz `security delete-generic-password` se stejnými hodnotami účtu a služby. ^[how-to/macos-keychain/README.md:76-80]

```bash
security delete-generic-password -a "martin.adamec" -s "DIRECT_PASSWD"
```

## Sources

- [macOS Keychain — ukládání hesel do terminálu](how-to/macos-keychain/README.md)
