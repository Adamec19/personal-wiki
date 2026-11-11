---
title: Typově bezpečný přístup k vlastnostem pomocí keyof a T[K]
summary: K extends keyof T omezuje klíč na klíče objektu a indexed access type T[K] určuje odpovídající typ hodnoty.
sources:
  - how-to/typescript-cheat-sheet/02-functions-and-generics.md
kind: concept
createdAt: "2026-11-11T11:03:13.550Z"
updatedAt: "2026-11-11T11:03:13.550Z"
tags:
  - typescript
  - generics
  - keyof
  - indexed-access-types
aliases:
  - typově-bezpečný-přístup-k-vlastnostem-pomocí-keyof-a-tk
  - TBPKVPKAT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Typově bezpečný přístup k vlastnostem pomocí keyof a T[K]

`keyof T` představuje union klíčů typu `T`, zatímco `T[K]` označuje typ hodnoty konkrétního klíče. Jejich kombinace umožňuje napsat generickou funkci, která přijímá klíč daného objektu a zachovává odpovídající návratový typ. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:44-55]

## Generická funkce pro čtení vlastností

Funkce `getProperty` používá parametr `T` pro typ objektu a parametr `K extends keyof T` pro omezení klíče na jeho vlastnosti. Návratový typ `T[K]` propojuje vybraný klíč s typem vrácené hodnoty. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:46-55]

```ts
const getProperty = <T, K extends keyof T>(object: T, key: K): T[K] => {
  return object[key];
};

const user = { id: "1", age: 37 };
const age = getProperty(user, "age");
```

Při volání `getProperty(user, "age")` odpovídá návratový typ vlastnosti `age`, tedy `number`. Funkce tak zachovává vztah mezi vstupem a výstupem, který je hlavním účelem generik. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:19-26, how-to/typescript-cheat-sheet/02-functions-and-generics.md:46-55]

## Související koncepty

Omezení parametru `K` navazuje na [[Omezení generických typů pomocí extends]]. Zápis `T[K]` podrobněji souvisí s [[TypeScript Indexed Access Types]]. Generika mají smysl tehdy, když zachovávají důležitý vztah mezi typy; jejich použití nemá pouze vytvářet dojem flexibility. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:30-55, how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-110]

## Sources

- [Functions and Generics](how-to/typescript-cheat-sheet/02-functions-and-generics.md)
