---
title: Schema-Derived Form Types
summary: Use a validation schema as the source of form types, deriving TypeScript types with Zod's z.infer.
sources:
  - how-to/react-cheat-sheet/04-forms.md
kind: concept
createdAt: "2026-11-11T10:58:31.176Z"
updatedAt: "2026-11-11T10:58:31.176Z"
tags:
  - forms
  - validation
  - typescript
  - zod
aliases:
  - schema-derived-form-types
  - SFT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Schema-Derived Form Types

Schema-derived form types use a validation schema as the source of a form’s TypeScript type. The example below defines `UserSchema` with Zod and derives `UserForm` through `z.infer<typeof UserSchema>`, following the principle of a [[Single source of truth for type contracts]]. ^[how-to/react-cheat-sheet/04-forms.md:14-26]

## Defining the schema and type

```tsx
import { z } from "zod";

const UserSchema = z.object({
  email: z.string().email(),
  displayName: z.string().min(1),
  phone: z.string().nullable()
});

type UserForm = z.infer<typeof UserSchema>;
```

The schema requires an email-formatted string, a display name containing at least one character, and a phone value that can be a string or `null`. `UserForm` is inferred directly from this schema. ^[how-to/react-cheat-sheet/04-forms.md:19-25]

For controlled fields, represent empty values explicitly with `null` or `""`, rather than mixing `undefined`, `null`, and empty strings. This relates to [[Explicit Empty Values in Controlled Fields]]. ^[how-to/react-cheat-sheet/04-forms.md:28-28]

## Using the type in field wrappers

A field wrapper can access the form through `useFormContext<UserForm>()` and connect a `Controller` to an input, including its validation error message. The wrapper handles form-to-UI integration; business decisions for the whole feature belong elsewhere. See [[Form Field Wrappers]]. ^[how-to/react-cheat-sheet/04-forms.md:30-50]

## Placement and submission

Within a [[Layered Form Architecture]], `models/schema.ts` holds the schema and derived type, while client interactions, field components, and submission or side-effect hooks occupy separate layers. ^[how-to/react-cheat-sheet/04-forms.md:3-12]

The [[Form Submission Pipeline]] validates form data before converting the form model into an API request, sending it, normalizing API errors, and presenting the result. API payload mapping should remain outside the JSX event handler. ^[how-to/react-cheat-sheet/04-forms.md:68-76]

## Sources

- [Forms](how-to/react-cheat-sheet/04-forms.md)
