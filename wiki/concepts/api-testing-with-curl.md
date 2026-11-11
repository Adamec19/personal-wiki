---
title: API Testing with cURL
summary: Use curl to test API endpoints directly from a terminal and quickly verify responses without a browser or graphical API client.
sources:
  - how-to/curl-api/README.md
kind: concept
createdAt: "2026-11-11T10:55:09.814Z"
updatedAt: "2026-11-11T10:55:09.814Z"
tags:
  - curl
  - api-testing
  - command-line
aliases:
  - api-testing-with-curl
  - ATWC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# API Testing with cURL

`curl` umožňuje testovat API endpointy přímo z terminálu. Hodí se pro rychlé ověření funkčnosti endpointu, kontrolu odpovědi bez prohlížeče a testování autentizace nebo hlaviček. ^[how-to/curl-api/README.md:3-10]

## Základní požadavky

GET požadavek lze odeslat zadáním URL. Výstup ve formátu JSON lze následně zformátovat pomocí `python3 -m json.tool`. ^[how-to/curl-api/README.md:14-20]

```bash
curl https://api.example.com/users

curl https://api.example.com/users | python3 -m json.tool
```

Pro [[HTTP Methods and JSON Requests|odesílání JSON dat]] slouží hlavička `Content-Type: application/json` a přepínač `-d`. Metodu POST určuje `-X POST`; data lze zadat přímo nebo načíst ze souboru pomocí `-d @data.json`. ^[how-to/curl-api/README.md:31-42]

```bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Martin", "email": "martin@example.com"}'

curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d @data.json
```

Stejným způsobem lze zadat metody PUT, PATCH a DELETE. Příklady PUT a PATCH posílají JSON data, zatímco DELETE obsahuje pouze URL záznamu. ^[how-to/curl-api/README.md:46-58]

```bash
curl -X PUT https://api.example.com/users/123 \
  -H "Content-Type: application/json" \
  -d '{"name": "Martin Updated"}'

curl -X PATCH https://api.example.com/users/123 \
  -H "Content-Type: application/json" \
  -d '{"name": "Martin Patch"}'

curl -X DELETE https://api.example.com/users/123
```

## Autentizace

[[API Authentication with cURL]] zahrnuje Bearer token v hlavičce `Authorization`, Basic auth pomocí `-u` a API klíč předaný hlavičkou nebo query parametrem. ^[how-to/curl-api/README.md:62-79]

```bash
curl https://api.example.com/users \
  -H "Authorization: Bearer tvuj-token-zde"

curl https://api.example.com/users \
  -u username:password

curl https://api.example.com/users \
  -H "X-API-Key: tvuj-api-klic"

curl "https://api.example.com/users?api_key=tvuj-api-klic"
```

## Kontrola odpovědi

Pro [[HTTP Response Inspection|kontrolu HTTP odpovědi]] zobrazí `-i` hlavičky společně s tělem odpovědi a `-I` pouze hlavičky. Přepínač `-v` poskytne podrobný výpis komunikace. ^[how-to/curl-api/README.md:22-26, how-to/curl-api/README.md:99-103]

```bash
curl -i https://api.example.com/users
curl -I https://api.example.com/users
curl -v https://api.example.com/users
```

Samotný HTTP stavový kód lze vypsat kombinací `-o /dev/null`, `-s` a `-w "%{http_code}"`. Výsledkem je například `200` nebo `404`. ^[how-to/curl-api/README.md:123-127]

```bash
curl -o /dev/null -s -w "%{http_code}" https://api.example.com/users
```

## Práce s výstupem a přesměrováním

Pro [[cURL Output Handling|práci s výstupem]] slouží `-o`, které uloží odpověď do souboru, a `-s`, které skryje ukazatel průběhu. Přepínač `-L` následuje přesměrování 301 a 302. ^[how-to/curl-api/README.md:99-106]

```bash
curl https://api.example.com/users -o response.json
curl -L https://api.example.com/users
```

Přepínač `-k` ignoruje SSL chyby; zdroj jej uvádí pouze pro lokální vývoj, například při testování HTTPS endpointu na localhostu. ^[how-to/curl-api/README.md:107-107, how-to/curl-api/README.md:118-121]

```bash
curl -k https://localhost:3000/api/users
```

## Příklad se Strapi

[[Strapi API Requests with cURL]] mohou používat Bearer token pro získání i vytvoření záznamů. Příklad vytvoření stránky odesílá pole `title` a `slug` uvnitř objektu `data`. ^[how-to/curl-api/README.md:83-95]

```bash
curl http://localhost:1337/api/pages \
  -H "Authorization: Bearer tvuj-strapi-token"

curl -X POST http://localhost:1337/api/pages \
  -H "Authorization: Bearer tvuj-strapi-token" \
  -H "Content-Type: application/json" \
  -d '{"data": {"title": "Nová stránka", "slug": "nova-stranka"}}'
```

## Sources

- [cURL API — testování API z terminálu](how-to/curl-api/README.md)
