---
title: Global dialog service architecture
summary: Triggers, feature services, a shared store, a provider, a renderer, and dialog primitives support dialogs opened from distant application locations.
sources:
  - how-to/react-cheat-sheet/05-dialogs.md
kind: concept
createdAt: "2026-11-11T10:59:05.712Z"
updatedAt: "2026-11-11T10:59:05.712Z"
tags:
  - dialogs
  - architecture
  - react
aliases:
  - global-dialog-service-architecture
  - GDSA
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Global dialog service architecture

Globální dialog service odděluje vyvolání dialogu od jeho vykreslení. Hodí se pro opakované informační a potvrzovací dialogy nebo situace, kdy trigger a dialog nejsou blízko sebe. Základní tok je: trigger → typované `openDialog(type, props)` → store → globální renderer → komponenta dialogu. ^[how-to/react-cheat-sheet/05-dialogs.md:44-52]

## Vrstvy architektury

Trigger zná pouze konkrétní akci, například `showHelp()`. Hook nebo service připraví titulek, obsah a callbacky. Store uchovává seznam otevřených dialogů a jejich identifikátory, provider jej zpřístupňuje React stromu a globální renderer mapuje `type` na konkrétní komponentu. Dialog primitive zajišťuje overlay, focus trap, Escape, kliknutí mimo obsah a animaci. Toto rozdělení umožňuje měnit vizuální implementaci bez úprav všech triggerů. ^[how-to/react-cheat-sheet/05-dialogs.md:54-63]

[[Feature hooks for dialogs]] zapouzdřují opakované volání dialogů, překladové klíče a podobu obsahu. Triggery pak používají pojmenované akce místo přímých volání globálního storu s opakovanými texty. Překlady patří do i18n vrstvy, nikoli do globálního storu. ^[how-to/react-cheat-sheet/05-dialogs.md:91-110, how-to/react-cheat-sheet/05-dialogs.md:119-119]

## Typovaný store

[[Type-safe dialog stores]] propojují typ dialogu s odpovídajícími props. Následující kontrakt rozlišuje informační a potvrzovací dialog, přiděluje každé otevřené instanci vlastní `id` a umožňuje její samostatné zavření. Renderer přitom nemusí znát jednotlivé triggery a dialog lze otevřít také z hooku nebo utility vrstvy. ^[how-to/react-cheat-sheet/05-dialogs.md:65-89]

```tsx
type DialogMap = {
  info: { title: string; content: React.ReactNode };
  confirm: { title: string; onConfirm: () => void };
};

type Dialog = {
  [K in keyof DialogMap]: {
    id: string;
    type: K;
    props: DialogMap[K];
  };
}[keyof DialogMap];

type DialogStore = {
  dialogs: Dialog[];
  openDialog: <T extends keyof DialogMap>(
    type: T,
    props: DialogMap[T]
  ) => string;
  closeDialog: (id: string) => void;
};
```

## Vlastnictví stavu a zavírání

React stav musí zůstat jediným zdrojem pravdy. Dialog nemá být současně řízený propem `open`, nesynchronizovaným lokálním stavem a globálním storem. V globální architektuře musí provider obalit všechny triggery i renderer a renderer musí při zavření odstranit dialog podle konkrétního `id`. Tyto odpovědnosti rozvíjí [[Dialog state ownership and lifecycle]]. ^[how-to/react-cheat-sheet/05-dialogs.md:23-23, how-to/react-cheat-sheet/05-dialogs.md:114-115]

Externí `onOpenChange` se musí kombinovat s interním close handlerem, aby jej tiše nepřepsal; souvisejícím tématem je [[Dialog close-handler composition]]. Potvrzovací dialog má po potvrzení nejprve zavřít dialog a poté podle potřeby provést navazující akci. ^[how-to/react-cheat-sheet/05-dialogs.md:116-117]

## Portály a přístupnost

Dialog se často vykresluje pomocí `createPortal(..., document.body)`, aby jej neořízlo rodičovské `overflow: hidden` nebo lokální stacking context. Portál mění umístění v DOM, ale zachovává React strom: context i propagace událostí vycházejí z místa vykreslení v React stromu. Globální renderer proto musí mít přístup k potřebnému provideru; další podrobnosti popisuje [[React portals and context propagation]]. ^[how-to/react-cheat-sheet/05-dialogs.md:123-125]

Samotný portál nezajišťuje focus trap ani ARIA. Dialog primitive nebo vlastní implementace musí dodat přístupné označení, smysluplný počáteční focus, obsluhu Escape, návrat focusu na trigger a jasné ovládání klávesnicí. Viz [[Accessible dialog behavior]]. ^[how-to/react-cheat-sheet/05-dialogs.md:144-154]

## Kdy zvolit lokální dialog

Globální service není vhodná pouze proto, že zkracuje zápis. [[Local dialog state]] je čitelnější, pokud dialog používá jediná komponenta, jeho obsah závisí na lokálním stavu, nemusí se otevírat ze vzdálených míst a není potřeba spravovat více dialogů jako stack. ^[how-to/react-cheat-sheet/05-dialogs.md:156-163]

## Sources

- [Dialogs](how-to/react-cheat-sheet/05-dialogs.md)
