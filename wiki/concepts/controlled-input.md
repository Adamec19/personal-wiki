---
title: Controlled input
summary: Řízený vstup přijímá hodnotu přes props a předává změny callbackem, takže správu hodnoty ponechává nadřazené komponentě.
sources:
  - how-to/react-cheat-sheet/10-component-snippets.md
kind: concept
createdAt: "2026-11-11T11:00:49.871Z"
updatedAt: "2026-11-11T11:00:49.871Z"
tags:
  - react
  - forms
  - state-management
aliases:
  - controlled-input
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Controlled input

Controlled input je komponenta, která přijímá aktuální hodnotu přes prop `value` a změny předává konzumentovi callbackem `onChange`. Ukázkový `SearchInput` tak má malý, typovaný veřejný kontrakt: `value` je `string` a `onChange` přijímá novou hodnotu typu `string`. ^[how-to/react-cheat-sheet/10-component-snippets.md:81-95]

## Implementace

Komponenta předává `value` přímo elementu `<input>`. Při změně vstupu zavolá `onChange` s `event.target.value`; text „Hledat“ je součástí obalujícího elementu `<label>`. ^[how-to/react-cheat-sheet/10-component-snippets.md:86-93]

```tsx
type SearchInputProps = {
  value: string;
  onChange: (value: string) => void;
};

const SearchInput = ({ value, onChange }: SearchInputProps) => {
  return (
    <label>
      Hledat
      <input value={value} onChange={(event) => onChange(event.target.value)} />
    </label>
  );
};

export { SearchInput };
```

## Návrhové zásady

Controlled nebo uncontrolled chování má být explicitní. Při návrhu je také potřeba ověřit malý a typovaný veřejný kontrakt, jeden účel komponenty a podporu klávesnice a screen readeru. Tyto otázky rozvádí [[Kontrolní seznam návrhu komponent]]; s kontraktem souvisí [[Component Props as a Public Contract]]. ^[how-to/react-cheat-sheet/10-component-snippets.md:128-135]

Ukázka je výchozí kostra, kterou je nutné přizpůsobit přístupnosti, design systému, zpracování chyb a datovému kontraktu konkrétní aplikace. ^[how-to/react-cheat-sheet/10-component-snippets.md:3-3]

## Sources

- [Component Snippets](how-to/react-cheat-sheet/10-component-snippets.md)
