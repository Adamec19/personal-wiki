---
title: Syntaxe generik v TSX
summary: Zápis <T,> pomáhá parseru v souborech .tsx rozlišit generický parametr od JSX tagu.
sources:
  - how-to/typescript-cheat-sheet/02-functions-and-generics.md
kind: concept
createdAt: "2026-11-11T11:03:13.747Z"
updatedAt: "2026-11-11T11:03:13.747Z"
tags:
  - typescript
  - generics
  - tsx
aliases:
  - syntaxe-generik-v-tsx
  - SGVT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Syntaxe generik v TSX

V souborech `.tsx` lze generický parametr šipkové funkce zapsat jako `<T,>`. Čárka pomáhá parseru rozlišit deklaraci generika od JSX tagu. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:22-28]

## Generická funkce

Generikum zachovává vztah mezi typem vstupu a výstupu. Funkce `first` přijímá pole prvků typu `T` a vrací hodnotu typu `T | undefined`; zápis `<T,>` je vhodný i pro použití v TSX. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:19-28]

```tsx
const first = <T,>(items: T[]): T | undefined => items[0];

const firstNumber = first([1, 2, 3]);
const firstName = first(["Ada", "Grace"]);
```

## Generická komponenta

Stejný zápis používají [[Generické komponenty]]. V komponentě `Select` propojuje parametr `T` typ položek v `options` s argumenty funkcí `getValue`, `getLabel` a `onChange`. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:73-83]

```tsx
type SelectProps<T> = {
  options: T[];
  getValue: (option: T) => string;
  getLabel: (option: T) => string;
  onChange: (option: T) => void;
};

const Select = <T,>({
  options,
  getValue,
  getLabel,
  onChange,
}: SelectProps<T>) => {
  return (
    <select
      onChange={(event) => {
        const selected = options.find(
          (option) => getValue(option) === event.target.value
        );
        if (selected) onChange(selected);
      }}
    >
      {options.map((option) => (
        <option key={getValue(option)} value={getValue(option)}>
          {getLabel(option)}
        </option>
      ))}
    </select>
  );
};
```

Generikum má zachovat důležitý vztah mezi typy. Pokud existuje pouze jeden konkrétní typ nebo generikum zhoršuje čitelnost, je vhodné zvážit [[Kdy generika nepoužívat]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-110]

## Sources

- [Functions and Generics](how-to/typescript-cheat-sheet/02-functions-and-generics.md)
