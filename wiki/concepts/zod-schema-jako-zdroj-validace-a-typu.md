---
title: Zod schema jako zdroj validace a typu
summary: Zod schema definuje runtime validaci a pomocí z.infer poskytuje TypeScript typ, čímž předchází rozcházení definic.
sources:
  - how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md
kind: concept
createdAt: "2026-11-11T11:04:50.257Z"
updatedAt: "2026-11-11T11:04:50.257Z"
tags:
  - zod
  - typescript
  - schema-validation
aliases:
  - zod-schema-jako-zdroj-validace-a-typu
  - ZSJZVAT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Zod schema jako zdroj validace a typu

Zod schema slouží jako společný zdroj runtime validace a TypeScript typu. Typ se odvozuje pomocí `z.infer`, aby se ručně napsaná definice typu nerozcházela se schématem. Tento přístup podporuje [[Single source of truth for type contracts|jediný zdroj pravdy pro typové kontrakty]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:32-52]

## Proč validovat za běhu

TypeScript typ sám nezaručuje, že server vrátí očekávanou strukturu. Data z HTTP, JSON, localStorage, query parametrů nebo `postMessage` jsou nedůvěryhodná, dokud neprojdou ověřením za běhu; podrobněji viz [[Compile-time typy versus runtime validace]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:3-16]

## Definice schématu a odvození typu

Schéma popisuje očekávanou odpověď a parser přijímá vstup typu `unknown`. V následujícím příkladu se `UserResponse` odvozuje přímo ze schématu, které zároveň ověřuje vstupní data. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:34-52]

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

export { UserResponseSchema, parseUserResponse };
```

## Volba mezi `parse` a `safeParse`

Metoda `parse` při nevalidním vstupu vyhodí výjimku a hodí se tam, kde nevalidní odpověď znamená selhání. Metoda `safeParse` vrací výsledek, takže je vhodná pro formuláře, fallback chování nebo uživatelské chyby. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:54-71]

```ts
const parseUserResponseSafe = (value: unknown) => {
  const result = UserResponseSchema.safeParse(value);

  if (!result.success) {
    return { data: null, error: result.error };
  }

  return { data: result.data, error: null };
};
```

## Umístění na API hranici

Validace patří mezi neověřenou odpověď a validovaný API model. Následný mapper převádí API model na UI nebo doménový model. Formulářový model, API request a API response nemusí sdílet stejný typ; jejich oddělení představuje záměrnou hranici, viz [[Oddělení modelů v datovém toku]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:18-30]

```text
unknown response
  → runtime schema/parser
  → validated API model
  → mapper
  → UI/domain model
```

## Sources

- how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md
