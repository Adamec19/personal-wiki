---
title: cURL Output Handling
summary: Save responses to files, suppress progress output, and format JSON responses through python3 -m json.tool.
sources:
  - how-to/curl-api/README.md
kind: concept
createdAt: "2026-11-11T10:55:12.606Z"
updatedAt: "2026-11-11T10:55:12.606Z"
tags:
  - curl
  - command-line
  - json
aliases:
  - curl-output-handling
  - COH
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# cURL Output Handling

Při [[API Testing with cURL|testování API pomocí cURL]] lze odpověď zobrazit v terminálu, formátovat JSON, uložit tělo odpovědi do souboru nebo vypsat pouze HTTP status code. Pro kontrolu hlaviček a podrobností komunikace slouží další přepínače. ^[how-to/curl-api/README.md:14-27, how-to/curl-api/README.md:99-126]

## Zobrazení a formátování JSON

Základní příkaz vypíše odpověď do terminálu. Přesměrování přes `python3 -m json.tool` zajistí čitelně formátovaný JSON. ^[how-to/curl-api/README.md:16-20]

```bash
curl https://api.example.com/users

curl https://api.example.com/users | python3 -m json.tool
```

## Hlavičky a diagnostika

Přepínač `-i` zobrazí hlavičky společně s tělem odpovědi, zatímco `-I` zobrazí pouze hlavičky. Pro podrobný výpis celé komunikace slouží `-v`; tyto možnosti souvisejí s [[HTTP Response Inspection|kontrolou HTTP odpovědi]]. ^[how-to/curl-api/README.md:22-26, how-to/curl-api/README.md:99-104]

```bash
curl -i https://api.example.com/users

curl -I https://api.example.com/users

curl -v https://api.example.com/users
```

## Uložení odpovědi do souboru

Pomocí `-o` lze odpověď uložit do zadaného souboru. Přepínač `-s` skryje progress bar. ^[how-to/curl-api/README.md:104-105, how-to/curl-api/README.md:113-116]

```bash
curl -s https://api.example.com/users -o response.json
```

## Výpis pouze HTTP status code

Pro výpis samotného stavového kódu lze spojit `-o /dev/null`, které zahodí tělo odpovědi, `-s` pro skrytí progress baru a `-w "%{http_code}"` pro vypsání kódu. Výsledkem je například `200` nebo `404`. ^[how-to/curl-api/README.md:123-126]

```bash
curl -o /dev/null -s -w "%{http_code}" https://api.example.com/users
```

## Sources

- [cURL API — testování API z terminálu](how-to/curl-api/README.md)
