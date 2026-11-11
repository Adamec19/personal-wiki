---
title: Form Field Wrappers
summary: Use field wrappers to connect form state and validation errors to UI primitives while keeping feature-level business decisions outside them.
sources:
  - how-to/react-cheat-sheet/04-forms.md
kind: concept
createdAt: "2026-11-11T10:58:37.263Z"
updatedAt: "2026-11-11T10:58:37.263Z"
tags:
  - forms
  - ui-components
  - separation-of-concerns
aliases:
  - form-field-wrappers
  - FFW
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Form Field Wrappers

Field wrapper propojuje formulář s UI primitivou. Jeho odpovědností je napojení pole na formulářový stav a předání validační chyby do UI komponenty. Nemá obsahovat business rozhodnutí celé feature. ^[how-to/react-cheat-sheet/04-forms.md:30-50]

## Příklad napojení

Komponenta `TextField` získává `control` pomocí `useFormContext<UserForm>()` a předává jej spolu s názvem pole komponentě `Controller`. Ta poskytuje `field` pro napojení komponenty `Input` a `fieldState` pro zobrazení chybové zprávy. Povolené názvy polí jsou omezené na `"email"` a `"displayName"`. ^[how-to/react-cheat-sheet/04-forms.md:33-45]

```tsx
const TextField = ({ name }: { name: "email" | "displayName" }) => {
  const { control } = useFormContext<UserForm>();

  return (
    <Controller
      control={control}
      name={name}
      render={({ field, fieldState }) => (
        <Input {...field} error={fieldState.error?.message} />
      )}
    />
  );
};

export { TextField };
```

## Hranice odpovědnosti

V rámci [[Layered Form Architecture]] patří field komponenty a sekce do `components/`, zatímco submit a vedlejší efekty mají vlastní hooky. Reakce na změny polí se oddělují do hooku s úklidem subscription; souvisejícím tématem je [[Form Side-Effect Hooks and Subscription Cleanup]]. ^[how-to/react-cheat-sheet/04-forms.md:5-12, how-to/react-cheat-sheet/04-forms.md:52-65]

Pro controlled pole je vhodné zvolit explicitní prázdnou hodnotu, například `null` nebo `""`, místo směšování `undefined`, `null` a prázdného řetězce. Tuto konvenci rozvádí [[Explicit Empty Values in Controlled Fields]]. ^[how-to/react-cheat-sheet/04-forms.md:28-28]

## Sources

- [Forms](how-to/react-cheat-sheet/04-forms.md)
