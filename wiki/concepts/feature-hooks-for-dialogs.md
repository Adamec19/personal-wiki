---
title: Feature hooks for dialogs
summary: Feature hooks encapsulate dialog content, translations, and callbacks to avoid repeated store calls across triggers.
sources:
  - how-to/react-cheat-sheet/05-dialogs.md
kind: concept
createdAt: "2026-11-11T10:59:05.572Z"
updatedAt: "2026-11-11T10:59:05.572Z"
tags:
  - react-hooks
  - internationalization
  - encapsulation
aliases:
  - feature-hooks-for-dialogs
  - FHFD
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Feature hooks for dialogs

Feature hook pro dialogy zapouzdřuje přípravu obsahu a callbacků pro konkrétní oblast aplikace. Trigger pak zná pouze pojmenovanou akci, například `showHelp()`, zatímco hook sestaví parametry pro otevření dialogu. Toto rozdělení navazuje na [[Global dialog service architecture]]. ^[how-to/react-cheat-sheet/05-dialogs.md:44-63]

## Zapouzdření obsahu a překladů

Místo opakovaného volání globálního storu na mnoha místech poskytuje feature hook konkrétní akce, například otevření nápovědy k platbě. Uvnitř schovává názvy překladových klíčů a tvar obsahu předávaného do `openDialog`. Překlady zůstávají v i18n vrstvě, nikoli v globálním storu. ^[how-to/react-cheat-sheet/05-dialogs.md:91-110, how-to/react-cheat-sheet/05-dialogs.md:119-119]

```tsx
const useHelpDialogs = () => {
  const { openDialog } = useDialogStore();
  const t = useTranslations("help");

  return {
    payment: () =>
      openDialog("info", {
        title: t("payment.title"),
        content: t("payment.content")
      })
  };
};

export { useHelpDialogs };
```

Hook v příkladu nabízí akci `payment()`, která otevře informační dialog s přeloženým titulkem a obsahem. Používá přitom globální store prostřednictvím `useDialogStore()`. ^[how-to/react-cheat-sheet/05-dialogs.md:95-110]

## Zapojení do aplikace

Feature hook připravuje parametry dialogu; store eviduje otevřené dialogy a jejich identifikátory, globální renderer vybírá konkrétní komponentu a dialog primitive řeší overlay, focus trap, Escape a další chování. [[Type-safe dialog stores]] umožňují navázat typ předávaných props na zvolený typ dialogu. ^[how-to/react-cheat-sheet/05-dialogs.md:54-81]

Provider musí obalovat všechny triggery i globální renderer. Při zavření musí renderer odstranit dialog podle jeho konkrétního `id` a případný vlastní `onOpenChange` musí spolupracovat s interním close handlerem. Podrobnosti rozvádějí [[Dialog state ownership and lifecycle]] a [[Dialog close-handler composition]]. ^[how-to/react-cheat-sheet/05-dialogs.md:112-117]

## Kdy zvolit lokální dialog

Globální service se hodí pro opakované informační či potvrzovací dialogy nebo pro vzdálené triggery. Pokud dialog používá jediná komponenta, jeho obsah závisí na lokálním stavu a není potřeba řídit stack dialogů, bývá čitelnější [[Local dialog state]]. ^[how-to/react-cheat-sheet/05-dialogs.md:44-46, how-to/react-cheat-sheet/05-dialogs.md:156-163]

## Sources

- [Dialogs](how-to/react-cheat-sheet/05-dialogs.md)
