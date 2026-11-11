---
title: Seeding Through the Strapi Documents API
summary: Creating seed records through the Documents API runs validations and lifecycle hooks, supporting correct generatedUrl values and duplicate checks.
sources:
  - how-to/restore-db/README.md
kind: concept
createdAt: "2026-11-11T11:01:34.921Z"
updatedAt: "2026-11-11T11:01:34.921Z"
tags:
  - strapi
  - documents-api
  - data-validation
aliases:
  - seeding-through-the-strapi-documents-api
  - STTSDA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Seeding Through the Strapi Documents API

Seeding through the Strapi Documents API populates a clean local Strapi v5 database with sample development data. The `seedDevData.js` script provides this approach when an older SQL dump contains invalid data that prevents Strapi v5 from starting. ^[how-to/restore-db/README.md:75-79]

## Why use the Documents API?

The script creates records through the Strapi Documents API rather than raw SQL. This runs validations and lifecycle logic, allowing `generatedUrl` generation and duplicate checks to work correctly. See [[Seeding Through the Strapi Documents API|Documents API seeding]] in the broader context of [[Strapi v5 Development Data Seeding]]. ^[how-to/restore-db/README.md:86-86]

## Created data and repeatability

The script creates three blog post categories, two page categories, four tags, two release-notes categories, and one 600×400 PNG placeholder image uploaded to `public/uploads`. It also creates five blog posts and four pages as drafts, then publishes them to produce Strapi v5 draft-and-publish pairs. This relates to [[Strapi v5 Draft and Publish Seeding]]. ^[how-to/restore-db/README.md:81-84]

The script deletes nothing and skips existing records on repeated runs, matching them by slug or title. Uploads remain local in development mode. These properties support [[Idempotent and Non-Destructive Seeding]]. ^[how-to/restore-db/README.md:88-92]

## Configuration and prerequisites

`STRAPI_APP_DIR` identifies the Strapi project directory and defaults to `~/work/direct/projects/direct.cz-cms/strapi`. The script reads `DATABASE_URL` from that project's `.env` file and loads `@strapi/strapi` and `dotenv` from its `node_modules`, so project dependencies must already be installed. ^[how-to/restore-db/README.md:94-100]

Execution requires Node.js, Docker with the `postgres_strapi` container running, and a database whose schema has been initialized by running `yarn develop` at least once. See [[Clean Database Initialization for Strapi v5]]. ^[how-to/restore-db/README.md:133-138]

## Running the script

The script can be run from any directory using its path. Set `STRAPI_APP_DIR` to use a different Strapi project location. ^[how-to/restore-db/README.md:109-117]

```bash
node /Users/martin.adamec/work/how-to/restore-db/seedDevData.js
```

```bash
STRAPI_APP_DIR=/jina/cesta/strapi node seedDevData.js
```

For a clean start, the documented workflow drops and recreates the database, starts Strapi to create the schema and run migrations, then runs the seed script. The database reset is destructive; it is a separate preparation step from the non-destructive seeding operation. ^[how-to/restore-db/README.md:88-91, how-to/restore-db/README.md:119-130]

## Sources

- [Restore Databáze — postgres_strapi](how-to/restore-db/README.md)
