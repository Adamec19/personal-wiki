---
title: Runtime-Aligned TypeScript Configuration
summary: Choose target, module, and moduleResolution to match the runtime and bundler instead of copying compiler settings without understanding their effects.
sources:
  - how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md
kind: concept
createdAt: "2026-11-11T11:05:08.934Z"
updatedAt: "2026-11-11T11:05:08.934Z"
tags:
  - typescript
  - configuration
  - runtime
aliases:
  - runtime-aligned-typescript-configuration
  - RTC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Runtime-Aligned TypeScript Configuration

Runtime-aligned TypeScript configuration matches compiler settings to the project’s runtime and bundler. In particular, `target`, `module`, and `moduleResolution` must reflect the actual environment; a configuration should not be copied without understanding those choices. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:19-34]

## Compiler settings

The source provides the following practical starting point. Its environment-dependent settings must be checked against the project’s runtime and bundler. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:17-34]

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "Bundler",
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitOverride": true,
    "noEmit": true,
    "skipLibCheck": true
  }
}
```

[[TypeScript Strict Mode and Null Safety|Strict mode]] enables checks that catch problems earlier. A key effect is `strictNullChecks`, which prevents `null` and `undefined` from being automatically compatible with every type. [[Checked Indexed Access|noUncheckedIndexedAccess]] additionally makes indexed array access account for a potentially missing element through `T | undefined`. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:5-15, how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:36-42]

## Path aliases and project boundaries

[[Path Alias Coordination Across Tools|Path aliases]] require coordinated configuration in the bundler, test runner, and editor tooling. Defining an alias in `tsconfig` alone does not change runtime resolution. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:50-52]

[[TypeScript File Inclusion and Exclusion|File inclusion and exclusion]] define which source files belong to the project, but `exclude` is not a security boundary: an imported file can still enter the program. [[TypeScript Project References|Project references]] are appropriate when several TypeScript projects are built independently; a single well-configured `tsconfig` is simpler for an ordinary application. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:44-48]

## Verification and configuration discipline

Run the compiler’s type check with the following command and include it in CI. Linting and formatting address different concerns and do not replace compiler checks. See [[Type Checking in Continuous Integration]]. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:54-60]

```sh
tsc --noEmit
```

Avoid disabling strict checking to suppress errors, treating `skipLibCheck` as a fix for errors in your own types, configuring aliases without bundler and test support, or adding compiler options without verifying their effects. ^[how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md:62-67]

## Sources

- [tsconfig and Project Setup](how-to/typescript-cheat-sheet/07-tsconfig-and-project-setup.md)
