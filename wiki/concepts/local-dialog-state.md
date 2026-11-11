---
title: Local dialog state
summary: Component-local state suits dialogs whose triggers and content belong to a single component.
sources:
  - how-to/react-cheat-sheet/05-dialogs.md
kind: concept
createdAt: "2026-11-11T10:58:53.403Z"
updatedAt: "2026-11-11T10:58:53.403Z"
tags:
  - dialogs
  - component-design
aliases:
  - local-dialog-state
  - LDS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Local dialog state

Lokální stav dialogu je vhodný, když dialog patří jedné komponentě a není potřeba jej otevírat z více vzdálených míst. Otevření a zavření řídí React state, který je jediným zdrojem pravdy. Dialog nemá současně používat `open` prop, vlastní nesynchronizovaný stav a globální store. ^[how-to/react-cheat-sheet/05-dialogs.md:23-29]

## Základní použití

Komponenta drží boolean `isOpen`. Trigger jej nastaví na `true` a dialog dostává aktuální hodnotu přes `open`. Callback `onOpenChange` aktualizuje tentýž stav při změně otevření dialogu. Tento přístup odpovídá principu [[Controlled Components and State Ownership]]. ^[how-to/react-cheat-sheet/05-dialogs.md:31-42]

```tsx
const [isOpen, setIsOpen] = useState(false);

return (
  <>
    <button onClick={() => setIsOpen(true)}>Detail</button>
    <Dialog open={isOpen} onOpenChange={setIsOpen}>
      <DialogContent>Obsah dialogu</DialogContent>
    </Dialog>
  </>
);
```

## Kdy zvolit lokální stav

Lokální dialog je čitelnější, pokud jej používá jediná komponenta, obsah závisí na jejím lokálním stavu, otevření není potřeba spouštět ze vzdálených míst a není nutné řídit více dialogů jako stack. Kratší zápis globální služby sám o sobě není důvodem k jejímu použití. ^[how-to/react-cheat-sheet/05-dialogs.md:156-163]

[[Global dialog service architecture|Globální dialogová služba]] se hodí pro opakované informační nebo potvrzovací dialogy a situace, kdy trigger a vykreslení dialogu nejsou blízko sebe. ^[how-to/react-cheat-sheet/05-dialogs.md:44-52]

## Stav a chování dialogu

Boolean řídí otevření, ale dialog potřebuje také správu focusu, vykreslení, zavírání a přístupnost. Při skládání callbacků je nutné propojit `onOpenChange` s interním close handlerem, aby nebyl tiše přepsán; související téma je [[Dialog close-handler composition]]. ^[how-to/react-cheat-sheet/05-dialogs.md:3-3, how-to/react-cheat-sheet/05-dialogs.md:114-116]

[[Accessible dialog behavior|Přístupný dialog]] má roli `dialog`, `aria-modal="true"` a přístupný název. Po otevření přesune focus na smysluplný prvek, podporuje zavření klávesou Escape, pokud není záměrně zakázané, a po zavření vrací focus na trigger. ^[how-to/react-cheat-sheet/05-dialogs.md:146-153]

## Sources

- [Dialogs](how-to/react-cheat-sheet/05-dialogs.md)
