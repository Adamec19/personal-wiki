---
title: Kontrola datového toku a správy stavu
summary: Review má ověřovat čitelnost datového toku, absenci zbytečně uloženého odvozeného stavu a záměrnou volbu controlled či uncontrolled komponenty.
sources:
  - how-to/react-cheat-sheet/08-testing-and-review.md
kind: concept
createdAt: "2026-11-11T10:59:59.068Z"
updatedAt: "2026-11-11T10:59:59.068Z"
tags:
  - code-review
  - správa-stavu
aliases:
  - kontrola-datového-toku-a-správy-stavu
  - KDTASS
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Kontrola datového toku a správy stavu

Kontrola datového toku a správy stavu při review ověřuje, zda je tok dat čitelný od vstupu po výstup, zda state neobsahuje hodnoty, které lze odvodit, a zda je komponenta záměrně controlled nebo uncontrolled. ^[how-to/react-cheat-sheet/08-testing-and-review.md:25-30]

## Co při review ověřit

Čitelnost datového toku posuzuj od vstupu po výstup. Součástí kontroly je ověření API response před použitím, oddělení business logiky od generické UI komponenty a zobrazení nebo předání chyby na správnou hranici. Souvisejí s tím [[Oddělení business logiky od generického UI]] a [[Hranice a datový tok v React aplikaci]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:27-33]

U správy stavu zkontroluj, zda uloženou hodnotu nelze odvodit a zda je volba controlled nebo uncontrolled komponenty záměrná. Tato témata rozvíjejí [[Odvozené hodnoty a jediný zdroj pravdy]] a [[Controlled Components and State Ownership]]. U každého effectu ověř cleanup a správné dependencies; viz [[Kontrola životního cyklu efektů]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:28-30]

## Ověření chování testy

Testy mají ověřovat kontrakt a pozorovatelné chování: správný stav zobrazený uživateli, data předaná callbackům, odmítnutí neplatného vstupu a přepínání loading/error/success stavů. U dialogu ověřují také správný obsah a způsob zavření. Podrobněji viz [[Testování kontraktu a pozorovatelného chování]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:3-11]

Příkladem ověření datového toku je test editoru, který změní hodnotu z `"old"` na `"new"`, klikne na tlačítko Save a zkontroluje, že callback `onSave` obdržel `"new"`. Název testu má popisovat pozorovatelný výsledek. ^[how-to/react-cheat-sheet/08-testing-and-review.md:23-23, how-to/react-cheat-sheet/08-testing-and-review.md:37-49]

## Sources

- [Testing and Review](how-to/react-cheat-sheet/08-testing-and-review.md)
