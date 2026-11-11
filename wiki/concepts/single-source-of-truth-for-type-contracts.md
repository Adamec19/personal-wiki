---
title: Single source of truth for type contracts
summary: Prevent schemas, response interfaces, and UI types from drifting by establishing one authoritative contract and deriving or mapping other representations.
sources:
  - how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md
kind: concept
createdAt: "2026-11-11T11:05:38.661Z"
updatedAt: "2026-11-11T11:05:38.661Z"
tags:
  - typescript
  - data-contracts
  - maintainability
aliases:
  - single-source-of-truth-for-type-contracts
  - SSOTFTC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Single source of truth for type contracts

Jediný zdroj pravdy pro typové kontrakty omezuje duplicitu stejného datového tvaru. Pokud je tentýž kontrakt samostatně definován jako schema, response interface a UI typ, mohou se jeho definice časem rozejít. Urči jednu autoritativní definici a ostatní typy z ní odvozuj nebo mezi modely explicitně mapuj. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:59-61]

## Odvozování a mapování modelů

Rozlišuj role modelů pomocí názvů, například `User`, `UserForm` a `UserResponse`. Runtime schema pojmenuj `UserSchema`, parser `parseUserResponse` a mapper `toCreateUserRequest`. Tato pojmenování podporují přehledné [[Oddělení modelů v datovém toku|oddělení modelů v datovém toku]] při odvozování a mapování kontraktů. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:59-74]

Odvozování typů má zůstat čitelné. Conditional nebo mapped typy nepřidávej pouze proto, že je to možné; pokud složitá generic signature nepřináší skutečnou bezpečnost, zjednoduš ji. Viz [[Avoiding type-level overengineering]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:63-65]

## Vztah k runtime validaci

Jednotný typový kontrakt nenahrazuje ověření externích dat. Type assertion jako `response as User` data nezmění ani neověří; pro externí vstup použij parser, schema nebo skutečný type guard. Viz [[Runtime validation versus type assertions]]. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:27-33]

Při kontrole návrhu ověřuj, zda se stejný kontrakt nezdvojuje na více místech a zda jsou externí vstupy runtime validované. ^[how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md:76-83]

## Sources

- [Patterns and Pitfalls](how-to/typescript-cheat-sheet/08-patterns-and-pitfalls.md)
