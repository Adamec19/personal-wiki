---
title: HTTP Methods and JSON Requests
summary: Send GET, POST, PUT, PATCH, and DELETE requests with curl, including JSON payloads supplied inline or loaded from a file.
sources:
  - how-to/curl-api/README.md
kind: concept
createdAt: "2026-11-11T10:55:07.075Z"
updatedAt: "2026-11-11T10:55:07.075Z"
tags:
  - http
  - json
  - curl
aliases:
  - http-methods-and-json-requests
  - JSON Requests and HTTP Methods
  - HMAJR
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# HTTP Methods and JSON Requests

`curl` umožňuje testovat API endpointy přímo z terminálu. Pro získání dat lze použít jednoduchý GET požadavek; příklady zápisových požadavků používají `-X` pro určení HTTP metody, `-H` pro hlavičku `Content-Type: application/json` a `-d` pro odesílaná JSON data. ^[how-to/curl-api/README.md:5-10, how-to/curl-api/README.md:14-58]

## GET požadavek

GET požadavek v uvedeném příkladu nevyžaduje explicitní určení metody. JSON odpověď lze pro přehlednější zobrazení předat příkazu `python3 -m json.tool`. ^[how-to/curl-api/README.md:14-20]

```bash
curl https://api.example.com/users

curl https://api.example.com/users | python3 -m json.tool
```

## POST s JSON daty

POST požadavek lze sestavit pomocí `-X POST`. Hlavička `Content-Type: application/json` označuje formát odesílaných dat a `-d` obsahuje JSON tělo požadavku. ^[how-to/curl-api/README.md:31-36]

```bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Martin", "email": "martin@example.com"}'
```

JSON data lze také načíst ze souboru pomocí `-d @data.json`. ^[how-to/curl-api/README.md:38-41]

```bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d @data.json
```

## PUT, PATCH a DELETE

Příklady PUT a PATCH posílají JSON data na endpoint konkrétního uživatele. DELETE používá stejný endpoint bez těla požadavku. Metodu ve všech případech určuje přepínač `-X`. ^[how-to/curl-api/README.md:46-58]

```bash
curl -X PUT https://api.example.com/users/123 \
  -H "Content-Type: application/json" \
  -d '{"name": "Martin Updated"}'

curl -X PATCH https://api.example.com/users/123 \
  -H "Content-Type: application/json" \
  -d '{"name": "Martin Patch"}'

curl -X DELETE https://api.example.com/users/123
```

## JSON požadavek s autentizací

JSON požadavek lze doplnit hlavičkou `Authorization` s Bearer tokenem, jak ukazuje příklad vytvoření záznamu ve Strapi. Data jsou v tomto příkladu zabalena do objektu `data`. Další souvislosti popisují [[API Authentication with cURL]] a [[Strapi API Requests with cURL]]. ^[how-to/curl-api/README.md:83-95]

```bash
curl -X POST http://localhost:1337/api/pages \
  -H "Authorization: Bearer tvuj-strapi-token" \
  -H "Content-Type: application/json" \
  -d '{"data": {"title": "Nová stránka", "slug": "nova-stranka"}}'
```

## Kontrola odpovědi

Pro zobrazení odpovědi včetně hlaviček lze použít `-i`; pro zobrazení pouze hlaviček slouží `-I`. Podrobnější kontrolu odpovědí rozvádí [[HTTP Response Inspection]]. ^[how-to/curl-api/README.md:22-26]

## Sources

- [cURL API — testování API z terminálu](how-to/curl-api/README.md)
