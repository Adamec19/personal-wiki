---
title: Restoring a Strapi SQL database dump
summary: Restore a database using restore_db.py or by copying an SQL dump into the PostgreSQL container and executing it with psql.
sources:
  - how-to/direct-dev/strapi/README.md
kind: concept
createdAt: "2026-11-11T10:55:33.735Z"
updatedAt: "2026-11-11T10:55:33.735Z"
tags:
  - database-restore
  - postgresql
  - strapi
aliases:
  - restoring-a-strapi-sql-database-dump
  - RASSDD
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Restoring a Strapi SQL database dump

A Strapi SQL database dump can be restored into the Docker-hosted PostgreSQL database `postgres_strapi` either by running the provided restoration script or by manually copying and executing the SQL file. ^[how-to/direct-dev/strapi/README.md:29-40]

## Target database

The source defines a container named `postgres_strapi` using PostgreSQL 15, with database and user settings, host port `5432`, and a named volume for database storage. See also [[PostgreSQL containers for Strapi]]. ^[how-to/direct-dev/strapi/README.md:5-14]

```bash
docker run -d --name postgres_strapi \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=direct \
  -e POSTGRES_DB=postgres_strapi \
  -p 5432:5432 \
  -v postgres_strapi_data:/var/lib/postgresql/data \
  postgres:15
```

## Restore using the script

The documented script-based import is invoked with the following command. The source does not include the script’s implementation or configuration. ^[how-to/direct-dev/strapi/README.md:29-34]

```bash
python3 restore_db.py
```

## Restore manually

The manual procedure copies the SQL dump from the host into `/tmp/restore.sql` inside the container, then runs `psql` as the `postgres` user against the `postgres_strapi` database. This combines [[Kopírování souborů mezi hostitelem a kontejnerem]] with [[Spouštění příkazů uvnitř kontejnerů]]. ^[how-to/direct-dev/strapi/README.md:36-40]

```bash
docker cp /Users/martin.adamec/work/how-to/restore-db/db_strapi_backup_22.12_2026.sql postgres_strapi:/tmp/restore.sql
docker exec -i postgres_strapi psql -U postgres -d postgres_strapi -f /tmp/restore.sql
```

## Inspect the database

The source also provides commands to list databases and tables, and to count records in Strapi’s `admin_users` table. These commands expose database contents for inspection; the source does not define a complete restoration validation procedure. ^[how-to/direct-dev/strapi/README.md:106-122]

```bash
docker exec -it postgres_strapi psql -U postgres -c "\l"
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "\dt"
docker exec -it postgres_strapi psql -U postgres -d postgres_strapi -c "SELECT COUNT(*) FROM admin_users;"
```

## Sources

- [Strapi Database - Quick Commands](how-to/direct-dev/strapi/README.md)
