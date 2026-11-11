---
title: Type Checking in Continuous Integration
summary: Run tsc --noEmit in CI to verify types, alongside linting and formatting, which address different concerns and do not replace compiler checks.
sources:
  - how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md
kind: concept
createdAt: "2026-11-11T11:05:15.610Z"
updatedAt: "2026-11-11T11:05:15.610Z"
tags:
  - typescript
  - continuous-integration
  - verification
aliases:
  - type-checking-in-continuous-integration
  - TCICI
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Type Checking in Continuous Integration

Type checking should run in continuous integration (CI) to verify the project with the TypeScript compiler. Linting and formatting address a different layer; neither replaces compiler checks. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:54-60]

## Verification command

Run the following command to check types without emitting output files. The source also includes `noEmit: true` in its example project configuration. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:19-32, how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:54-60]

```sh
tsc --noEmit
```

## Configuration behind the check

Use `strict: true` as the starting point for [[TypeScript Project Configuration]]. It enables checks that catch problems early, including `strictNullChecks`, which prevents `null` and `undefined` from being automatically compatible with every type. See [[TypeScript Strict Mode and Null Safety]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:3-15]

Enable `noUncheckedIndexedAccess` to make indexed access account for potentially missing elements. For example, reading from a `string[]` can produce `string | undefined`, requiring the empty-array case to be handled. See [[Checked Indexed Access]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:36-42]

The compiler configuration must match the project's runtime and bundler: choose `target`, `module`, and `moduleResolution` with that environment in mind. See [[Runtime-Aligned TypeScript Configuration]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:19-34]

## Sources

- [tsconfig and Project Setup](how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md)
