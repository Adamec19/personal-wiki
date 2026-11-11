---
title: Přenesení commitu na správnou větev
summary: Použití git cherry-pick k aplikování omylem umístěného commitu na správnou větev a následné odebrání z původní větve.
sources:
  - how-to/git-flow/README.md
kind: concept
createdAt: "2026-11-11T10:56:42.147Z"
updatedAt: "2026-11-11T10:56:42.147Z"
tags:
  - git
  - cherry-pick
  - branches
aliases:
  - přenesení-commitu-na-správnou-větev
  - PCNSV
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Přenesení commitu na správnou větev

Pokud byl commit vytvořen na nesprávné větvi, lze jej pomocí `git cherry-pick` přenést na správnou větev a poté odstranit z původní větve. ^[how-to/git-flow/README.md:56-63]

## Postup

Nejprve zjistěte hash commitu příkazem `git log --oneline`. Přepněte se na cílovou větev a použijte `git cherry-pick` s nalezeným hashem; `abc1234` v ukázce nahraďte skutečným hashem commitu. ^[how-to/git-flow/README.md:58-60]

```bash
git log --oneline
git checkout spravna-vetev
git cherry-pick abc1234
```

Poté se vraťte na původní větev. Pokud je chybně umístěný commit jejím posledním commitem, následující příkaz jej odstraní i s jeho změnami. `git reset --hard HEAD~1` je destruktivní krok, proto před jeho použitím ověřte stav repozitáře pomocí `git status` a historii pomocí `git log --oneline`. ^[how-to/git-flow/README.md:6-6, how-to/git-flow/README.md:50-62, how-to/git-flow/README.md:95-95]

```bash
git checkout spatna-vetev
git reset --hard HEAD~1
```

## Související koncepty

Pro orientaci ve větvích viz [[Správa větví v Gitu]]; pro zjištění hashe a kontrolu změn viz [[Prohlížení historie a rozdílů v Gitu]]. ^[how-to/git-flow/README.md:16-24, how-to/git-flow/README.md:92-99]

## Sources

- [Git Flow — praktický cheat sheet](how-to/git-flow/README.md)
