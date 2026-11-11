---
title: Diagnostika problémů s SSH připojením
summary: Řešení problémů zahrnuje kontrolu SSH adresy Git remote, ověření autentizace na GitHubu a podrobný výpis pomocí ssh -v.
sources:
  - how-to/ssh-keys/README.md
kind: concept
createdAt: "2026-11-11T11:02:18.612Z"
updatedAt: "2026-11-11T11:02:18.612Z"
tags:
  - ssh
  - git
  - troubleshooting
aliases:
  - diagnostika-problémů-s-ssh-připojením
  - DPSSP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Diagnostika problémů s SSH připojením

Při problémech s [[Autentizace pomocí SSH klíčů|autentizací pomocí SSH klíčů]] lze ověřit připojení, zkontrolovat použitý protokol Git remote a při chybě oprávnění zapnout podrobný výpis SSH. ^[how-to/ssh-keys/README.md:114-132]

## Git stále žádá heslo

Pokud Git žádá heslo i po nastavení SSH klíče, zkontroluj adresy vzdáleného repozitáře příkazem `git remote -v`. Remote má používat SSH; pokud začíná na `https://`, změň jeho adresu na SSH pomocí `git remote set-url origin git@github.com:Adamec19/repozitar.git`, kde účet a název repozitáře nahraď odpovídajícími hodnotami. ^[how-to/ssh-keys/README.md:114-121]

## Ověření autentizace na GitHubu

Příkaz `ssh -T git@github.com` ověří [[Nastavení SSH přístupu na GitHub|SSH přístup na GitHub]]. Pokud odpověď obsahuje tvé uživatelské jméno a potvrzení úspěšné autentizace, klíč je nastavený. ^[how-to/ssh-keys/README.md:44-48, how-to/ssh-keys/README.md:123-127]

## Chyba Permission denied

Při chybě `Permission denied` spusť `ssh -v uzivatel@server`. Přepínač `-v` zapne podrobný výpis, který pomůže určit, kde připojení selhává. ^[how-to/ssh-keys/README.md:129-132]

## Kontrola klíčů a SSH agenta

Existující soubory klíčů zobrazíš příkazem `ls -la ~/.ssh/`. Veřejný klíč pro kontrolu nebo kopírování vypíše `cat ~/.ssh/id_ed25519.pub`. Soukromý klíč zůstává na počítači a nesmí se sdílet. ^[how-to/ssh-keys/README.md:7-9, how-to/ssh-keys/README.md:94-99]

V rámci [[Správa klíčů v SSH agentovi|správy klíčů v SSH agentovi]] zobrazíš načtené klíče příkazem `ssh-add -l`. Klíč přidáš příkazem `ssh-add ~/.ssh/id_ed25519`. ^[how-to/ssh-keys/README.md:103-108]

## Sources

- [SSH Keys — generování a správa klíčů](how-to/ssh-keys/README.md)
