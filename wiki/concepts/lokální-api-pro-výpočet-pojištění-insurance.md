---
title: Lokální API pro výpočet pojištění Insurance
summary: Lokální backend poskytuje výpočet pojištění na endpointu http://localhost:8976/restapi-property/services/rest/property/insurance/v6/calculation.
sources:
  - how-to/direct-dev/README.md
kind: concept
createdAt: "2026-11-11T10:55:17.416Z"
updatedAt: "2026-11-11T10:55:17.416Z"
tags:
  - insurance
  - backend
  - lokální-vývoj
aliases:
  - lokální-api-pro-výpočet-pojištění-insurance
  - LAPVPI
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Lokální API pro výpočet pojištění Insurance

Pro lokální vývoj Insurance je backendový endpoint pro výpočet pojištění dostupný na následující adrese. ^[how-to/direct-dev/README.md:8-13]

```text
http://localhost:8976/restapi-property/services/rest/property/insurance/v6/calculation
```

## Nastavení frontendu

API URL se na frontendové straně nastavuje v projektu `DIF`, v souboru `src/services/insurance/const.ts`. Zde se adresa upravuje při přepínání mezi lokálním backendem a jiným prostředím; související témata jsou [[Konfigurace API URL v projektu DIF]] a [[Přepínání prostředí při vývoji Insurance]]. ^[how-to/direct-dev/README.md:15-19]

## Sources

- [how-to/direct-dev/README.md](how-to/direct-dev/README.md)
