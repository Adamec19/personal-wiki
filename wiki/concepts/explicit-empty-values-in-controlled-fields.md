---
title: Explicit Empty Values in Controlled Fields
summary: Represent empty controlled-field values explicitly with null or an empty string instead of mixing undefined, null, and empty strings.
sources:
  - how-to/react-cheat-sheet/04-forms.md
kind: concept
createdAt: "2026-11-11T10:58:31.453Z"
updatedAt: "2026-11-11T10:58:31.453Z"
tags:
  - forms
  - controlled-inputs
  - data-modeling
aliases:
  - explicit-empty-values-in-controlled-fields
  - EEVICF
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Explicit Empty Values in Controlled Fields

U controlled fieldů je praktičtější reprezentovat prázdnou hodnotu explicitně pomocí `null` nebo `""` než směšovat `undefined`, `null` a prázdný string. Zvolená reprezentace tak dává prázdné hodnotě jasnou podobu. ^[how-to/react-cheat-sheet/04-forms.md:28-28]

## Soulad se schématem

Reprezentaci prázdné hodnoty lze vyjádřit ve schématu, ze kterého se odvozuje typ formuláře. Zdrojový příklad definuje telefon jako `z.string().nullable()`, takže připouští string nebo `null`, a typ `UserForm` odvozuje pomocí `z.infer<typeof UserSchema>`. Tento postup souvisí s konceptem [[Schema-Derived Form Types]]. ^[how-to/react-cheat-sheet/04-forms.md:14-26]

## Napojení na UI a odeslání

[[Form Field Wrappers|Field wrapper]] propojuje formulář s UI primitive; v uvedeném příkladu předává `field` do komponenty `Input` a doplňuje chybovou zprávu. Business rozhodnutí celé feature do wrapperu nepatří. ^[how-to/react-cheat-sheet/04-forms.md:30-50]

Převod formulářového modelu na API request má vlastní místo v [[Form Submission Pipeline|procesu odeslání]]: následuje po validaci a před odesláním requestu. Mapování API payloadu nemá být přímo v JSX event handleru. ^[how-to/react-cheat-sheet/04-forms.md:68-76]

## Sources

- [Forms](how-to/react-cheat-sheet/04-forms.md)
