---
title: Oddělení business logiky od generického UI
summary: Review má hlídat, aby business logika nepronikala do generických UI komponent.
sources:
  - how-to/react-cheat-sheet/08-testing-and-review.md
kind: concept
createdAt: "2026-11-11T11:00:07.771Z"
updatedAt: "2026-11-11T11:00:07.771Z"
tags:
  - architektura
  - code-review
aliases:
  - oddělení-business-logiky-od-generického-ui
  - OBLOGU
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Oddělení business logiky od generického UI

Při review komponent se kontroluje, zda business logika neproniká do generické UI komponenty. Tato kontrola je součástí posouzení čitelnosti datového toku, záměrné správy stavu a správného předávání chyb. ^[how-to/react-cheat-sheet/08-testing-and-review.md:25-33]

## Kontrola hranic komponenty

Při posuzování oddělení odpovědností sleduj [[Kontrola datového toku a správy stavu|datový tok a správu stavu]]: zda je cesta od vstupu po výstup čitelná, zda state neobsahuje odvoditelné hodnoty a zda je komponenta záměrně controlled nebo uncontrolled. Review zahrnuje také ověření API response před použitím a zobrazení nebo předání chyby na správnou hranici. ^[how-to/react-cheat-sheet/08-testing-and-review.md:27-33]

## Ověření veřejného kontraktu

[[Testování kontraktu a pozorovatelného chování]] se zaměřuje na výsledek dostupný uživateli nebo volajícímu, nikoli na interní implementaci. Ověřuje správně zobrazený stav, data předaná callbacku, odmítnutí neplatného vstupu, přechody loading/error/success a správné otevření i zavření dialogu. ^[how-to/react-cheat-sheet/08-testing-and-review.md:3-11]

Příkladem je test editoru, který změní obsah textového pole a po kliknutí na „Save“ ověří, že callback `onSave` obdržel upravenou hodnotu. Test tak kontroluje pozorovatelný výsledek interakce; podle tohoto výsledku má být také pojmenován. ^[how-to/react-cheat-sheet/08-testing-and-review.md:23-23, how-to/react-cheat-sheet/08-testing-and-review.md:39-49]

Při review změny ověř také to, zda test pokrývá nový behavior contract a zda změna neobsahuje nesouvisející refactoring. Tyto otázky doplňují [[Kontrola rozsahu změny a testovacího pokrytí|kontrolu rozsahu změny a testovacího pokrytí]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:34-35]

## Sources

- [Testing and Review](how-to/react-cheat-sheet/08-testing-and-review.md)
