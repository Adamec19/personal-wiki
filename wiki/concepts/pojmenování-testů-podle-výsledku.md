---
title: Pojmenování testů podle výsledku
summary: Název testu má popisovat pozorovatelný výsledek, nikoli privátní funkci.
sources:
  - how-to/react-cheat-sheet/08-testing-and-review.md
kind: concept
createdAt: "2026-11-11T10:59:48.275Z"
updatedAt: "2026-11-11T10:59:48.275Z"
tags:
  - testování
  - čitelnost
aliases:
  - pojmenování-testů-podle-výsledku
  - PTPV
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Pojmenování testů podle výsledku

Název testu má popisovat pozorovatelný výsledek, nikoli privátní funkci nebo interní implementaci. Vychází tak z principu [[Testování kontraktu a pozorovatelného chování]]: test ověřuje, co uživatel vidí, jaká data obdrží callback nebo jak se aplikace zachová při neplatném vstupu. ^[how-to/react-cheat-sheet/08-testing-and-review.md:5-11, how-to/react-cheat-sheet/08-testing-and-review.md:23-23]

## Příklad názvu

Název `disables itself while saving` vyjadřuje očekávané chování tlačítka během ukládání. Blok `describe("SaveButton")` určuje testovanou komponentu a název testu popisuje konkrétní výsledek. ^[how-to/react-cheat-sheet/08-testing-and-review.md:13-23]

```tsx
describe("SaveButton", () => {
  it("disables itself while saving", () => {
    // arrange, act, assert
  });
});
```

## Soulad názvu s ověřením

Název `calls onSave with the edited value` odpovídá testu, který upraví textové pole, klikne na tlačítko Save a ověří zavolání callbacku `onSave` s hodnotou `"new"`. Pojmenování tak přímo vystihuje ověřovaný kontrakt; souvisejícím tématem je [[Testování uživatelských interakcí a callbacků]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:39-49]

Při review je vhodné zkontrolovat, zda test pokrývá nový kontrakt chování. Název podle výsledku tento kontrakt výslovně pojmenovává. ^[how-to/react-cheat-sheet/08-testing-and-review.md:23-23, how-to/react-cheat-sheet/08-testing-and-review.md:34-34]

## Sources

- [Testing and Review](how-to/react-cheat-sheet/08-testing-and-review.md)
