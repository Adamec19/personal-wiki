---
title: Resetting a Strapi administrator password by transferring its hash
summary: Register an administrator against a temporary database, retrieve the generated password hash, and copy it into the original database's admin_users record.
sources:
  - how-to/direct-dev/strapi/README.md
kind: concept
createdAt: "2026-11-11T10:55:37.626Z"
updatedAt: "2026-11-11T10:55:37.626Z"
tags:
  - strapi
  - authentication
  - database-administration
aliases:
  - resetting-a-strapi-administrator-password-by-transferring-its-hash
  - RASAPBTIH
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Resetting a Strapi administrator password by transferring its hash

Heslo administrátora Strapi lze obnovit přenesením hashe z účtu vytvořeného v čisté pomocné databázi do odpovídajícího záznamu v původní databázi. Postup používá kontejnery `postgres_strapi_2` jako zdroj hashe a `postgres_strapi` jako cíl. ^[how-to/direct-dev/strapi/README.md:44-86]

## 1. Připravit pomocnou databázi

Zastavte původní kontejner a spusťte čistý pomocný PostgreSQL kontejner. V tomto postupu pomocný kontejner používá hostitelský port `5432`, který uvolní zastavení původního kontejneru. Souvisí s [[PostgreSQL containers for Strapi]]. ^[how-to/direct-dev/strapi/README.md:46-59]

```bash
docker stop postgres_strapi

docker run -d --hostname postgres_strapi_2 --name postgres_strapi_2 \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=direct \
  -e POSTGRES_DB=postgres_strapi \
  -p 5432:5432 \
  postgres:15.3-alpine3.18
```

## 2. Vytvořit účet a získat hash

Spusťte Strapi a zaregistrujte administrátorský účet. Poté z pomocné databáze vypište e-mail a hash hesla uložený v tabulce `admin_users`. Viz také [[Managing Strapi administrator records with psql]]. ^[how-to/direct-dev/strapi/README.md:61-69]

```bash
npm run develop
```

```bash
docker exec -it postgres_strapi_2 psql -U postgres -d postgres_strapi \
  -c "SELECT email, password FROM admin_users;"
```

## 3. Přepnout zpět na původní databázi

Zastavte Strapi pomocí `Ctrl + C`, zastavte pomocný kontejner a znovu spusťte původní kontejner. ^[how-to/direct-dev/strapi/README.md:71-82]

```bash
docker stop postgres_strapi_2
docker start postgres_strapi
```

## 4. Aktualizovat heslo cílového účtu

V původní databázi aktualizujte sloupec `password` u účtu vybraného podle e-mailu. Zástupný hash nahraďte získaným hashem a `USER@EMAIL.cz` e-mailem cílového administrátora. V uvedeném shellovém příkazu escapujte každý znak `$` jako `\$`; související téma je [[Escaping password hashes in shell commands]]. ^[how-to/direct-dev/strapi/README.md:84-87]

```bash
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi \
  -c "UPDATE admin_users SET password = '\$2a\$10\$HASH' WHERE email = 'USER@EMAIL.cz';"
```

## 5. Spustit Strapi a přihlásit se

Znovu spusťte Strapi a přihlaste se k cílovému účtu heslem použitým při registraci v pomocné databázi. ^[how-to/direct-dev/strapi/README.md:61-69, how-to/direct-dev/strapi/README.md:84-92]

```bash
npm run develop
```

## Sources

- [Strapi Database - Quick Commands](how-to/direct-dev/strapi/README.md)
