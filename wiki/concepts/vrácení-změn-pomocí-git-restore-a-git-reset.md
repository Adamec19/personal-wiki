---
title: Vrácení změn pomocí git restore a git reset
summary: Obnovení souborů, odebrání změn ze stage a odstranění posledního commitu se zachováním nebo zahozením změn.
sources:
  - how-to/git-flow/README.md
kind: concept
createdAt: "2026-11-11T10:56:43.152Z"
updatedAt: "2026-11-11T10:56:43.152Z"
tags:
  - git
  - restore
  - reset
aliases:
  - vrácení-změn-pomocí-git-restore-a-git-reset
  - VZPGRAGR
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Vrácení změn pomocí git restore a git reset

Při vracení změn záleží na tom, zda jde o necommitované úpravy, soubor přidaný do stage, nebo již vytvořený commit. Zdroj pro tyto situace uvádí příkazy `git restore`, `git restore --staged` a `git reset` s volbami `--soft` či `--hard`. ^[how-to/git-flow/README.md:28-53]

## Vrácení necommitovaných změn

Příkaz `git restore` vrátí necommitované změny v konkrétním souboru. Varianta s `.` slouží k zahození všech necommitovaných změn. ^[how-to/git-flow/README.md:30-38]

```bash
git restore src/components/Button.tsx
git restore .
```

## Odebrání souboru ze stage

Pokud byl soubor omylem přidán pomocí `git add`, lze jej odebrat ze stage příkazem `git restore --staged`. Tato operace řeší výběr změn pro commit v rámci [[Příprava a úprava commitů v Gitu|přípravy commitu]]. ^[how-to/git-flow/README.md:40-43]

```bash
git restore --staged src/components/Button.tsx
```

## Vrácení posledního commitu

Příkaz `git reset --soft HEAD~1` vrátí poslední commit a zachová změny v souborech. Hodí se tedy v situaci, kdy má zůstat kód zachován. ^[how-to/git-flow/README.md:45-48, how-to/git-flow/README.md:123-126]

```bash
git reset --soft HEAD~1
```

Příkaz `git reset --hard HEAD~1` zahodí poslední commit i jeho změny. Jde o destruktivní variantu, u níž zdroj výslovně upozorňuje na ztrátu kódu. ^[how-to/git-flow/README.md:50-54, how-to/git-flow/README.md:128-132]

```bash
git reset --hard HEAD~1
```

## Kontrola historie a změn

Před rozhodnutím lze pomocí `git diff` zobrazit změny před commitem a pomocí `git diff --staged` obsah stage. Příkaz `git log --oneline` poskytuje přehled historie commitů a slouží také ke kontrole po resetu. Podrobnosti shrnuje [[Prohlížení historie a rozdílů v Gitu]]. ^[how-to/git-flow/README.md:92-99, how-to/git-flow/README.md:134-137]

```bash
git diff
git diff --staged
git log --oneline
```

## Přepsání lokální větve podle remote

Při [[Synchronizace se vzdáleným repozitářem|synchronizaci se vzdáleným repozitářem]] zdroj uvádí také kombinaci `git fetch origin` a `git reset --hard origin/main`, která přepíše lokální větev podle vzdálené větve. Tento postup zahodí všechny lokální změny. ^[how-to/git-flow/README.md:149-154]

```bash
git fetch origin
git reset --hard origin/main
```

## Sources

- [Git Flow — praktický cheat sheet](how-to/git-flow/README.md)
