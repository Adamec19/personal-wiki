---
title: Testování kontraktu a pozorovatelného chování
summary: Testy mají ověřovat uživatelské stavy, data callbacků, validaci a chování dialogů místo interní implementace.
sources:
  - how-to/react-cheat-sheet/08-testing-and-review.md
kind: concept
createdAt: "2026-11-11T10:59:51.708Z"
updatedAt: "2026-11-11T10:59:51.708Z"
tags:
  - testování
  - kontrakty
aliases:
  - testování-kontraktu-a-pozorovatelného-chování
  - TKAPC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Testování kontraktu a pozorovatelného chování

Testování kontraktu a pozorovatelného chování ověřuje, co komponenta poskytuje uživateli a jaká data předává prostřednictvím callbacků. Testy se zaměřují na výsledky chování, nikoli na interní implementaci. ^[how-to/react-cheat-sheet/08-testing-and-review.md:5-11]

## Co ověřovat

Testy mají pokrývat správně zobrazený stav, data předaná callbackům a odmítnutí neplatného vstupu validací. Součástí kontraktu jsou také přechody mezi loading, error a success stavy nebo otevření správného obsahu dialogu a jeho správné zavření. ^[how-to/react-cheat-sheet/08-testing-and-review.md:5-11]

## Pojmenování testů

Název testu má popisovat pozorovatelný výsledek, nikoli privátní funkci. Například `disables itself while saving` vyjadřuje očekávané chování tlačítka během ukládání. Podrobněji viz [[Pojmenování testů podle výsledku]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:13-23]

## Příklad testu interakce

Následující test upraví hodnotu textového pole, klikne na tlačítko Save a ověří, že callback `onSave` obdržel novou hodnotu. Propojuje tak uživatelskou interakci s kontrolou výstupního kontraktu komponenty; souvisejícím tématem je [[Testování uživatelských interakcí a callbacků]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:39-49]

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

Ukázka je obecná. Test runner a mock API je potřeba zvolit podle konkrétního projektu. ^[how-to/react-cheat-sheet/08-testing-and-review.md:52-52]

## Kontrola při review

Při review je třeba ověřit, zda test pokrývá nový kontrakt chování a zda změna neobsahuje nesouvisející refaktoring. Tyto otázky propojují testování s [[Kontrola rozsahu změny a testovacího pokrytí|kontrolou rozsahu změny a testovacího pokrytí]]. ^[how-to/react-cheat-sheet/08-testing-and-review.md:34-35]

## Sources

- [Testing and Review](how-to/react-cheat-sheet/08-testing-and-review.md)
