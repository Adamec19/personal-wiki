---
title: Compile-time typy versus runtime validace
summary: TypeScript typy nezaručují strukturu externích dat; data z HTTP, JSON či dalších vstupů je nutné ověřit za běhu.
sources:
  - how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md
kind: concept
createdAt: "2026-11-11T11:04:45.266Z"
updatedAt: "2026-11-11T11:04:45.266Z"
tags:
  - typescript
  - runtime-validation
aliases:
  - compile-time-typy-versus-runtime-validace
  - CTVRV
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Compile-time typy versus runtime validace

TypeScript typy chrání kód při vývoji, ale nezaručují skutečný tvar dat získaných za běhu. Ani přiřazení výsledku `fetchUser()` do proměnné typu `User` nezaručuje, že server vrátil požadované vlastnosti. Data z HTTP, JSON, localStorage, query parametrů nebo `postMessage` jsou nedůvěryhodná, dokud neprojdou runtime ověřením. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:3-16]

## Validace na hranici aplikace

Vstupní data mají projít od hodnoty `unknown` přes runtime schema nebo parser k ověřenému API modelu. Mapper je následně převádí na UI nebo doménový model. Formulářový model, API request a API response nemusí sdílet stejný typ; jejich oddělení představuje záměrnou hranici v datovém toku. Viz [[Oddělení modelů v datovém toku]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:18-30]

## Schema jako zdroj typu

Runtime schema může být společným zdrojem validace i TypeScript typu. Následující příklad používá Zod a odvozuje typ pomocí `z.infer`, aby se ručně napsaný typ nerozcházel se schematem. Tento přístup souvisí s [[Single source of truth for type contracts]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:32-52]

```ts
import { z } from "zod/v4";

const UserResponseSchema = z.object({
  id: z.string(),
  name: z.string(),
  roles: z.array(z.string())
});

type UserResponse = z.infer<typeof UserResponseSchema>;

const parseUserResponse = (value: unknown): UserResponse => {
  return UserResponseSchema.parse(value);
};
```

## Zpracování nevalidních dat

Metoda `parse` při nevalidních datech vyhodí výjimku a hodí se tam, kde nevalidní odpověď představuje selhání. Metoda `safeParse` vrací výsledek, jehož větev lze rozlišit pomocí `success`; hodí se pro formuláře, náhradní chování nebo uživatelské chyby. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:54-71]

Také zachycené chyby je potřeba považovat za `unknown`: ne každá vyhozená hodnota je instancí `Error`. Přístup k `error.message` proto vyžaduje předchozí zúžení, například pomocí `instanceof Error`, a explicitní náhradní zprávu pro ostatní hodnoty. Viz [[Bezpečné zpracování chyb typu unknown]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:94-105]

## Sources

- how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md
