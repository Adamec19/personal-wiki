---
title: Bezpečné zpracování chyb typu unknown
summary: Zachycené chyby je vhodné chápat jako unknown a před přístupem k message je zúžit, protože vyhozená hodnota nemusí být instancí Error.
sources:
  - how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md
kind: concept
createdAt: "2026-11-11T11:05:00.053Z"
updatedAt: "2026-11-11T11:05:00.053Z"
tags:
  - typescript
  - error-handling
  - type-narrowing
aliases:
  - bezpečné-zpracování-chyb-typu-unknown
  - BZCTU
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Bezpečné zpracování chyb typu unknown

Chybu zachycenou pomocí `catch (error)` je vhodné považovat za `unknown`. Vyhozená hodnota nemusí být instancí `Error`, proto je před přístupem k její vlastnosti `message` potřeba ověřit její typ. Tento postup souvisí s [[TypeScript Type Narrowing|zužováním typů]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:94-105]

## Získání chybové zprávy

Funkce `getErrorMessage` přijímá hodnotu typu `unknown` a vždy vrací řetězec. Pokud kontrola `instanceof Error` uspěje, použije zprávu z chyby; pro ostatní hodnoty vrátí explicitní náhradní text. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:96-103]

```ts
const getErrorMessage = (error: unknown): string => {
  if (error instanceof Error) return error.message;
  return "Nastala neočekávaná chyba";
};

export { getErrorMessage };
```

## Zpracování chyb na API hranici

Při runtime validaci lze zvolit mezi výjimkou a návratovým výsledkem. Metoda `parse` vyhodí výjimku a hodí se tam, kde nevalidní odpověď představuje selhání. Metoda `safeParse` vrací výsledek a hodí se pro formuláře, náhradní chování nebo uživatelské chyby. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:54-71]

Součástí kontroly API hranice má být ověření, že je chyba zúžena z `unknown` a náhradní chování je explicitní. Bezpečné zpracování chyb tak doplňuje [[Compile-time typy versus runtime validace|runtime validaci vstupních dat]]. ^[how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md:107-113]

## Sources

- [API and Runtime Validation](how-to/typescript-cheat-sheet/06-api-and-runtime-validation.md)
