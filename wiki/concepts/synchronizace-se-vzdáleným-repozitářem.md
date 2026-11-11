---
title: Synchronizace se vzdáleným repozitářem
summary: Odesílání a stahování změn pomocí push, pull a fetch, porovnání větví a nahrazení lokálního stavu vzdálenou větví.
sources:
  - how-to/git-flow/README.md
kind: concept
createdAt: "2026-11-11T10:56:59.388Z"
updatedAt: "2026-11-11T10:56:59.388Z"
tags:
  - git
  - remote
  - synchronization
aliases:
  - synchronizace-se-vzdáleným-repozitářem
  - SSVR
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Synchronizace se vzdáleným repozitářem

Synchronizace se vzdáleným repozitářem zahrnuje odesílání lokálních změn, stahování vzdálených změn a porovnávání lokální a vzdálené větve. Základními příkazy jsou `git push`, `git pull` a `git fetch`. ^[how-to/git-flow/README.md:5-12, how-to/git-flow/README.md:141-147]

## Odeslání a stažení změn

Příkaz `git push` odešle změny na vzdálený repozitář. Příkaz `git pull` stáhne vzdálené změny a provede jejich sloučení. Tyto operace patří mezi základní kroky [[Každodenní práce s Gitem]]. ^[how-to/git-flow/README.md:3-12, how-to/git-flow/README.md:143-145]

```bash
git push
git pull
```

Pokud chcete změny pouze stáhnout bez sloučení, použijte `git fetch`. Rozdíl mezi lokální větví `main` a vzdálenou větví `origin/main` zobrazí `git diff main origin/main`. ^[how-to/git-flow/README.md:143-147]

```bash
git fetch
git diff main origin/main
```

## Kontrola před odesláním

Commity v aktuální větvi oproti `origin/main` vypíše následující příkaz. Tento přehled slouží ke kontrole před odesláním změn a souvisí s [[Prohlížení historie a rozdílů v Gitu]]. ^[how-to/git-flow/README.md:116-121]

```bash
git log --oneline origin/main..HEAD
```

## Přepsání lokální větve vzdáleným stavem

Lokální větev lze přepsat podle stavu `origin/main` pomocí stažení aktuálního vzdáleného stavu a následného tvrdého resetu. **Tento postup zahodí lokální změny.** ^[how-to/git-flow/README.md:149-154]

```bash
git fetch origin
git reset --hard origin/main
```

## Sources

- [Git Flow — praktický cheat sheet](how-to/git-flow/README.md)
