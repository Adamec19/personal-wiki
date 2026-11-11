---
title: Environment backup and restoration safeguards
summary: The script preserves the original .env, rejects missing configuration or an existing backup, and restores the original file on normal exit or Ctrl+C.
sources:
  - how-to/docker-basics/local-prod-web/README.md
kind: concept
createdAt: "2026-11-11T10:56:22.726Z"
updatedAt: "2026-11-11T10:56:22.726Z"
tags:
  - configuration
  - safety
  - process-lifecycle
aliases:
  - environment-backup-and-restoration-safeguards
  - restoration safeguards and Environment backup
  - EBARS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Environment backup and restoration safeguards

The `run-local-prod.sh` utility temporarily replaces a project's `.env` file with a selected environment configuration to validate a production build locally. Its safeguards preserve the original configuration, prevent an existing backup from being overwritten, and restore the original `.env` when the process ends. ^[how-to/docker-basics/local-prod-web/README.md:97-110] ^[how-to/docker-basics/local-prod-web/README.md:116-122]

## Backup and restoration lifecycle

Before changing the environment configuration, the script checks that the selected env file exists. If a local `.env` is present, it temporarily moves that file to `.env.before-local-prod`. It then copies the selected configuration into `.env`, the location expected by the application and build. See [[Production environment file selection]] for the configuration selection step. ^[how-to/docker-basics/local-prod-web/README.md:97-102]

After the process ends, the script removes the temporary `.env` and restores the original file. Restoration also happens when the server is stopped with `Ctrl+C`. This supports [[Local production execution without Docker]] while preserving the project's existing local environment configuration. ^[how-to/docker-basics/local-prod-web/README.md:110-122]

## Conditions that stop execution

The script exits with an error if the selected env file does not exist. It also refuses to start another run when `.env.before-local-prod` already exists, protecting that backup from being overwritten. ^[how-to/docker-basics/local-prod-web/README.md:118-120]

## Recovery after an abnormal termination

An unusual termination can leave `.env.before-local-prod` in place. Before manually moving or removing the backup, inspect both files using the following command. ^[how-to/docker-basics/local-prod-web/README.md:124-131]

```bash
ls -l .env .env.before-local-prod
```

## Sources

- [Lokální spuštění produkčního buildu podobně jako v Dockeru](how-to/docker-basics/local-prod-web/README.md)
