---
title: Konfigurace API URL v projektu DIF
summary: URL pojišťovacího API se na frontendu projektu DIF upravuje v souboru src/services/insurance/const.ts.
sources:
  - how-to/direct-dev/README.md
kind: concept
createdAt: "2026-11-11T10:55:17.405Z"
updatedAt: "2026-11-11T10:55:17.405Z"
tags:
  - DIF
  - frontend
  - konfigurace
aliases:
  - konfigurace-api-url-v-projektu-dif
  - KAUVPD
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Konfigurace API URL v projektu DIF

API URL pro Insurance se na frontendové straně projektu `DIF` nastavuje v souboru `src/services/insurance/const.ts`. Změnou URL v tomto souboru lze přepínat mezi lokálním backendem a jiným prostředím. ^[how-to/direct-dev/README.md:15-19]

## Lokální backend

Pro [[Lokální API pro výpočet pojištění Insurance|lokální výpočet pojištění Insurance]] je uveden následující backendový endpoint. Při přepnutí na lokální backend nastavte v souboru `src/services/insurance/const.ts` tuto adresu. ^[how-to/direct-dev/README.md:10-19]

```text
http://localhost:8976/restapi-property/services/rest/property/insurance/v6/calculation
```

## Sources

- [Direct Dev — cheat sheet pro vývojáře](how-to/direct-dev/README.md)
