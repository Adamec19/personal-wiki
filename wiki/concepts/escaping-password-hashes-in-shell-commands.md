---
title: Escaping password hashes in shell commands
summary: Escape dollar signs in password hashes passed through double-quoted shell commands so the shell preserves the literal hash.
sources:
  - how-to/direct-dev/strapi/README.md
kind: concept
createdAt: "2026-11-11T10:55:30.282Z"
updatedAt: "2026-11-11T10:55:30.282Z"
tags:
  - shell
  - password-hashes
  - sql
aliases:
  - escaping-password-hashes-in-shell-commands
  - EPHISC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Escaping password hashes in shell commands

Při aktualizaci hesla administrátora Strapi pomocí shellového příkazu je potřeba escapovat znaky `$` v hashi jako `\$`. Zdroj tento zápis používá v SQL příkazu předávaném přes `docker exec` do `psql`, kde je argument `-c` uzavřen do dvojitých uvozovek. ^[how-to/direct-dev/strapi/README.md:84-87]

## Příklad aktualizace

Následující příkaz aktualizuje sloupec `password` v tabulce `admin_users` pro zadaný e-mail. Hodnota `\$2a\$10\$HASH` představuje zástupný hash; každý znak `$` je zapsán s předcházejícím zpětným lomítkem. ^[how-to/direct-dev/strapi/README.md:84-87]

```bash
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "UPDATE admin_users SET password = '\$2a\$10\$HASH' WHERE email = 'USER@EMAIL.cz';"
```

## Použití při přenosu hesla

V postupu [[Resetting a Strapi administrator password by transferring its hash]] se hash nejprve získá z druhé databáze dotazem `SELECT email, password FROM admin_users;`. Po zastavení dočasného prostředí a spuštění původního kontejneru se zkopírovaný hash vloží do aktualizačního příkazu s escapovanými znaky `$`. Poté se Strapi spustí a ověří se přihlášení. ^[how-to/direct-dev/strapi/README.md:66-92]

## Sources

- [Strapi Database - Quick Commands](how-to/direct-dev/strapi/README.md)
