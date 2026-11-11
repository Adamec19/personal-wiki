---
title: HTTP Response Inspection
summary: Inspect response headers, verbose communication details, and HTTP status codes using curl options.
sources:
  - how-to/curl-api/README.md
kind: concept
createdAt: "2026-11-11T10:55:08.954Z"
updatedAt: "2026-11-11T10:55:08.954Z"
tags:
  - http
  - debugging
  - curl
aliases:
  - http-response-inspection
  - HRI
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# HTTP Response Inspection

Kontrola HTTP odpovědi pomocí `curl` umožňuje ověřit funkčnost API endpointu a prozkoumat jeho výstup přímo z terminálu. Hodí se také při ladění odpovědí bez prohlížeče nebo testování autentizace a hlaviček. ^[how-to/curl-api/README.md:5-10]

## Tělo odpovědi a JSON

Základní požadavek vypíše odpověď endpointu do terminálu. JSON lze pro přehlednější čtení předat příkazu `python3 -m json.tool`. ^[how-to/curl-api/README.md:14-20]

```bash
curl https://api.example.com/users

curl https://api.example.com/users | python3 -m json.tool
```

## Hlavičky odpovědi

Přepínač `-i` zobrazí spolu s odpovědí také její hlavičky. Pro zobrazení pouze hlaviček bez těla slouží `-I`. ^[how-to/curl-api/README.md:22-26]

```bash
curl -i https://api.example.com/users

curl -I https://api.example.com/users
```

## HTTP stavový kód

Pokud je potřeba pouze HTTP stavový kód, lze spojit `-o /dev/null`, `-s` a `-w "%{http_code}"`. Výsledkem je samotné číslo, například `200` nebo `404`. ^[how-to/curl-api/README.md:123-126]

```bash
curl -o /dev/null -s -w "%{http_code}" https://api.example.com/users
```

## Podrobnosti komunikace a uložení výstupu

Přepínač `-v` zobrazí celou komunikaci a `-s` skryje ukazatel průběhu. Odpověď lze uložit do souboru pomocí `-o`; další práce s výstupem souvisí s [[cURL Output Handling]]. ^[how-to/curl-api/README.md:99-105]

```bash
curl -v https://api.example.com/users

curl https://api.example.com/users -o response.json
```

Při kontrole endpointů s přesměrováním lze použít `-L`, který následuje přesměrování `301` a `302`. Kontrola odpovědí je součástí širšího [[API Testing with cURL|testování API pomocí cURL]]. ^[how-to/curl-api/README.md:5-10, how-to/curl-api/README.md:106-106]

## Sources

- [cURL API — testování API z terminálu](how-to/curl-api/README.md)
