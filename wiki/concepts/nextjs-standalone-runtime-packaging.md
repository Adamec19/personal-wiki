---
title: Next.js standalone runtime packaging
summary: The production runtime combines .next/standalone/server.js with copied public and .next/static assets and runs through Node.js.
sources:
  - how-to/docker-basics/local-prod-web/README.md
kind: concept
createdAt: "2026-11-11T10:56:20.380Z"
updatedAt: "2026-11-11T10:56:20.380Z"
tags:
  - nextjs
  - standalone
  - deployment
aliases:
  - nextjs-standalone-runtime-packaging
  - NSRP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Next.js standalone runtime packaging

Next.js standalone runtime packaging prepares the production build for execution through a Node.js server, with static assets included in the runtime directory. The supplied workflow reproduces the relevant packaging steps of a production Docker image on the host computer, enabling [[Local production execution without Docker]]. ^[how-to/docker-basics/local-prod-web/README.md:3-17]

## Build output and runtime layout

The workflow expects a project with `package.json`, a `pnpm build` command, and Next.js standalone output. Its expected build structure contains `.next/standalone/server.js`, `.next/static/`, and `public/`. Projects with a different build output require adjustments to the script. ^[how-to/docker-basics/local-prod-web/README.md:19-34]

After building, the script copies `.next/static` and `public` into `.next/standalone`, matching the production Docker image’s packaging steps. It then runs `.next/standalone/server.js` through Node.js. These steps bring the standalone server and static files together for production runtime validation. ^[how-to/docker-basics/local-prod-web/README.md:105-114]

## Preparation and execution

Before packaging, the script selects an environment file, copies it to the project’s `.env`, enables Corepack, and installs dependencies with `pnpm install --frozen-lockfile`. It then creates the production build with `pnpm build`. These preparation steps connect packaging with [[Production environment file selection]] and [[Dependency installation with a frozen lockfile]]. ^[how-to/docker-basics/local-prod-web/README.md:97-105]

The local runner configures the application URL as `http://localhost:3000` and disables Redis cache. These settings belong to the supplied workflow; when adapting it to another project, check the expected URL, port, cache settings, environment-file convention, build command, and static-asset requirements. ^[how-to/docker-basics/local-prod-web/README.md:109-110, how-to/docker-basics/local-prod-web/README.md:133-145]

## Validation and development

Running the packaged output verifies the production build, including the standalone server and static files. This supports [[Production build validation versus development mode]]: ordinary development uses `pnpm dev` with hot reload, while source changes made after the production build require running the packaging script again. ^[how-to/docker-basics/local-prod-web/README.md:112-114, how-to/docker-basics/local-prod-web/README.md:147-157]

## Sources

- [Lokální spuštění produkčního buildu podobně jako v Dockeru](how-to/docker-basics/local-prod-web/README.md)
