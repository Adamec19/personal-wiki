---
title: Správa klíčů v SSH agentovi
summary: Příkaz ssh-add přidává soukromý klíč do SSH agenta a přepínač -l vypisuje načtené klíče.
sources:
  - how-to/ssh-keys/README.md
kind: concept
createdAt: "2026-11-11T11:02:11.167Z"
updatedAt: "2026-11-11T11:02:11.167Z"
tags:
  - ssh
  - ssh-agent
  - key-management
aliases:
  - správa-klíčů-v-ssh-agentovi
  - SKVSA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Správa klíčů v SSH agentovi

SSH klíč lze přidat do SSH agenta příkazem `ssh-add`. Pro klíč uložený ve výchozí cestě z postupu [[Generování SSH klíčů Ed25519]] se používá soubor `~/.ssh/id_ed25519`. ^[how-to/ssh-keys/README.md:22-29, how-to/ssh-keys/README.md:103-108]

## Přidání klíče

Následující příkaz přidá klíč do SSH agenta. Zadává se cesta k soukromému klíči; soubor s příponou `.pub` obsahuje veřejný klíč. Soukromý klíč zůstává na vlastním počítači a nesmí se sdílet. ^[how-to/ssh-keys/README.md:7-9, how-to/ssh-keys/README.md:26-29, how-to/ssh-keys/README.md:103-108]

```bash
ssh-add ~/.ssh/id_ed25519
```

## Zobrazení klíčů v agentovi

Příkaz `ssh-add -l` zobrazí klíče v SSH agentovi. ^[how-to/ssh-keys/README.md:103-108]

```bash
ssh-add -l
```

## Související nastavení

Pro [[Nastavení SSH přístupu na GitHub]] je potřeba veřejný klíč vložit do nastavení GitHubu. Pro [[Instalace veřejného SSH klíče na server|přístup na vzdálený server]] lze použít `ssh-copy-id`. ^[how-to/ssh-keys/README.md:34-42, how-to/ssh-keys/README.md:79-89]

## Sources

- [SSH Keys — generování a správa klíčů](how-to/ssh-keys/README.md)
