---
title: The satisfies operator
summary: Use satisfies to check type compatibility while preserving inference instead of relying on assertions that can conceal errors.
sources:
  - how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md
kind: concept
createdAt: "2026-11-11T11:05:26.428Z"
updatedAt: "2026-11-11T11:05:26.428Z"
tags:
  - typescript
  - type-inference
  - type-safety
aliases:
  - the-satisfies-operator
  - TSO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# The satisfies operator

Operátor `satisfies` v TypeScriptu kontroluje kompatibilitu hodnoty s požadovaným typem a zachovává přitom odvození jejího typu (inference). ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:35-45]

## Použití

V následujícím příkladu `satisfies Config` ověřuje kompatibilitu objektu s typem `Config`, aniž by potlačil odvození typu objektu. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:37-45]

```ts
type Config = { enabled: boolean };

const config = {
  enabled: true
} satisfies Config;
```

## Rozdíl oproti type assertion

Zatímco `satisfies` kompatibilitu kontroluje, assertion `as Config` říká compileru, aby deklarovanému typu důvěřoval, a může tak skrýt chybu. Assertion proto není náhradou za kontrolu kompatibility. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:35-45]

Kontrolu typů je také potřeba odlišovat od [[Runtime validation versus type assertions|runtime validace]]: `as User` externí data nezmění ani neověří. Pro externí vstup zdroj doporučuje parser, schema nebo skutečný type guard. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-33]

## Související koncepty

[[Const Assertions|`as const`]] má jiný účel: zužuje literály a přidává readonly charakter. Hodí se pro konstantní konfigurace, mapy a seznamy hodnot; nemá sloužit jako automatická oprava chyby související s mutabilitou. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:47-49]

## Sources

- [Patterns and Pitfalls](how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md)
