---
title: Utility types v TypeScriptu
summary: Odvozují nové typy z existujících a snižují duplicitu, aniž by měly skrývat důležitý business kontrakt.
sources:
  - how-to/typescript-cheat-sheet/04-utility-types.md
kind: concept
createdAt: "2026-11-11T11:04:02.312Z"
updatedAt: "2026-11-11T11:04:02.312Z"
tags:
  - typescript
  - typový-systém
aliases:
  - utility-types-v-typescriptu
  - UTVT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Utility types v TypeScriptu

Utility types odvozují nové typy z existujících a snižují duplicitu. Při jejich použití by však měl zůstat čitelný důležitý business kontrakt. ^[how-to/typescript-cheat-sheet/04-utility-types.md:1-3]

## Úprava vlastností: `Partial`, `Required`, `Readonly`

Utility [[Partial, Required a Readonly]] umožňují odvodit varianty existujícího objektového typu. `Partial` se hodí například pro patch request, nemá však nahrazovat přesný typ formuláře. ^[how-to/typescript-cheat-sheet/04-utility-types.md:5-19]

```ts
type User = {
  id: string;
  name: string;
  email: string;
};

type UserPatch = Partial<User>;
type CompleteUser = Required<User>;
type ImmutableUser = Readonly<User>;
```

## Výběr vlastností: `Pick` a `Omit`

[[Pick a Omit]] použijeme tehdy, když nový typ skutečně reprezentuje podmnožinu původního kontraktu. Následující příklad vybírá `id` a `name`, případně vytváří variantu bez `email`. ^[how-to/typescript-cheat-sheet/04-utility-types.md:21-28]

```ts
type UserPreview = Pick<User, "id" | "name">;
type UserWithoutEmail = Omit<User, "email">;
```

## Kontrola klíčů pomocí `Record`

[[Record v kombinaci se satisfies]] hlídá, že v objektu nechybí žádný požadovaný klíč a nepřibyl překlep. Příkladem je slovník popisků pro jednotlivá oprávnění. ^[how-to/typescript-cheat-sheet/04-utility-types.md:30-42]

```ts
type Permission = "read" | "write" | "delete";

const permissionLabels = {
  read: "Číst",
  write: "Upravovat",
  delete: "Mazat"
} satisfies Record<Permission, string>;
```

## Odvození typů z funkcí

[[ReturnType a Parameters]] jsou užitečné, pokud je funkce zdrojem pravdy: umožňují odvodit typ jejího výsledku a parametrů bez ručního duplikování signatury. ^[how-to/typescript-cheat-sheet/04-utility-types.md:44-57]

```ts
const createUser = (name: string, role: string) => ({
  id: crypto.randomUUID(),
  name,
  role
});

type CreatedUser = ReturnType<typeof createUser>;
type CreateUserArgs = Parameters<typeof createUser>;
```

## Práce s union typy

[[NonNullable, Extract a Exclude]] umožňují odvodit typ bez `null` a `undefined`, vybrat určité členy union typu nebo některé členy vyloučit. ^[how-to/typescript-cheat-sheet/04-utility-types.md:59-68]

```ts
type MaybeUser = User | null | undefined;
type UserOnly = NonNullable<MaybeUser>;

type Events = "created" | "updated" | "deleted";
type WriteEvents = Extract<Events, "created" | "updated">;
type ReadOnlyEvents = Exclude<Events, "deleted">;
```

## Výsledek asynchronní funkce

[[Awaited]] lze kombinovat s `ReturnType` pro odvození typu výsledné hodnoty asynchronní funkce. ^[how-to/typescript-cheat-sheet/04-utility-types.md:70-75]

```ts
const loadUser = async () => ({ id: "1", name: "Ada" });
type LoadedUser = Awaited<ReturnType<typeof loadUser>>;
```

## Kdy vytvořit vlastní utility type

Před vytvořením vlastního utility typu je vhodné zvážit standardní utility, [[TypeScript Indexed Access Types|indexed access]] nebo [[The satisfies operator|satisfies]]. [[Návrh vlastních utility typů|Vlastní utility typ]] má smysl, když se daný vzor opakuje a jeho pojmenování zlepší čitelnost. ^[how-to/typescript-cheat-sheet/04-utility-types.md:77-79]

## Sources

- [Utility Types](how-to/typescript-cheat-sheet/04-utility-types.md)
