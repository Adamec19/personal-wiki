---
title: Appropriate use of const assertions
summary: Use as const for literal narrowing and readonly typing in constant configurations, maps, and value lists rather than as an automatic mutability fix.
sources:
  - how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md
kind: concept
createdAt: "2026-11-11T11:05:25.656Z"
updatedAt: "2026-11-11T11:05:25.656Z"
tags:
  - typescript
  - literal-types
  - readonly
aliases:
  - appropriate-use-of-const-assertions
  - AUOCA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Appropriate use of [[const-assertions|Const Assertions]]

Const assertion `as const` makes a value readonly and narrows its literals. Use it deliberately for constant configurations, maps, and lists of values, rather than adding it everywhere. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:47-49]

## Choosing the right construct

Use [[Const Assertions|`as const`]] when readonly values and narrowed literals are appropriate. Do not use it as an automatic fix for a mutability error. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:47-49]

When the goal is to check compatibility with a type while preserving inference, use [[The satisfies operator|`satisfies`]]. A type assertion such as `as Config` tells the compiler to trust the assertion and can hide an error. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:35-45]

## Runtime validation is separate

Type assertions do not validate external data: `response as User` neither changes nor verifies the value. External input requires a parser, schema, or actual type guard; see [[Runtime validation versus type assertions]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-33]

## Sources

- [Patterns and Pitfalls](how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md)
