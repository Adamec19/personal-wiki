---
title: Identifikace záznamů Keychain pomocí account a service
summary: Parametry -a pro účet a -s pro službu určují záznam, se kterým příkaz security pracuje.
sources:
  - how-to/macos-keychain/README.md
kind: concept
createdAt: "2026-11-11T10:57:10.762Z"
updatedAt: "2026-11-11T10:57:10.762Z"
tags:
  - keychain
  - identifikace
  - cli
aliases:
  - identifikace-záznamů-keychain-pomocí-account-a-service
  - IZKPAAS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Identifikace záznamů Keychain pomocí account a service

Při práci s [[macOS Keychain jako úložiště tajných údajů|macOS Keychain]] pomocí příkazu `security` určují parametry `-a` a `-s`, se kterým záznamem pracuješ. Parametr `-a` označuje **account**, tedy uživatelské jméno, a `-s` označuje **service**, libovolný identifikátor klíče. V příkladech je account `martin.adamec` a service `DIRECT_PASSWD`. ^[how-to/macos-keychain/README.md:21-31]

## Použití při správě záznamu

Při uložení hesla se zadávají oba identifikátory společně s hodnotou hesla v parametru `-w`. ^[how-to/macos-keychain/README.md:21-31]

```bash
security add-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w "moje_heslo"
```

Pro přečtení hesla se použijí stejné hodnoty account a service. Takto lze heslo také [[Dynamické načítání hesel do proměnných prostředí|dynamicky načítat do proměnné prostředí]]. ^[how-to/macos-keychain/README.md:47-59]

```bash
security find-generic-password -a "martin.adamec" -s "DIRECT_PASSWD" -w
```

Při [[Aktualizace hesla v Keychain bez úpravy konfigurace shellu|aktualizaci existujícího hesla]] se zachovají oba identifikátory a přidá se příznak `-U`. Konfiguraci `.zshrc`, která heslo načítá dynamicky, není nutné měnit; nové heslo se načte při příštím otevření terminálu. ^[how-to/macos-keychain/README.md:35-43]

```bash
security add-generic-password -U -a "martin.adamec" -s "DIRECT_PASSWD" -w "nove_heslo"
```

Stejná dvojice account a service určuje také záznam, který se má smazat. ^[how-to/macos-keychain/README.md:76-80]

```bash
security delete-generic-password -a "martin.adamec" -s "DIRECT_PASSWD"
```

## Sources

- [macOS Keychain — ukládání hesel do terminálu](how-to/macos-keychain/README.md)
