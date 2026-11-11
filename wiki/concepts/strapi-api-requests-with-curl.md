---
title: Strapi API Requests with cURL
summary: Retrieve and create Strapi page records using Bearer authentication and a JSON request body wrapped in a data object.
sources:
  - how-to/curl-api/README.md
kind: concept
createdAt: "2026-11-11T10:55:17.677Z"
updatedAt: "2026-11-11T10:55:17.677Z"
tags:
  - strapi
  - api
  - curl
aliases:
  - strapi-api-requests-with-curl
  - SARWC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Strapi API Requests with cURL

`curl` umožňuje testovat API endpointy přímo z terminálu. U Strapi jej lze použít například k načtení stránek nebo vytvoření záznamu s autentizací pomocí Bearer tokenu. ^[how-to/curl-api/README.md:5-10, how-to/curl-api/README.md:83-95]

## Načtení stránek

Následující požadavek načte všechny stránky z endpointu `/api/pages` na lokálním Strapi serveru. Token se předává v hlavičce `Authorization`; související postupy popisuje [[API Authentication with cURL]]. ^[how-to/curl-api/README.md:85-88]

```bash
curl http://localhost:1337/api/pages \
  -H "Authorization: Bearer tvuj-strapi-token"
```

## Vytvoření záznamu

Pro vytvoření stránky se používá metoda `POST`, hlavička `Content-Type: application/json` a JSON tělo s vlastnostmi `title` a `slug` zabalenými do objektu `data`. Obecné příklady metod a JSON požadavků uvádí [[HTTP Methods and JSON Requests]]. ^[how-to/curl-api/README.md:90-94]

```bash
curl -X POST http://localhost:1337/api/pages \
  -H "Authorization: Bearer tvuj-strapi-token" \
  -H "Content-Type: application/json" \
  -d '{"data": {"title": "Nová stránka", "slug": "nova-stranka"}}'
```

## Kontrola odpovědi

Při ověřování požadavků lze pomocí `-i` zobrazit hlavičky spolu s odpovědí nebo pomocí `-v` zobrazit celou komunikaci. JSON výstup lze formátovat přes `python3 -m json.tool` a odpověď uložit pomocí `-o response.json`. Další souvislosti nabízejí [[HTTP Response Inspection]] a [[cURL Output Handling]]. ^[how-to/curl-api/README.md:19-23, how-to/curl-api/README.md:99-105, how-to/curl-api/README.md:113-116]

## Sources

- [cURL API — testování API z terminálu](how-to/curl-api/README.md)
