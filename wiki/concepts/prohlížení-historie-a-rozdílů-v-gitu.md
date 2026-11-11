---
title: Prohlížení historie a rozdílů v Gitu
summary: Kontrola historie commitů, obsahu konkrétního commitu, pracovních změn, stage a commitů vůči origin/main.
sources:
  - how-to/git-flow/README.md
kind: concept
createdAt: "2026-11-11T10:56:58.051Z"
updatedAt: "2026-11-11T10:56:58.051Z"
tags:
  - git
  - history
  - diff
aliases:
  - prohlížení-historie-a-rozdílů-v-gitu
  - PHARVG
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Prohlížení historie a rozdílů v Gitu

Git umožňuje prohlížet historii commitů, změny konkrétního commitu i rozdíly před vytvořením commitu. Samostatně lze zobrazit změny připravené ve stage a porovnat lokální větev se vzdálenou. ^[how-to/git-flow/README.md:92-99, how-to/git-flow/README.md:141-147]

## Historie commitů

Příkaz `git log --oneline` zobrazí stručnou historii commitů. Pro zobrazení změn konkrétního commitu použijte `git show` s jeho hashem. ^[how-to/git-flow/README.md:94-99]

```bash
git log --oneline
git show abc1234
```

## Rozdíly před commitem

Příkaz `git diff` zobrazí změny před commitem, zatímco `git diff --staged` ukáže změny připravené ve stage. Tyto příkazy pomáhají při kontrole změn v rámci [[Příprava a úprava commitů v Gitu|přípravy commitu]]. ^[how-to/git-flow/README.md:94-99]

```bash
git diff
git diff --staged
```

## Porovnání s remote větví

Před pushnutím lze příkazem `git log --oneline origin/main..HEAD` zobrazit commity vůči `origin/main`, které obsahuje aktuální historie `HEAD` navíc. Zdroj tento příkaz uvádí jako kontrolu commitů od posledního pushu. ^[how-to/git-flow/README.md:116-121]

```bash
git log --oneline origin/main..HEAD
```

Příkaz `git fetch` stáhne změny z remote bez sloučení. Následné `git diff main origin/main` zobrazí rozdíly mezi lokální větví `main` a vzdálenou větví `origin/main`. Tento postup souvisí se [[Synchronizace se vzdáleným repozitářem|synchronizací se vzdáleným repozitářem]]. ^[how-to/git-flow/README.md:141-147]

```bash
git fetch
git diff main origin/main
```

## Sources

- [Git Flow — praktický cheat sheet](how-to/git-flow/README.md)
