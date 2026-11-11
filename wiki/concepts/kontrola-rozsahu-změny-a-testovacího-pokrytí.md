---
title: Kontrola rozsahu změny a testovacího pokrytí
summary: Review má ověřit pokrytí nového behaviorálního kontraktu testem a nepřítomnost nesouvisejícího refactoringu.
sources:
  - how-to/react-cheat-sheet/08-testing-and-review.md
kind: concept
createdAt: "2026-11-11T11:00:12.366Z"
updatedAt: "2026-11-11T11:00:12.366Z"
tags:
  - code-review
  - rozsah-změn
  - testování
aliases:
  - kontrola-rozsahu-změny-a-testovacího-pokrytí
  - KRZATP
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Kontrola rozsahu změny a testovacího pokrytí

Při review ověřuj, zda testy pokrývají nový kontrakt chování a zda změna neobsahuje nesouvisející refaktoring. Tyto dvě kontroly se soustředí na rozsah úpravy a ověření jejího výsledku. ^[how-to/react-cheat-sheet/08-testing-and-review.md:34-35]

## Co mají testy pokrývat

Testuj kontrakt a pozorovatelné chování, nikoli interní implementaci. Ověřuj správný stav zobrazený uživateli, data předaná callbackům, odmítnutí neplatného vstupu, přepínání loading/error/success stavů a správné otevírání i zavírání dialogu. Podrobněji viz [[Testování kontraktu a pozorovatelného chování]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:5-11]

Test pojmenuj podle pozorovatelného výsledku, nikoli podle privátní funkce. Název tak vyjadřuje ověřované chování, například že se tlačítko během ukládání deaktivuje; viz [[Pojmenování testů podle výsledku]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:13-23]

## Příklad ověření změněného chování

Ukázkový test editoru změní obsah textového pole z `"old"` na `"new"`, klikne na tlačítko Save a ověří, že callback `onSave` obdržel `"new"`. Pokrývá tím uživatelskou interakci a její výsledek předaný přes veřejný kontrakt komponenty; viz [[Testování uživatelských interakcí a callbacků]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:40-49]

Použitý test runner a mock API mají odpovídat konkrétnímu projektu; uvedený vzor je záměrně obecný. ^[how-to/react-cheat-sheet/08-testing-and-review.md:52-52]

## Sources

- [Testing and Review](how-to/react-cheat-sheet/08-testing-and-review.md)
