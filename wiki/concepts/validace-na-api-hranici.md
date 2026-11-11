---
title: Validace na API hranici
summary: Datový tok vede od neznámého vstupu přes runtime parser a validovaný API model k mapperu a UI či doménovému modelu.
sources:
  - how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md
kind: concept
createdAt: "2026-11-11T11:04:46.342Z"
updatedAt: "2026-11-11T11:04:46.342Z"
tags:
  - api
  - architecture
  - runtime-validation
aliases:
  - validace-na-api-hranici
  - VNAH
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Validace na API hranici

Validace na API hranici ověřuje za běhu, zda přijatá data odpovídají očekávanému kontraktu. TypeScript chrání kód při typové kontrole, ale nemůže zaručit skutečný obsah odpovědi serveru. Data z HTTP, JSON, localStorage, query parametrů nebo `postMessage` jsou do ověření nedůvěryhodná. Viz [[Compile-time typy versus runtime validace]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:3-16]

## Datový tok

Vstupní odpověď má procházet od `unknown` přes runtime schema nebo parser k validovanému API modelu. Mapper ji následně převádí na UI či doménový model. Formulářový model, API request a API response nemusí sdílet stejný typ; jejich převod představuje záměrnou hranici. Viz [[Oddělení modelů v datovém toku]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:18-30]

## Schema jako zdroj typu

Schema může sloužit současně jako runtime validátor a zdroj TypeScript typu. Následující příklad používá Zod a odvozuje `UserResponse` pomocí `z.infer`, aby se validace a ručně udržovaný typ nerozcházely. Viz [[Single source of truth for type contracts]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:32-52]

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

Metoda `parse` při nevalidních datech vyhodí výjimku a hodí se tam, kde nevalidní odpověď znamená selhání. `safeParse` vrací výsledek, který umožňuje explicitně zpracovat chybu, například ve formuláři nebo při použití náhradního chování. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:54-71]

```ts
const parseUserResponseSafe = (value: unknown) => {
  const result = UserResponseSchema.safeParse(value);

  if (!result.success) {
    return { data: null, error: result.error };
  }

  return { data: result.data, error: null };
};
```

## Request mapper a chyby

Request mapper je místo pro normalizaci, transformaci a vyjádření explicitního API kontraktu. Například může spojit jméno a příjmení z formuláře do jediného pole `name` v requestu. Tato transformace nemá být vložená přímo do JSX event handleru. Viz [[Request mapper a oddělení datových modelů]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:73-92]

Chybu zachycenou v `catch` je potřeba považovat za `unknown` a před použitím zúžit její typ. Ne každá vyhozená hodnota je instancí `Error`; pro ostatní případy lze vrátit explicitní náhradní zprávu. Viz [[Bezpečné zpracování chyb typu unknown]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:94-105]

## Sources

- [API and Runtime Validation](how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md)
