---
title: Slučování větví a řešení konfliktů
summary: Sloučení větve pomocí git merge a dokončení konfliktního sloučení po ruční opravě souborů.
sources:
  - how-to/git-flow/README.md
kind: concept
createdAt: "2026-11-11T10:56:54.902Z"
updatedAt: "2026-11-11T10:56:54.902Z"
tags:
  - git
  - merge
  - conflicts
aliases:
  - slučování-větví-a-řešení-konfliktů
  - SVAŘK
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Slučování větví a řešení konfliktů

Sloučení větve pomocí `git merge` přenese její změny do aktuální větve. Pro sloučení do `main` se nejprve přepněte na `main` a poté zadejte název slučované větve. Přepínání větví souvisí s tématem [[Správa větví v Gitu]]. ^[how-to/git-flow/README.md:67-72]

```bash
git checkout main
git merge nazev-vetve
```

## Řešení konfliktů

Pokud při slučování vznikne konflikt, ručně vyřešte konflikty v dotčených souborech. Poté změny přidejte do stage pomocí `git add .` a dokončete sloučení příkazem `git commit`. ^[how-to/git-flow/README.md:74-78]

```bash
git add .
git commit
```

## Slučování při synchronizaci s remote

Příkaz `git pull` stáhne změny ze vzdáleného repozitáře a provede sloučení. Naproti tomu `git fetch` změny pouze stáhne bez sloučení. Rozdíl mezi lokální a vzdálenou větví lze zobrazit příkazem `git diff main origin/main`; další související postupy popisuje [[Synchronizace se vzdáleným repozitářem]]. ^[how-to/git-flow/README.md:141-147]

```bash
git pull
git fetch
git diff main origin/main
```

## Sources

- [Git Flow — praktický cheat sheet](how-to/git-flow/README.md)
