---
title: Generické komponenty
summary: Generická komponenta Select propojuje typ položek options s typy parametrů callbacků getValue, getLabel a onChange.
sources:
  - how-to/typescript-cheat-sheet/02-functions-and-generics.md
kind: concept
createdAt: "2026-11-11T11:03:31.901Z"
updatedAt: "2026-11-11T11:03:31.901Z"
tags:
  - typescript
  - generics
  - components
  - tsx
aliases:
  - generické-komponenty
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Generické komponenty

Generická komponenta používá typový parametr k zachování vztahu mezi svými props. Například `Select<T>` propojuje typ položek v `options` s parametry funkcí `getValue`, `getLabel` a `onChange`, takže všechny pracují se stejným typem `T`. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:75-83]

## Příklad komponenty Select

Typ `SelectProps<T>` popisuje seznam položek, funkce pro získání jejich hodnoty a popisku a callback přijímající vybranou položku. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:75-81]

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

export { Select };
```

Při změně výběru komponenta vyhledá položku podle hodnoty vrácené funkcí `getValue`. Pokud ji najde, předá ji do `onChange`. Funkce `getLabel` určuje zobrazený text jednotlivých možností. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:85-95]

## Syntaxe v TSX

Zápis `<T,>` obsahuje čárku, aby parser v souboru `.tsx` neinterpretoval generický parametr jako JSX tag. Podrobněji viz [[Syntaxe generik v TSX]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:22-28]

## Kdy generika použít

Generika mají zachovávat důležitý vztah mezi typy. U této komponenty propojují položky seznamu s funkcemi, které je zpracovávají; jejich účelem není pouze vytvářet dojem flexibility. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:75-81, how-to/typescript-cheat-sheet/02-functions-and-generics.md:110-110]

Generika nejsou vhodná, pokud komponenta vždy pracuje s jediným konkrétním typem nebo pokud zhoršují čitelnost. Business varianty mohou vyžadovat explicitní union; v jiných situacích může být srozumitelnější `unknown` s následným narrowing. Viz [[Kdy generika nepoužívat]] a [[TypeScript Type Narrowing]]. ^[how-to/typescript-cheat-sheet/02-functions-and-generics.md:103-110]

## Sources

- [Functions and Generics](how-to/typescript-cheat-sheet/02-functions-and-generics.md)
