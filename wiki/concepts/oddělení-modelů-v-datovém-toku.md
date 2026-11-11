---
title: Oddělení modelů v datovém toku
summary: Odděl UI, formulářový či doménový model, request mapper, API klienta a modely odpovědi podle účelu jednotlivých hranic.
sources:
  - how-to/react-cheat-sheet/06-api-and-data.md
kind: concept
createdAt: "2026-11-11T10:59:19.190Z"
updatedAt: "2026-11-11T10:59:19.190Z"
tags:
  - architektura
  - datový-tok
aliases:
  - oddělení-modelů-v-datovém-toku
  - OMVDT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Oddělení modelů v datovém toku

Oddělení modelů v datovém toku rozlišuje podobu dat podle účelu jednotlivých hranic aplikace. Formulářový model nemusí být totožný s daty odesílanými do API; datový tok proto zahrnuje samostatný form/domain model, request mapper, API client, response schema a UI model. ^[how-to/react-cheat-sheet/06-api-and-data.md:3-9]

## Průchod dat aplikací

```text
UI → form/domain model → request mapper → API client → response schema → UI model
```

Toto rozdělení vyjadřuje, že každá hranice má jiný účel. [[Request mapper a oddělení datových modelů|Request mapper]] tvoří přechod mezi form/domain modelem a API klientem, zatímco schéma odpovědi stojí mezi API klientem a modelem pro UI. ^[how-to/react-cheat-sheet/06-api-and-data.md:3-9]

## Ověření externích dat

Data přicházející zvenčí se považují za `unknown`, dokud je neověří schéma nebo bezpečný parser. [[Compile-time typy versus runtime validace|Runtime validace]] tak představuje explicitní krok při zpracování odpovědi API. Následující příklad ověřuje, že uživatel má řetězcové `id` a `name` a pole řetězců `roles`. ^[how-to/react-cheat-sheet/06-api-and-data.md:11-23]

```tsx
const UserResponseSchema = z.object({
  id: z.string(),
  name: z.string(),
  roles: z.array(z.string())
});

const response = UserResponseSchema.parse(await fetchUser());
```

## Sources

- how-to/react-cheat-sheet/06-api-and-data.md
