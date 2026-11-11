---
title: Generování SSH klíčů Ed25519
summary: Příkaz ssh-keygen vytváří pár klíčů Ed25519 s volitelnou passphrase, komentářem a vlastní cestou uložení.
sources:
  - how-to/ssh-keys/README.md
kind: concept
createdAt: "2026-11-11T11:01:57.940Z"
updatedAt: "2026-11-11T11:01:57.940Z"
tags:
  - ssh
  - key-management
  - ed25519
aliases:
  - generování-ssh-klíčů-ed25519
  - GSKE
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Generování SSH klíčů Ed25519

SSH klíče umožňují přihlašování na GitHub, vzdálené servery a další služby bez zadávání hesla. Tvoří je pár: soukromý klíč zůstává na počítači a nikdy se nesdílí, veřejný klíč se nahraje na cílovou službu. Podrobněji viz [[Autentizace pomocí SSH klíčů]]. ^[how-to/ssh-keys/README.md:5-9]

## Vytvoření klíče

Nový klíč vygeneruješ příkazem níže. Parametr `-t ed25519` vybírá moderní, doporučený typ klíče; `-C` přidává komentář či označení, obvykle e-mailovou adresu. ^[how-to/ssh-keys/README.md:13-20]

```bash
ssh-keygen -t ed25519 -C "tvuj@email.cz"
```

Po spuštění se příkaz zeptá na umístění klíče a passphrase. Stisknutím Enter přijmeš výchozí cestu `~/.ssh/id_ed25519`. Passphrase můžeš zadat, nebo ji ponechat prázdnou stisknutím Enter. ^[how-to/ssh-keys/README.md:22-24]

## Vytvořené soubory

Vzniknou dva soubory: `~/.ssh/id_ed25519` obsahuje soukromý klíč, který se nikdy nesdílí, a `~/.ssh/id_ed25519.pub` obsahuje veřejný klíč určený k nahrání na GitHub či server. ^[how-to/ssh-keys/README.md:26-30]

Veřejný klíč pro kopírování zobrazíš následujícím příkazem. ^[how-to/ssh-keys/README.md:94-99]

```bash
cat ~/.ssh/id_ed25519.pub
```

## Další klíč pod jiným názvem

Pro další účet, například pracovní, lze vytvořit samostatný klíč. Parametr `-f` v uvedeném příkladu určuje odlišný název a cestu souboru. ^[how-to/ssh-keys/README.md:52-57]

```bash
ssh-keygen -t ed25519 -C "work@firma.cz" -f ~/.ssh/id_ed25519_work
```

## Navazující nastavení

Po vygenerování lze veřejný klíč přidat na GitHub nebo vzdálený server a soukromý klíč do SSH agenta. Další postupy popisují [[Nastavení SSH přístupu na GitHub]], [[Instalace veřejného SSH klíče na server]] a [[Správa klíčů v SSH agentovi]]. ^[how-to/ssh-keys/README.md:34-48, how-to/ssh-keys/README.md:79-90, how-to/ssh-keys/README.md:103-108]

## Sources

- [SSH Keys — generování a správa klíčů](how-to/ssh-keys/README.md)
