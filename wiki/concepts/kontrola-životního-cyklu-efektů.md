---
title: Kontrola životního cyklu efektů
summary: Review má kontrolovat cleanup efektů a správnost jejich dependencies.
sources:
  - how-to/react-cheat-sheet/08-testing-and-review.md
kind: concept
createdAt: "2026-11-11T10:59:57.725Z"
updatedAt: "2026-11-11T10:59:57.725Z"
tags:
  - code-review
  - efekty
aliases:
  - kontrola-životního-cyklu-efektů
  - KŽCE
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Kontrola životního cyklu efektů

Kontrola životního cyklu efektů je součástí review React kódu. U každého efektu ověřuje, zda má cleanup a správné dependencies. ^[how-to/react-cheat-sheet/08-testing-and-review.md:25-29]

## Co při review ověřit

Cleanup a dependencies tvoří dva výslovné kontrolní body pro každý efekt. Souvisejí s tématy [[Cleanup efektů]] a [[Synchronizace s externími systémy pomocí useEffect]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:29-29]

Kontrolu efektů doplňuje posouzení čitelnosti datového toku a toho, zda state neobsahuje hodnotu, kterou lze odvodit. Navazující témata jsou [[Kontrola datového toku a správy stavu]] a [[Odvozené hodnoty a jediný zdroj pravdy]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:27-29]

## Ověření chování testy

Testy mají ověřovat kontrakt a pozorovatelné chování, nikoli interní implementaci. Patří sem správně zobrazený stav, data předaná callbacku nebo přepínání loading/error/success stavů. Při review se zároveň kontroluje, zda test pokrývá nový behavior contract; podrobněji viz [[Testování kontraktu a pozorovatelného chování]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:5-11, how-to/react-cheat-sheet/08-testing-and-review.md:34-34]

## Sources

- [Testing and Review](how-to/react-cheat-sheet/08-testing-and-review.md)
