---
title: Přepínání prostředí při vývoji Insurance
summary: Frontend lze přepínat mezi lokálním backendem a jiným prostředím změnou API URL v konfiguraci projektu DIF.
sources:
  - how-to/direct-dev/README.md
kind: concept
createdAt: "2026-11-11T10:55:20.026Z"
updatedAt: "2026-11-11T10:55:20.026Z"
tags:
  - insurance
  - vývojová-prostředí
  - konfigurace
aliases:
  - přepínání-prostředí-při-vývoji-insurance
  - PPPVI
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Přepínání prostředí při vývoji Insurance

Přepínání mezi lokálním backendem a jiným prostředím při vývoji Insurance se provádí změnou API URL na frontendové straně projektu `DIF`. Konfigurace je v souboru `src/services/insurance/const.ts`. ^[how-to/direct-dev/README.md:15-19]

## Lokální prostředí

Pro připojení k lokálnímu backendu nastav v uvedeném souboru následující endpoint pro výpočet pojištění. ^[how-to/direct-dev/README.md:10-19]

```text
http://localhost:8976/restapi-property/services/rest/property/insurance/v6/calculation
```

Při přechodu na jiné prostředí uprav API URL ve stejném souboru. Souvislosti popisují [[Konfigurace API URL v projektu DIF]] a [[Lokální API pro výpočet pojištění Insurance]]. ^[how-to/direct-dev/README.md:15-19]

## Sources

- [Direct Dev — cheat sheet pro vývojáře](how-to/direct-dev/README.md)
