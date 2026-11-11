---
title: Nastavení SSH přístupu na GitHub
summary: Veřejný klíč se přidává do nastavení GitHubu a autentizace se ověřuje příkazem ssh -T git@github.com.
sources:
  - how-to/ssh-keys/README.md
kind: concept
createdAt: "2026-11-11T11:02:05.376Z"
updatedAt: "2026-11-11T11:02:05.376Z"
tags:
  - github
  - ssh
  - authentication
aliases:
  - nastavení-ssh-přístupu-na-github
  - NSPNG
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Nastavení SSH přístupu na GitHub

SSH klíče umožňují bezpečné přihlašování na GitHub bez zadávání hesla. Používají pár klíčů: soukromý klíč zůstává na počítači a nikdy se nesdílí, veřejný klíč se nahraje na GitHub. Viz také [[Autentizace pomocí SSH klíčů]]. ^[how-to/ssh-keys/README.md:5-9]

## Vygenerování klíče

Pro [[Generování SSH klíčů Ed25519]] spusť následující příkaz. Parametr `-t ed25519` určuje doporučený typ klíče a `-C` přidává komentář, obvykle e-mail. ^[how-to/ssh-keys/README.md:13-20]

```bash
ssh-keygen -t ed25519 -C "tvuj@email.cz"
```

Při dotazu na umístění potvrď výchozí cestu `~/.ssh/id_ed25519` klávesou Enter. Passphrase můžeš zadat nebo ponechat prázdnou. Vznikne soukromý klíč `~/.ssh/id_ed25519` a veřejný klíč `~/.ssh/id_ed25519.pub`. ^[how-to/ssh-keys/README.md:22-30]

## Přidání veřejného klíče na GitHub

Na macOS zkopíruj veřejný klíč do schránky následujícím příkazem. Na GitHubu otevři **Settings → SSH and GPG keys → New SSH key**, vlož klíč a ulož jej. ^[how-to/ssh-keys/README.md:34-42]

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

Připojení ověř příkazem níže. Úspěšné ověření se projeví zprávou se jménem účtu a potvrzením autentizace. ^[how-to/ssh-keys/README.md:44-48]

```bash
ssh -T git@github.com
```

## Použití SSH v repozitáři

Pokud Git stále žádá heslo, zkontroluj adresy vzdáleného repozitáře pomocí `git remote -v`. Jestliže adresa začíná `https://`, přepni `origin` na SSH adresu příslušného repozitáře. ^[how-to/ssh-keys/README.md:114-121]

```bash
git remote -v
git remote set-url origin git@github.com:Adamec19/repozitar.git
```

## Více účtů na GitHubu

Pro oddělení pracovního a osobního účtu vygeneruj druhý klíč s vlastním názvem. ^[how-to/ssh-keys/README.md:52-57]

```bash
ssh-keygen -t ed25519 -C "work@firma.cz" -f ~/.ssh/id_ed25519_work
```

V souboru `~/.ssh/config` nastav alias `github-work` pro pracovní klíč a hostitele `github.com` pro výchozí klíč. ^[how-to/ssh-keys/README.md:59-70]

```text
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work

Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
```

Při klonování pracovního repozitáře použij nakonfigurovaný alias. ^[how-to/ssh-keys/README.md:72-75]

```bash
git clone git@github-work:firma/repozitar.git
```

## Správa klíčů a diagnostika

Klíč lze přidat do SSH agenta příkazem `ssh-add`; přepínač `-l` vypíše klíče uložené v agentovi. Podrobnosti shrnuje [[Správa klíčů v SSH agentovi]]. ^[how-to/ssh-keys/README.md:103-108]

```bash
ssh-add ~/.ssh/id_ed25519
ssh-add -l
```

Při chybě `Permission denied` pomůže podrobný výpis připojení pomocí `ssh -v`. Viz [[Diagnostika problémů s SSH připojením]]. ^[how-to/ssh-keys/README.md:129-132]

## Sources

- [SSH Keys — generování a správa klíčů](how-to/ssh-keys/README.md)
