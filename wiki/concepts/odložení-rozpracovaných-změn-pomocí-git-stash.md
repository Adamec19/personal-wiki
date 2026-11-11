---
title: Odložení rozpracovaných změn pomocí git stash
summary: Dočasné odložení změn, zobrazení uložených položek a jejich obnovení pomocí git stash pop.
sources:
  - how-to/git-flow/README.md
kind: concept
createdAt: "2026-11-11T10:56:53.785Z"
updatedAt: "2026-11-11T10:56:53.785Z"
tags:
  - git
  - stash
aliases:
  - odložení-rozpracovaných-změn-pomocí-git-stash
  - ORZPGS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Odložení rozpracovaných změn pomocí git stash

`git stash` slouží k dočasnému odložení aktuálních rozpracovaných změn stranou. Odložené změny lze následně vrátit pomocí `git stash pop` a jejich přehled zobrazit příkazem `git stash list`. ^[how-to/git-flow/README.md:82-88]

## Základní použití

Aktuální změny odložíš následujícím příkazem. ^[how-to/git-flow/README.md:84-85]

```bash
git stash
```

Přehled změn uložených ve stashi zobrazíš příkazem `git stash list`. ^[how-to/git-flow/README.md:87-88]

```bash
git stash list
```

Odložené změny vrátíš zpět pomocí `git stash pop`. ^[how-to/git-flow/README.md:86-88]

```bash
git stash pop
```

## Související koncepty

Odkládání rozpracovaných změn patří mezi postupy pro [[Každodenní práce s Gitem|každodenní práci s Gitem]]. Další související oblastí je [[Správa větví v Gitu|správa větví]]. ^[how-to/git-flow/README.md:3-24, how-to/git-flow/README.md:82-88]

## Sources

- [Git Flow — praktický cheat sheet](how-to/git-flow/README.md)
