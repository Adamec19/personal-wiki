---
title: Dialog close-handler composition
summary: Closing should remove the correct dialog ID, preserve internal handlers, and precede the confirmation action when appropriate.
sources:
  - how-to/react-cheat-sheet/05-dialogs.md
kind: concept
createdAt: "2026-11-11T10:59:08.188Z"
updatedAt: "2026-11-11T10:59:08.188Z"
tags:
  - dialogs
  - event-handling
  - lifecycle
aliases:
  - dialog-close-handler-composition
  - DCC
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Dialog close-handler composition

Dialog close-handler composition propojuje vlastní reakci na zavření s interní obsluhou životního cyklu dialogu. Při předání `onOpenChange` je potřeba zachovat interní close handler a kombinovat jej s dalším chováním, nikoli jej tiše přepsat. ^[how-to/react-cheat-sheet/05-dialogs.md:112-117]

## Stav a průběh zavření

React stav je zdroj pravdy pro otevření dialogu. Zavření vede přes `onOpenChange(false)` k odstranění stavu a odmountování dialogu. Dialog proto nemá být současně řízený propem `open`, vlastním nesynchronizovaným stavem a globálním storem; souvisí to s [[Dialog state ownership and lifecycle]]. ^[how-to/react-cheat-sheet/05-dialogs.md:7-23]

U lokálního dialogu lze předat `setIsOpen` přímo jako `onOpenChange`. V globální službě musí renderer při zavření odstranit konkrétní dialog podle jeho `id`, aby se změna týkala správné instance. Typovaný store k tomu nabízí `closeDialog(id)`; viz [[Local dialog state]] a [[Type-safe dialog stores]]. ^[how-to/react-cheat-sheet/05-dialogs.md:31-42, how-to/react-cheat-sheet/05-dialogs.md:73-81, how-to/react-cheat-sheet/05-dialogs.md:114-116]

## Potvrzení a další způsoby zavření

Interaktivní confirm dialog má po potvrzení nejprve zavřít dialog a teprve potom podle potřeby provést navazující akci. Při skládání callbacků je proto nutné zachovat toto pořadí i interní obsluhu zavření. ^[how-to/react-cheat-sheet/05-dialogs.md:116-117]

Dialog primitive zajišťuje Escape, kliknutí mimo obsah, focus trap, overlay a animaci. Kompozice handlerů musí respektovat také [[Accessible dialog behavior]]: Escape má dialog zavřít, pokud není záměrně zakázaný, a po zavření se má focus vrátit na trigger. ^[how-to/react-cheat-sheet/05-dialogs.md:54-61, how-to/react-cheat-sheet/05-dialogs.md:146-154]

## Sources

- [Dialogs](how-to/react-cheat-sheet/05-dialogs.md)
