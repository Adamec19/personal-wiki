---
title: Request mapper a oddělení datových modelů
summary: Samostatný mapper převádí formulářový model na API request a soustřeďuje normalizaci, transformaci a explicitní API kontrakt mimo JSX event handlery.
sources:
  - how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md
kind: concept
createdAt: "2026-11-11T11:04:52.777Z"
updatedAt: "2026-11-11T11:04:52.777Z"
tags:
  - api
  - data-mapping
  - separation-of-concerns
aliases:
  - request-mapper-a-oddělení-datových-modelů
  - RMAODM
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Request mapper a oddělení datových modelů

Request mapper je funkce, která převádí formulářový nebo UI model na datový model API požadavku. Formulář, API request a API response nemusí sdílet stejný typ: explicitní převod mezi nimi představuje záměrnou hranici, nikoli zbytečnou duplicitu. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:18-30, how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:73-92]

## Oddělení datových modelů

Na vstupu z API má datový tok postupovat od neověřené odpovědi přes runtime schema nebo parser k validovanému API modelu a následně přes mapper k UI či doménovému modelu. Samotný TypeScript typ nezaručuje skutečný tvar dat ze serveru; tuto hranici řeší [[Compile-time typy versus runtime validace|runtime validace]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:5-30]

## Příklad request mapperu

Formulář může uchovávat jméno a příjmení odděleně, zatímco API očekává jediné pole `name`. Funkce `toCreateUserRequest` tento převod vyjadřuje explicitně a pomocí `trim()` odstraní krajní mezery výsledné hodnoty. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:75-87]

```ts
type UserForm = {
  firstName: string;
  lastName: string;
};

type CreateUserRequest = {
  name: string;
};

const toCreateUserRequest = (form: UserForm): CreateUserRequest => ({
  name: `${form.firstName} ${form.lastName}`.trim()
});

export { toCreateUserRequest };
```

## Odpovědnost mapperu

Mapper je vhodné místo pro normalizaci a transformaci dat i pro vyjádření explicitního API kontraktu. Převod má být umístěn v samostatné funkci, nikoli přímo v JSX event handleru. Tím navazuje na [[Oddělení modelů v datovém toku]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:73-92]

Při kontrole API hranice je podstatné ověřit, že request zůstává oddělený od formulářového či UI modelu. Součástí stejné kontroly je runtime validace odpovědi, odvození typu ze schematu, zúžení chyb z `unknown` a explicitní fallback chování. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:107-113]

## Sources

- [API and Runtime Validation](how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md)
