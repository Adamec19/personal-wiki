---
title: Const assertions with satisfies
summary: Combine as const and satisfies to preserve literal types while checking configuration structure, then derive valid keys with keyof typeof.
sources:
  - how-to/typescript-cheat-sheet/09-snippets.md
kind: concept
createdAt: "2026-11-11T11:05:37.707Z"
updatedAt: "2026-11-11T11:05:37.707Z"
tags:
  - typescript
  - type-inference
  - configuration
aliases:
  - const-assertions-with-satisfies
  - CAWS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# [[const-assertions|Const Assertions]] with satisfies

Kombinace `as const satisfies` umožňuje definovat konfigurační objekt s konkrétními hodnotami a současně jej ověřit vůči požadovanému typu. Ukázka spojuje [[Const Assertions|const assertion]] s operátorem [[The satisfies operator|satisfies]] a typem `Record<string, ProductConfig>`. ^[how-to/typescript-cheat-sheet/09-snippets.md:3-17]

## Příklad konfigurace

Typ `ProductConfig` určuje strukturu položek: textový `label` a boolean `enabled`. Objekt `PRODUCTS` obsahuje dvě pojmenované konfigurace a používá `as const satisfies Record<string, ProductConfig>`. ^[how-to/typescript-cheat-sheet/09-snippets.md:6-14]

```ts
type ProductConfig = {
  label: string;
  enabled: boolean;
};

const PRODUCTS = {
  basic: { label: "Basic", enabled: true },
  premium: { label: "Premium", enabled: false }
} as const satisfies Record<string, ProductConfig>;

type ProductCode = keyof typeof PRODUCTS;
```

Typ `ProductCode` se odvozuje přímo z klíčů objektu pomocí `keyof typeof PRODUCTS`; v této ukázce tedy odpovídá unii `"basic" | "premium"`. Konfigurace tak zároveň poskytuje podklad pro odvození typu svých identifikátorů. ^[how-to/typescript-cheat-sheet/09-snippets.md:11-16]

## Sources

- [TypeScript Snippets](how-to/typescript-cheat-sheet/09-snippets.md)
