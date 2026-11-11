---
title: Zod parse versus safeParse
summary: parse při nevalidních datech vyhodí výjimku, zatímco safeParse vrací výsledek umožňující explicitní zpracování chyby či fallbacku.
sources:
  - how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md
kind: concept
createdAt: "2026-11-11T11:04:51.569Z"
updatedAt: "2026-11-11T11:04:51.569Z"
tags:
  - zod
  - error-handling
  - runtime-validation
aliases:
  - zod-parse-versus-safeparse
  - ZPVS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Zod parse versus safeParse

Zod nabízí dvě možnosti runtime validace: `parse` při nevalidním vstupu vyhodí výjimku, zatímco `safeParse` vrátí výsledek, který lze explicitně zpracovat. Volba závisí na tom, jak má aplikace reagovat na nevalidní data. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:54-71]

## Proč validovat za běhu

TypeScript nezaručuje, že data ze serveru odpovídají deklarovanému typu. Vstupy z HTTP, JSON, localStorage, query parametrů nebo `postMessage` jsou nedůvěryhodné, dokud neprojdou runtime validací. Tuto hranici popisuje také [[Compile-time typy versus runtime validace]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:3-16]

## `parse`: chyba jako výjimka

Metoda `parse` se hodí tam, kde nevalidní odpověď představuje selhání. Následující funkce přijímá `unknown` a vrací model ověřený schématem; při nevalidním vstupu vyhodí výjimku. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:34-47, how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:70-71]

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

Schéma slouží jako zdroj runtime validace i TypeScript typu. Odvození pomocí `z.infer` předchází rozcházení schématu a ručně napsaného typu, v souladu s principem [[Single source of truth for type contracts]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:43-52]

## `safeParse`: chyba jako výsledek

Metoda `safeParse` se hodí pro formuláře, fallback nebo uživatelskou chybu. Výsledek se kontroluje přes `success`: při neúspěchu je dostupné `error`, při úspěchu validovaná `data`. Ukázka tento výsledek převádí na objekt s explicitními hodnotami `data` a `error`. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:56-71]

```ts
const parseUserResponseSafe = (value: unknown) => {
  const result = UserResponseSchema.safeParse(value);

  if (!result.success) {
    return { data: null, error: result.error };
  }

  return { data: result.data, error: null };
};
```

## Umístění validace

Validace patří na hranici API: neznámá odpověď projde runtime schématem nebo parserem, vznikne validovaný API model a mapper jej následně převede na UI či doménový model. Formulářový model, API request a API response přitom nemusí sdílet jeden typ; viz [[Oddělení modelů v datovém toku]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:18-30]

## Sources

- [API and Runtime Validation](how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md)
