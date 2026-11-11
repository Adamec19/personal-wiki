---
title: Validace externích dat
summary: Považuj externí data za unknown, dokud jejich strukturu neověří schema nebo bezpečný parser.
sources:
  - how-to/react-cheat-sheet/06-api-and-data.md
kind: concept
createdAt: "2026-11-11T10:59:17.489Z"
updatedAt: "2026-11-11T10:59:17.489Z"
tags:
  - validace
  - api
aliases:
  - validace-externích-dat
  - VED
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Validace externích dat

Externí data jsou `unknown`, dokud je neověří schéma nebo bezpečný parser. Validace tak tvoří hranici mezi přijatou odpovědí a daty, se kterými aplikace dále pracuje. Souvisí s tématem [[Compile-time typy versus runtime validace]]. ^[how-to/react-cheat-sheet/06-api-and-data.md:11-23]

## Validace odpovědi pomocí schématu

Schéma popisuje očekávanou strukturu odpovědi. Následující příklad ověřuje, že uživatel obsahuje řetězcové `id` a `name` a pole řetězců `roles`; výsledek `fetchUser()` předává metodě `parse`. ^[how-to/react-cheat-sheet/06-api-and-data.md:13-21]

```tsx
const UserResponseSchema = z.object({
  id: z.string(),
  name: z.string(),
  roles: z.array(z.string())
});

const response = UserResponseSchema.parse(await fetchUser());
```

## Umístění v datovém toku

Validace odpovědi patří za API klienta a před UI model. Jednotlivé hranice mají odlišný účel a formulářový model nemusí odpovídat API payloadu; viz [[Oddělení modelů v datovém toku]]. ^[how-to/react-cheat-sheet/06-api-and-data.md:3-9]

```text
UI → form/domain model → request mapper → API client → response schema → UI model
```

## Sources

- [API and Data](how-to/react-cheat-sheet/06-api-and-data.md)
