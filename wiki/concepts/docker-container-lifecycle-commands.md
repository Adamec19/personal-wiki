---
title: Docker container lifecycle commands
summary: Inspect running or stopped database containers and control their lifecycle with docker ps, docker stop, and docker start.
sources:
  - how-to/direct-dev/strapi/README.md
kind: concept
createdAt: "2026-11-11T10:55:45.507Z"
updatedAt: "2026-11-11T10:55:45.507Z"
tags:
  - docker
  - container-management
aliases:
  - docker-container-lifecycle-commands
  - DCLC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Docker container lifecycle commands

Docker container lifecycle commands cover creating, listing, stopping, and starting containers. The source examples use PostgreSQL containers named `postgres_strapi` and `postgres_strapi_2` for Strapi databases. ^[how-to/direct-dev/strapi/README.md:3-25, how-to/direct-dev/strapi/README.md:96-104]

## Create a container

The following command creates and starts `postgres_strapi` using the `postgres:15` image. It configures database credentials, maps port `5432`, and uses the named volume `postgres_strapi_data` for PostgreSQL data. See [[PostgreSQL containers for Strapi]] for the database setup context. ^[how-to/direct-dev/strapi/README.md:5-14]

```bash
docker run -d --name postgres_strapi \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=direct \
  -e POSTGRES_DB=postgres_strapi \
  -p 5432:5432 \
  -v postgres_strapi_data:/var/lib/postgresql/data \
  postgres:15
```

## List containers

Use `docker ps` to list running containers and `docker ps -a` to list all containers. ^[how-to/direct-dev/strapi/README.md:98-104]

```bash
docker ps
docker ps -a
```

## Stop and start a container

Use `docker stop` to stop `postgres_strapi` and `docker start` to start it again. ^[how-to/direct-dev/strapi/README.md:98-104]

```bash
docker stop postgres_strapi
docker start postgres_strapi
```

## Switch containers during database maintenance

The password-transfer workflow stops `postgres_strapi`, runs a clean `postgres_strapi_2` on port `5432`, and starts Strapi to register an administrator. After retrieving the password hash, it stops Strapi and the temporary database container, then starts the original container again. This sequence supports [[Resetting a Strapi administrator password by transferring its hash]]. ^[how-to/direct-dev/strapi/README.md:44-82]

## Sources

- [Strapi Database - Quick Commands](how-to/direct-dev/strapi/README.md)
