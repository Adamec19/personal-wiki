---
title: Type Aliases and Interfaces
summary: Use type aliases for type compositions and interfaces for extensible or implementable object contracts, maintaining codebase consistency.
sources:
  - how-to/typescript-cheat-sheet/01-type-system-basics.md
kind: concept
createdAt: "2026-11-11T11:02:47.263Z"
updatedAt: "2026-11-11T11:02:47.263Z"
tags:
  - typescript
  - type-aliases
  - interfaces
aliases:
  - type-aliases-and-interfaces
  - Interfaces and Type Aliases
  - TAAI
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Type Aliases and Interfaces

TypeScript nabízí `type` a `interface` pro zápis typových kontraktů. Obě varianty lze použít k popisu objektu; zdroj ukazuje `type` pro objekt `User` a `interface` pro generický kontrakt `Repository<T>`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:22-33]

## Příklady

Typový alias pomocí `type` popisuje uživatele s vlastnostmi `id` a `name`, oběma typu `string`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:24-28]

```ts
type User = {
  id: string;
  name: string;
};
```

Rozhraní `Repository<T>` definuje metodu `findById`, která přijímá řetězcové ID a vrací `Promise<T | null>`. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:30-32]

```ts
interface Repository<T> {
  findById(id: string): Promise<T | null>;
}
```

## Kdy použít kterou variantu

`type` je vhodný pro [[Union and Literal Types|union]], intersection, tuple, [[TypeScript Mapped Types|mapped]] a [[TypeScript Conditional Types|conditional]] typy. `interface` je vhodný pro objektový kontrakt, který se může rozšířit nebo implementovat. Nejdůležitějším praktickým pravidlem je konzistence v rámci jednoho codebase. ^[how-to/typescript-cheat-sheet/01-type-system-basics.md:35-39]

## Sources

- [Type System Basics](how-to/typescript-cheat-sheet/01-type-system-basics.md)
