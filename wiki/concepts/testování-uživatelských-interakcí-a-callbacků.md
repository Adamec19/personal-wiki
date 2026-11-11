---
title: Testování uživatelských interakcí a callbacků
summary: Test může vykonat úpravu vstupu a uložení a následně ověřit, že callback obdržel upravenou hodnotu.
sources:
  - how-to/react-cheat-sheet/08-testing-and-review.md
kind: concept
createdAt: "2026-11-11T10:59:59.067Z"
updatedAt: "2026-11-11T10:59:59.067Z"
tags:
  - testování
  - uživatelské-interakce
aliases:
  - testování-uživatelských-interakcí-a-callbacků
  - TUIAC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Testování uživatelských interakcí a callbacků

Testy uživatelských interakcí ověřují kontrakt a pozorovatelné chování komponenty: co uživatel vidí a jaká data komponenta předává callbackům. Nemají se zaměřovat na interní implementaci. Souvisejícím principem je [[Testování kontraktu a pozorovatelného chování]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:5-11]

## Co ověřovat

Testy mají kontrolovat správný zobrazený stav, data předaná callbacku, odmítnutí neplatného vstupu validací a přechody mezi loading, error a success stavy. U dialogů ověřují také otevření správného obsahu a správný způsob zavření. ^[how-to/react-cheat-sheet/08-testing-and-review.md:7-11]

## Příklad: úprava hodnoty a uložení

Následující test vykreslí editor s výchozí hodnotou, simuluje vymazání a zadání nového textu a poté kliknutí na tlačítko Save. Výsledkem, který ověřuje, je zavolání callbacku `onSave` s upravenou hodnotou `"new"`. ^[how-to/react-cheat-sheet/08-testing-and-review.md:40-49]

```tsx
it("calls onSave with the edited value", async () => {
  const onSave = vi.fn();
  render(<Editor initialValue="old" onSave={onSave} />);

  await userEvent.clear(screen.getByRole("textbox"));
  await userEvent.type(screen.getByRole("textbox"), "new");
  await userEvent.click(screen.getByRole("button", { name: "Save" }));

  expect(onSave).toHaveBeenCalledWith("new");
});
```

Ukázka je obecná; test runner a mock API je potřeba zvolit podle konkrétního projektu. ^[how-to/react-cheat-sheet/08-testing-and-review.md:52-52]

## Pojmenování a kontrola testu

Název testu má popisovat pozorovatelný výsledek, například předání upravené hodnoty callbacku nebo deaktivaci tlačítka během ukládání. Nemá vycházet z názvu privátní funkce. Viz [[Pojmenování testů podle výsledku]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:15-23, how-to/react-cheat-sheet/08-testing-and-review.md:40-48]

Při review změny je třeba zkontrolovat, zda test pokrývá nový kontrakt chování a zda změna neobsahuje nesouvisející refaktoring. S tím souvisí [[Kontrola rozsahu změny a testovacího pokrytí]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:34-35]

## Sources

- [Testing and Review](how-to/react-cheat-sheet/08-testing-and-review.md)
