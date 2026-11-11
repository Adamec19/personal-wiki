---
title: API Authentication with cURL
summary: Authenticate requests using Bearer tokens, Basic authentication, or API keys supplied in headers or query parameters.
sources:
  - how-to/curl-api/README.md
kind: concept
createdAt: "2026-11-11T10:55:02.640Z"
updatedAt: "2026-11-11T10:55:02.640Z"
tags:
  - authentication
  - api
  - curl
aliases:
  - api-authentication-with-curl
  - AAWC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# API Authentication with cURL

`curl` can test API authentication directly from the terminal. The source demonstrates Bearer tokens, Basic authentication, and API keys supplied through headers or query parameters. ^[how-to/curl-api/README.md:5-10, how-to/curl-api/README.md:62-79]

## Bearer token

Pass a Bearer token in the `Authorization` header using `-H`. The source presents this method for JWTs and API keys. ^[how-to/curl-api/README.md:65-67]

```bash
curl https://api.example.com/users \
  -H "Authorization: Bearer tvuj-token-zde"
```

## Basic authentication

Use `-u` to provide a username and password separated by a colon. ^[how-to/curl-api/README.md:69-71]

```bash
curl https://api.example.com/users \
  -u username:password
```

## API key

An API key can be supplied in a header. The example uses `X-API-Key`. ^[how-to/curl-api/README.md:73-75]

```bash
curl https://api.example.com/users \
  -H "X-API-Key: tvuj-api-klic"
```

The source also demonstrates supplying an API key as the `api_key` query parameter. ^[how-to/curl-api/README.md:77-78]

```bash
curl "https://api.example.com/users?api_key=tvuj-api-klic"
```

## Strapi example

For [[Strapi API Requests with cURL]], the example authenticates a request to the local `/api/pages` endpoint with a Strapi Bearer token. ^[how-to/curl-api/README.md:83-88]

```bash
curl http://localhost:1337/api/pages \
  -H "Authorization: Bearer tvuj-strapi-token"
```

## Inspecting responses

When testing authentication, use `-i` to include response headers or `-v` to display the full communication. See [[HTTP Response Inspection]] and [[API Testing with cURL]] for related concepts. ^[how-to/curl-api/README.md:22-23, how-to/curl-api/README.md:99-104]

## Sources

- how-to/curl-api/README.md
