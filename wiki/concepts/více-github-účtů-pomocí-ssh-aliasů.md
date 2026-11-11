---
title: Více GitHub účtů pomocí SSH aliasů
summary: Samostatné klíče a aliasy Host v ~/.ssh/config umožňují vybírat účet pomocí adresy repozitáře.
sources:
  - how-to/ssh-keys/README.md
kind: concept
createdAt: "2026-11-11T11:02:24.991Z"
updatedAt: "2026-11-11T11:02:24.991Z"
tags:
  - github
  - ssh
  - configuration
aliases:
  - více-github-účtů-pomocí-ssh-aliasů
  - VGÚPSA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Více GitHub účtů pomocí SSH aliasů

Osobní a pracovní GitHub účet lze rozlišit samostatnými SSH klíči a konfigurací v `~/.ssh/config`. Alias `github-work` směruje připojení na `github.com` s pracovním klíčem, zatímco konfigurace pro `github.com` používá osobní klíč. ^[how-to/ssh-keys/README.md:52-70]

## Vygenerování pracovního klíče

Pro pracovní účet vytvořte druhý klíč s vlastním názvem. Příkaz používá typ Ed25519, komentář s pracovním e-mailem a cestu `~/.ssh/id_ed25519_work`. Podrobnosti popisuje [[Generování SSH klíčů Ed25519]]. ^[how-to/ssh-keys/README.md:15-20, how-to/ssh-keys/README.md:54-57]

```bash
ssh-keygen -t ed25519 -C "work@firma.cz" -f ~/.ssh/id_ed25519_work
```

Veřejný klíč přidejte do odpovídajícího GitHub účtu přes **Settings → SSH and GPG keys → New SSH key**; postup rozvádí [[Nastavení SSH přístupu na GitHub]]. Soukromý klíč zůstává na vašem počítači a nesmí se sdílet. ^[how-to/ssh-keys/README.md:7-9, how-to/ssh-keys/README.md:34-42]

## Nastavení SSH aliasů

Vytvořte nebo upravte soubor `~/.ssh/config`. Položka `Host` určuje alias použitý při připojení, `HostName` cílový server a `IdentityFile` příslušný klíč. Obě konfigurace používají uživatele `git`. ^[how-to/ssh-keys/README.md:59-70]

```sshconfig
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work

Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
```

## Klonování pracovního repozitáře

Při klonování pracovního repozitáře použijte v SSH adrese alias `github-work`. Tím adresa odpovídá konfiguraci pracovního klíče. ^[how-to/ssh-keys/README.md:61-64, how-to/ssh-keys/README.md:72-75]

```bash
git clone git@github-work:firma/repozitar.git
```

## Kontrola při potížích

Pokud Git stále žádá heslo, zkontrolujte pomocí `git remote -v`, zda vzdálená adresa používá SSH místo HTTPS. Další postupy obsahuje [[Diagnostika problémů s SSH připojením]]. ^[how-to/ssh-keys/README.md:114-121]

```bash
git remote -v
```

## Sources

- [SSH Keys — generování a správa klíčů](how-to/ssh-keys/README.md)
