---
title: Managing Strapi administrator records with psql
summary: Use psql inside the database container to list administrator emails, count administrator records, or delete all records from admin_users.
sources:
  - how-to/direct-dev/strapi/README.md
kind: concept
createdAt: "2026-11-11T10:55:35.337Z"
updatedAt: "2026-11-11T10:55:35.337Z"
tags:
  - strapi
  - postgresql
  - database-administration
aliases:
  - managing-strapi-administrator-records-with-psql
  - MSARWP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Managing Strapi administrator records with psql

Strapi administrator records can be inspected and modified in the `admin_users` table using `psql` inside the PostgreSQL container. The commands below target the `postgres_strapi` container and database, connecting as the PostgreSQL user `postgres`. ^[how-to/direct-dev/strapi/README.md:106-122]

## Inspecting administrator records

List administrator email addresses with this command. ^[how-to/direct-dev/strapi/README.md:114-115]

```bash
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "SELECT email FROM admin_users;"
```

Count administrator records with `COUNT(*)`. ^[how-to/direct-dev/strapi/README.md:120-121]

```bash
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "SELECT COUNT(*) FROM admin_users;"
```

To inspect email addresses together with stored password hashes in the secondary container, use the following query. This is part of [[Resetting a Strapi administrator password by transferring its hash]]. ^[how-to/direct-dev/strapi/README.md:44-68]

```bash
docker exec -it postgres_strapi_2 psql -U postgres -d postgres_strapi -c "SELECT email, password FROM admin_users;"
```

## Updating an administrator password

Update the password hash for the administrator identified by email. Replace `USER@EMAIL.cz` and the example hash with the intended values. In this double-quoted shell command, escape each `$` as `\$`; see [[Escaping password hashes in shell commands]]. ^[how-to/direct-dev/strapi/README.md:84-87]

```bash
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "UPDATE admin_users SET password = '\$2a\$10\$HASH' WHERE email = 'USER@EMAIL.cz';"
```

The documented hash-transfer procedure obtains a hash by starting Strapi against a clean secondary database and registering an administrator. It then stops Strapi and the secondary container, starts the original container, applies the update, and restarts Strapi to log in. ^[how-to/direct-dev/strapi/README.md:51-92]

## Deleting all administrator records

The following command deletes **every record** in `admin_users`; it has no `WHERE` clause restricting deletion to a particular administrator. ^[how-to/direct-dev/strapi/README.md:117-118]

```bash
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "DELETE FROM admin_users;"
```

## Sources

- [Strapi Database - Quick Commands](how-to/direct-dev/strapi/README.md)
