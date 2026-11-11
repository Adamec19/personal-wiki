---
title: Autentizace pomocí SSH klíčů
summary: SSH používá pár soukromého a veřejného klíče; soukromý klíč zůstává tajný a veřejný se přidává k cílové službě.
sources:
  - how-to/ssh-keys/README.md
kind: concept
createdAt: "2026-11-11T11:02:01.773Z"
updatedAt: "2026-11-11T11:02:01.773Z"
tags:
  - ssh
  - authentication
  - security
aliases:
  - autentizace-pomocí-ssh-klíčů
  - APSK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Autentizace pomocí SSH klíčů

SSH klíče umožňují bezpečné přihlašování na GitHub, vzdálené servery a další služby bez zadávání hesla. Autentizace využívá pár klíčů: **soukromý klíč (private key)** zůstává na počítači a nikdy se nesdílí, zatímco **veřejný klíč (public key)** se nahraje na cílovou službu nebo server. ^[how-to/ssh-keys/README.md:5-9]

## Vytvoření páru klíčů

Nový pár lze vytvořit příkazem níže. Parametr `-t ed25519` určuje ve zdroji doporučený typ klíče a `-C` přidává komentář, obvykle e-mail. Podrobnosti popisuje [[Generování SSH klíčů Ed25519]]. ^[how-to/ssh-keys/README.md:13-20]

```bash
ssh-keygen -t ed25519 -C "tvuj@email.cz"
```

Při generování se volí umístění klíče a volitelná passphrase. Výchozí umístění soukromého klíče je `~/.ssh/id_ed25519`; veřejný klíč vznikne v souboru `~/.ssh/id_ed25519.pub`. Passphrase lze zadat nebo ponechat prázdnou. ^[how-to/ssh-keys/README.md:22-30]

## Nastavení přístupu

### GitHub

Veřejný klíč zkopíruj do schránky a vlož na GitHubu do **Settings → SSH and GPG keys → New SSH key**. Připojení ověří příkaz `ssh -T git@github.com`; úspěšná odpověď obsahuje uživatelské jméno a potvrzení autentizace. Viz [[Nastavení SSH přístupu na GitHub]]. ^[how-to/ssh-keys/README.md:34-48]

```bash
pbcopy < ~/.ssh/id_ed25519.pub
ssh -T git@github.com
```

Pro více účtů lze vytvořit samostatné klíče a v `~/.ssh/config` přiřadit každému alias hostitele a odpovídající `IdentityFile`. Alias se následně použije v SSH adrese při klonování repozitáře, například `git@github-work:firma/repozitar.git`. ^[how-to/ssh-keys/README.md:52-75]

### Vzdálený server

Veřejný klíč lze na server přidat pomocí `ssh-copy-id` nebo ručně připojit jeho obsah do `~/.ssh/authorized_keys`. Poté se lze přihlásit příkazem `ssh uzivatel@ip-serveru` bez zadávání přihlašovacího hesla. Postup rozvádí [[Instalace veřejného SSH klíče na server]]. ^[how-to/ssh-keys/README.md:79-90]

```bash
ssh-copy-id uzivatel@ip-serveru
ssh uzivatel@ip-serveru
```

## Správa klíčů

Existující soubory klíčů lze vypsat pomocí `ls -la ~/.ssh/` a veřejný klíč zobrazit příkazem `cat ~/.ssh/id_ed25519.pub`. Soukromý klíč lze přidat do SSH agenta pomocí `ssh-add`; přepínač `-l` vypíše klíče dostupné v agentovi. Viz [[Správa klíčů v SSH agentovi]]. ^[how-to/ssh-keys/README.md:94-108]

```bash
ssh-add ~/.ssh/id_ed25519
ssh-add -l
```

## Diagnostika připojení

Pokud Git po nastavení klíčů stále žádá heslo, zkontroluj pomocí `git remote -v`, zda vzdálený repozitář používá SSH adresu. Remote s adresou začínající `https://` lze přepnout příkazem `git remote set-url origin git@github.com:Adamec19/repozitar.git`. ^[how-to/ssh-keys/README.md:114-121]

Nastavení klíče na GitHubu ověří `ssh -T git@github.com`. Při chybě `Permission denied` pomůže podrobný výpis příkazu `ssh -v uzivatel@server`, který ukáže průběh připojení. Další souvislosti nabízí [[Diagnostika problémů s SSH připojením]]. ^[how-to/ssh-keys/README.md:123-132]

## Sources

- [SSH Keys — generování a správa klíčů](how-to/ssh-keys/README.md)
