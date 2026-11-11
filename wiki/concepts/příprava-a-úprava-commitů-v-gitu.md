---
title: Příprava a úprava commitů v Gitu
summary: Přidávání změn do stage, vytváření commitů a oprava posledního commitu pomocí git commit --amend.
sources:
  - how-to/git-flow/README.md
kind: concept
createdAt: "2026-11-11T10:56:44.232Z"
updatedAt: "2026-11-11T10:56:44.232Z"
tags:
  - git
  - commits
  - staging
aliases:
  - příprava-a-úprava-commitů-v-gitu
  - PAÚCVG
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Příprava a úprava commitů v Gitu

Příprava commitu zahrnuje kontrolu změn, jejich přidání do stage a vytvoření commitu se zprávou. Poslední commit lze následně upravit pomocí `--amend` nebo vrátit pomocí `reset`. ^[how-to/git-flow/README.md:5-12, how-to/git-flow/README.md:40-53, how-to/git-flow/README.md:103-112]

## Kontrola a příprava změn

Příkaz `git status` zobrazí stav repozitáře. Pro kontrolu rozdílů slouží `git diff`; změny připravené ve stage zobrazí `git diff --staged`. Další přehled nabízí [[Prohlížení historie a rozdílů v Gitu]]. ^[how-to/git-flow/README.md:5-6, how-to/git-flow/README.md:92-99]

```bash
git status
git diff
git diff --staged
```

Do stage lze přidat všechny změny pomocí `git add .` nebo pouze konkrétní soubor. Připravené změny se uloží příkazem `git commit -m "popis změny"`. ^[how-to/git-flow/README.md:7-9]

```bash
git add src/components/Button.tsx
git commit -m "popis změny"
```

Pokud byl soubor přidán do stage omylem, lze jej odtud odebrat pomocí `git restore --staged`. ^[how-to/git-flow/README.md:40-43]

```bash
git restore --staged src/components/Button.tsx
```

## Úprava posledního commitu

Zprávu posledního, ještě nepushnutého commitu lze změnit pomocí `git commit --amend -m`. ^[how-to/git-flow/README.md:103-107]

```bash
git commit --amend -m "opravená zpráva"
```

Zapomenutý soubor lze přidat do posledního commitu tak, že se nejprve přidá do stage a poté se použije `git commit --amend --no-edit`. Tím se zachová původní zpráva commitu. ^[how-to/git-flow/README.md:109-111]

```bash
git add zapomenutý-soubor.txt
git commit --amend --no-edit
```

## Vrácení posledního commitu

Příkaz `git reset --soft HEAD~1` vrátí poslední commit a zachová změny v souborech. Varianta `git reset --hard HEAD~1` zahodí poslední commit i jeho změny, proto vyžaduje opatrnost. ^[how-to/git-flow/README.md:45-54]

```bash
git reset --soft HEAD~1
```

Pokud byl commit vytvořen na nesprávné větvi, postup jeho přesunu popisuje [[Přenesení commitu na správnou větev]]. Používá vyhledání hashe, `git cherry-pick` na cílové větvi a odstranění commitu z původní větve. ^[how-to/git-flow/README.md:56-63]

## Kontrola před odesláním

Před pushnutím lze zobrazit commity v rozsahu `origin/main..HEAD`. Po případných úpravách slouží `git log --oneline` k opětovné kontrole historie; samotné odeslání provede `git push`. ^[how-to/git-flow/README.md:10-10, how-to/git-flow/README.md:116-137]

```bash
git log --oneline origin/main..HEAD
git log --oneline
git push
```

## Sources

- [Git Flow — praktický cheat sheet](how-to/git-flow/README.md)
