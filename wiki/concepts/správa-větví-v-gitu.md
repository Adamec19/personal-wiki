---
title: Správa větví v Gitu
summary: Vytváření, přepínání, výpis a mazání lokálních i vzdálených větví.
sources:
  - how-to/git-flow/README.md
kind: concept
createdAt: "2026-11-11T10:56:42.387Z"
updatedAt: "2026-11-11T10:56:42.387Z"
tags:
  - git
  - branches
aliases:
  - správa-větví-v-gitu
  - SVVG
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Správa větví v Gitu

Správa větví zahrnuje vytváření nových větví, přepínání mezi nimi, jejich výpis a mazání lokálně i ve vzdáleném repozitáři. Změny z jedné větve lze sloučit do jiné pomocí `git merge`. ^[how-to/git-flow/README.md:16-24, how-to/git-flow/README.md:67-72]

## Vytvoření a přepínání větví

Příkaz `git checkout -b` vytvoří novou větev a zároveň na ni přepne. Pro přepnutí na existující větev se používá `git checkout` s jejím názvem. ^[how-to/git-flow/README.md:18-20]

```bash
git checkout -b nazev-vetve
git checkout main
```

## Výpis a mazání větví

Příkaz `git branch` zobrazí větve. Lokální větev lze smazat pomocí `git branch -d`; pro smazání větve na vzdáleném repozitáři `origin` slouží `git push origin --delete`. ^[how-to/git-flow/README.md:21-23]

```bash
git branch
git branch -d nazev-vetve
git push origin --delete nazev-vetve
```

## Sloučení větve

Příkaz `git merge` slučuje zadanou větev do aktuální větve. Pro začlenění změn do `main` je tedy nejprve potřeba přepnout na `main` a poté spustit merge. Pokud vzniknou konflikty, po jejich ručním vyřešení následuje přidání souborů do stage a commit. Podrobněji viz [[Slučování větví a řešení konfliktů]]. ^[how-to/git-flow/README.md:67-78]

```bash
git checkout main
git merge nazev-vetve
```

## Související postupy

Rozpracované změny lze dočasně odložit pomocí `git stash`, obnovit pomocí `git stash pop` a zobrazit pomocí `git stash list`. Tento postup popisuje [[Odložení rozpracovaných změn pomocí git stash]]. ^[how-to/git-flow/README.md:82-88]

Pokud commit vznikl na nesprávné větvi, lze zjistit jeho hash pomocí `git log --oneline`, přepnout na správnou větev a přenést jej příkazem `git cherry-pick`. Viz [[Přenesení commitu na správnou větev]]. ^[how-to/git-flow/README.md:56-60]

Pro porovnání lokální větve `main` s její vzdálenou podobou slouží `git diff main origin/main`. Příkaz `git fetch` stáhne změny bez sloučení, zatímco `git pull` změny stáhne a sloučí. Viz [[Synchronizace se vzdáleným repozitářem]]. ^[how-to/git-flow/README.md:141-147]

## Sources

- [Git Flow — praktický cheat sheet](how-to/git-flow/README.md)
