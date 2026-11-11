---
title: Local production execution without Docker
summary: run-local-prod.sh reproduces key production Dockerfile steps on the host to build and run a Next.js application without creating a Docker image.
sources:
  - how-to/docker-basics/local-prod-web/README.md
kind: concept
createdAt: "2026-11-11T10:56:23.572Z"
updatedAt: "2026-11-11T10:56:23.572Z"
tags:
  - local-development
  - production-builds
  - docker
aliases:
  - local-production-execution-without-docker
  - LPEWD
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Local production execution without Docker

Local production execution without Docker runs a production build directly on the host computer, reproducing important steps from a production Dockerfile without building or starting a Docker image. The supplied `run-local-prod.sh` utility supports Next.js applications that produce a [[Next.js standalone runtime packaging|standalone build]] and run through a Node.js server. ^[how-to/docker-basics/local-prod-web/README.md:3-17]

## Prerequisites

The project must have a `package.json`, a `pnpm build` command, Next.js standalone output, and an environment file in the project or its `envs/` directory. Node.js, Corepack, and access to the repository and its dependencies are also required. The script expects `.next/standalone/server.js`, `.next/static/`, and `public/`; projects with different build output require adjustments. ^[how-to/docker-basics/local-prod-web/README.md:19-34]

## Usage

Pass the project root as the first argument and the environment file name or path as the second. The script changes into the project directory, so it can be invoked from any location. Without arguments, it uses the current directory and `envs/.env.PUBLIC_WEB_PROD`. Environment file names are searched for in both the project root and `envs/`; explicit relative or absolute paths are also supported. See [[Production environment file selection]]. ^[how-to/docker-basics/local-prod-web/README.md:58-85]

```bash
./run-local-prod.sh /cesta/k/projektu .env.PROD
```

After startup, the application is available at `http://localhost:3000`. Stop the server with `Ctrl+C`. ^[how-to/docker-basics/local-prod-web/README.md:87-93]

## Execution workflow

The script validates the selected environment file, temporarily moves any existing `.env` to `.env.before-local-prod`, and copies the selected configuration into `.env`. It then enables Corepack, installs dependencies with `pnpm install --frozen-lockfile`, and creates the production build with `pnpm build`. This installation step relates to [[Dependency installation with a frozen lockfile]]. ^[how-to/docker-basics/local-prod-web/README.md:97-105]

To prepare the runtime, the script copies `.next/static` and `public` into `.next/standalone`, matching the production Docker image’s packaging steps. It starts `.next/standalone/server.js` through Node.js, sets the local URL to `http://localhost:3000`, and disables Redis cache. On exit, it removes the temporary `.env` and restores the original file. ^[how-to/docker-basics/local-prod-web/README.md:106-110]

## Environment safeguards

The script stops if the selected environment file does not exist or if `.env.before-local-prod` already exists, protecting an existing backup from being overwritten. It automatically restores the original `.env` when the server stops, including through `Ctrl+C`. See [[Environment backup and restoration safeguards]]. ^[how-to/docker-basics/local-prod-web/README.md:116-122]

If an unusual termination leaves a backup behind, inspect both files before manually moving or removing the backup. ^[how-to/docker-basics/local-prod-web/README.md:124-131]

```bash
ls -l .env .env.before-local-prod
```

## Validation scope and adaptation

This workflow checks the generated production build, including the standalone server and static files. For normal development with hot reload, use `pnpm dev`. Source changes do not automatically appear in the production build; rerun the script after making changes. See [[Production build validation versus development mode]]. ^[how-to/docker-basics/local-prod-web/README.md:112-114, how-to/docker-basics/local-prod-web/README.md:147-157]

When adapting the script, check the package manager, build command, standalone server path, static asset requirements, environment file location, and URL, port, or cache settings. If only the project location or selected environment file differs, the existing arguments are sufficient. ^[how-to/docker-basics/local-prod-web/README.md:133-145]

## Sources

- [how-to/docker-basics/local-prod-web/README.md](how-to/docker-basics/local-prod-web/README.md)
