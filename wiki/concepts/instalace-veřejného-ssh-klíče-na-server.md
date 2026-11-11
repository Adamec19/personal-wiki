---
title: Instalace veřejného SSH klíče na server
summary: Veřejný klíč lze na server přidat pomocí ssh-copy-id nebo ručním připojením do ~/.ssh/authorized_keys.
sources:
  - how-to/ssh-keys/README.md
kind: concept
createdAt: "2026-11-11T11:02:08.703Z"
updatedAt: "2026-11-11T11:02:08.703Z"
tags:
  - ssh
  - servers
  - authentication
aliases:
  - instalace-veřejného-ssh-klíče-na-server
  - IVSKNS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Instalace veřejného SSH klíče na server

Veřejný SSH klíč se instaluje na vzdálený server, aby umožnil přihlašování pomocí [[Autentizace pomocí SSH klíčů|SSH klíčů]] bez zadávání hesla k serveru. Soukromý klíč zůstává na místním počítači a nesmí se sdílet; na server se přenáší pouze veřejný klíč. ^[how-to/ssh-keys/README.md:5-9]

## Předpoklady

Potřebuješ existující pár klíčů. Při výchozím uložení je soukromý klíč v `~/.ssh/id_ed25519` a veřejný v `~/.ssh/id_ed25519.pub`. Vytvoření páru popisuje [[Generování SSH klíčů Ed25519]]. ^[how-to/ssh-keys/README.md:13-30]

## Instalace pomocí ssh-copy-id

Pro přidání klíče na server použij následující příkaz, kde `uzivatel` označuje vzdálený účet a `ip-serveru` adresu serveru. ^[how-to/ssh-keys/README.md:79-82]

```bash
ssh-copy-id uzivatel@ip-serveru
```

## Ruční instalace

Alternativně lze obsah veřejného klíče přenést přes SSH a připojit do souboru `~/.ssh/authorized_keys` vzdáleného účtu. Příkaz nejprve vytvoří adresář `~/.ssh`, pokud ještě neexistuje. ^[how-to/ssh-keys/README.md:84-86]

```bash
cat ~/.ssh/id_ed25519.pub | ssh uzivatel@ip-serveru \
  "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

## Ověření a diagnostika

Po instalaci ověř přihlášení následujícím příkazem. Přihlášení by mělo proběhnout bez zadávání hesla k serveru. ^[how-to/ssh-keys/README.md:88-90]

```bash
ssh uzivatel@ip-serveru
```

Pokud připojení skončí chybou `Permission denied`, zapni podrobný výpis pomocí přepínače `-v`. Ten pomůže zjistit, ve které části připojení nastává problém; související téma je [[Diagnostika problémů s SSH připojením]]. ^[how-to/ssh-keys/README.md:129-132]

```bash
ssh -v uzivatel@ip-serveru
```

## Sources

- [SSH Keys — generování a správa klíčů](how-to/ssh-keys/README.md)
