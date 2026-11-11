---
title: Runtime validation versus type assertions
summary: Type assertions do not validate or transform data; external inputs require a runtime parser, schema, or genuine type guard.
sources:
  - how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md
kind: concept
createdAt: "2026-11-11T11:05:24.076Z"
updatedAt: "2026-11-11T11:05:24.076Z"
tags:
  - typescript
  - runtime-validation
  - type-assertions
aliases:
  - runtime-validation-versus-type-assertions
  - RVVTA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Runtime validation versus type assertions

A type assertion such as `as User` tells the TypeScript compiler to trust a type claim. It does not change the data or verify its structure. External input therefore needs a parser, runtime schema, or an actual type guard. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-33]

## Assertions do not validate data

The following assertion provides no runtime validation of `response`: ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-33]

```ts
const value = response as User;
```

At application boundaries, prefer `unknown`: it requires a check before the value can be used. By contrast, `any` disables checking for that value; if its use is necessary, document the reason and keep its scope small. See [[Unknown Versus Any]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:51-57]

## Compatibility checks with `satisfies`

The [[The satisfies operator|`satisfies` operator]] checks type compatibility while preserving inference. A type assertion such as `as Config` instead asks the compiler to trust the claim and can hide an error. For external data, the source separately requires a parser, schema, or actual type guard. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-45]

```ts
type Config = { enabled: boolean };

const config = {
  enabled: true
} satisfies Config;
```

## Naming and review

Use names that distinguish runtime validation from other operations: `UserSchema` for a runtime schema, `parseUserResponse` for a parser, and `isUser` for a type guard. This follows [[Role-based naming for types and conversion functions]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:67-74]

During review, check whether safety comes from an actual check or merely an assertion, whether external input is validated at runtime, and whether `any` escapes into the rest of the application. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:76-83]

## Sources

- how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md
