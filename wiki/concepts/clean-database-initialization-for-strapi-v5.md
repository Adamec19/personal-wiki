---
title: Clean Database Initialization for Strapi v5
summary: When an old dump contains invalid data, recreate the database, run Strapi to create its schema and apply migrations, then seed fresh valid development data.
sources:
  - how-to/restore-db/README.md
kind: concept
createdAt: "2026-11-11T11:01:51.050Z"
updatedAt: "2026-11-11T11:01:51.050Z"
tags:
  - strapi
  - database-initialization
  - development
aliases:
  - clean-database-initialization-for-strapi-v5
  - CDIFSV
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Clean Database Initialization for Strapi v5

Clean database initialization creates a fresh local Strapi v5 database schema and populates it with valid development data. This workflow is useful when an older SQL dump contains invalid data that prevents Strapi v5 from starting. ^[how-to/restore-db/README.md:77-86]

## Prerequisites

The workflow requires Docker with the `postgres_strapi` container running, Node.js, and a Strapi project with its dependencies installed using `yarn install`. Before seeding, the database must have a schema created by running `yarn develop` at least once. ^[how-to/restore-db/README.md:133-138]

## Initialization workflow

The clean-start procedure deletes the existing database, creates an empty replacement, starts Strapi to create the schema and run migrations, and then runs `seedDevData.js`. The database reset is destructive, even though the seed script itself does not delete data. ^[how-to/restore-db/README.md:88-91, how-to/restore-db/README.md:119-130]

1. Recreate the database:

```bash
docker exec postgres_strapi psql -U postgres -c "DROP DATABASE postgres_strapi WITH (FORCE);"
docker exec postgres_strapi psql -U postgres -c "CREATE DATABASE postgres_strapi;"
```

2. Start Strapi to create the schema and run migrations:

```bash
cd ~/work/direct/projects/direct.cz-cms/strapi && yarn develop
```

3. Populate the database:

```bash
node /Users/martin.adamec/work/how-to/restore-db/seedDevData.js
```

These commands follow the source’s documented clean-start sequence. ^[how-to/restore-db/README.md:119-130]

## Seed configuration

The seed script uses `STRAPI_APP_DIR` to locate the Strapi project, defaulting to `~/work/direct/projects/direct.cz-cms/strapi`. It reads `DATABASE_URL` from that project’s `.env` and loads `@strapi/strapi` and `dotenv` from the project’s `node_modules`. A different project location can be supplied when invoking the script. ^[how-to/restore-db/README.md:94-100, how-to/restore-db/README.md:114-117]

```bash
STRAPI_APP_DIR=/jina/cesta/strapi node seedDevData.js
```

## Seeded data and behavior

The script creates three blog post categories, two page categories, four tags, two release-notes categories, one 600×400 PNG placeholder image, five blog posts, and four pages. Posts and pages are created as drafts and then published to produce Strapi v5 draft-and-publish pairs; see [[Strapi v5 Draft and Publish Seeding]]. ^[how-to/restore-db/README.md:81-84]

Records are created through the Strapi Documents API, allowing validations and lifecycles to run, including `generatedUrl` generation and duplicate checks. See [[Seeding Through the Strapi Documents API]]. ^[how-to/restore-db/README.md:86-86]

The script is non-destructive and idempotent: repeated runs skip existing records matched by slug or title. In development mode, uploads remain local rather than going to the cloud. See [[Idempotent and Non-Destructive Seeding]]. ^[how-to/restore-db/README.md:88-92]

## Sources

- [how-to/restore-db/README.md](how-to/restore-db/README.md)
