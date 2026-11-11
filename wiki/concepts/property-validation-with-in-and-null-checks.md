---
title: Property Validation with in and Null Checks
summary: An unknown value can be validated by checking that it is a non-null object, that a property exists using in, and that the property has the expected type.
sources:
  - how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md
kind: concept
createdAt: "2026-11-11T11:03:48.164Z"
updatedAt: "2026-11-11T11:03:48.164Z"
tags:
  - typescript
  - runtime-validation
aliases:
  - property-validation-with-in-and-null-checks
  - Null Checks and Property Validation with in
  - PVWIANC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Property Validation with in and Null Checks

Validace vlastnosti kombinuje kontrolu objektu, vyloučení `null`, ověření přítomnosti klíče pomocí `in` a kontrolu typu jeho hodnoty. Následující vlastní type guard ověřuje, zda hodnota typu `unknown` obsahuje vlastnost `message` typu `string`. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:74-85]

```ts
const hasMessage = (value: unknown): value is { message: string } => {
  return (
    typeof value === "object" &&
    value !== null &&
    "message" in value &&
    typeof value.message === "string"
  );
};
```

## Pořadí kontrol

Podmínky nejprve ověří `typeof value === "object"` a `value !== null`. Poté `"message" in value` ověří přítomnost vlastnosti a `typeof value.message === "string"` zkontroluje její hodnotu. Samotná přítomnost klíče tak není jedinou podmínkou úspěšné validace. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:75-81]

Návratový type predicate `value is { message: string }` sděluje TypeScriptu výsledek vlastní kontroly a umožňuje [[TypeScript Type Narrowing|zúžení typu]] pro následný přístup k vlastnosti. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:3-3, how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:48-48, how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:75-81]

## Správnost kontroly

Type guard musí odpovídat skutečným datům. Chybný predicate může přesvědčit compiler, ale runtime data nezmění; deklarované vlastnosti proto musí skutečně ověřovat za běhu. Tato zásada souvisí s tématem [[Runtime validation versus type assertions]]. ^[how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:70-70, how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md:110-113]

## Sources

- [Narrowing and Type Guards](how-to/typescript-cheat-sheet/03-narrowing-and-type-guards.md)
