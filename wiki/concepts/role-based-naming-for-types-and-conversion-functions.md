---
title: Role-based naming for types and conversion functions
summary: Use consistent names that distinguish models, forms, responses, status unions, runtime schemas, parsers, mappers, and type guards.
sources:
  - how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md
kind: concept
createdAt: "2026-11-11T11:05:38.583Z"
updatedAt: "2026-11-11T11:05:38.583Z"
tags:
  - typescript
  - naming-conventions
  - code-readability
aliases:
  - role-based-naming-for-types-and-conversion-functions
  - conversion functions and Role-based naming for types
  - RNFTACF
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Role-based naming for types and conversion functions

Role-based naming distinguishes model types by their purpose and gives functions names that identify their role as parsers, mappers, or type guards. The source uses `User`, `UserForm`, and `UserResponse` for model roles, with separate conventions for value unions and runtime schemas. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:67-74]

## Type names

Use `User`, `UserForm`, and `UserResponse` to distinguish model roles, `UserStatus` for a union of values, and `UserSchema` for a runtime schema. These names make each declaration’s intended role explicit. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:69-71]

## Function names

Use `parseUserResponse` for a parser, `toCreateUserRequest` for a mapper, and `isUser` for a type guard. These conventions distinguish parsing, conversion, and checking in function names. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:72-74]

The distinction between parsing and asserting a type matters: `response as User` does not change or validate data. External input requires a parser, runtime schema, or actual type guard; see [[Runtime validation versus type assertions]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-33]

## Keep contracts consistent

Distinct role names should be paired with a [[Single source of truth for type contracts]]. If the same shape exists independently as a schema, response interface, and UI type, those definitions can drift. Establish one authoritative contract and derive or map the other types from it. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:59-61]

## Sources

- [Patterns and Pitfalls](how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md)
