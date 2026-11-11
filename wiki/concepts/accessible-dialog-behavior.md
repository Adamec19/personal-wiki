---
title: Accessible dialog behavior
summary: Accessible dialogs require semantic roles, an accessible name, focus management and restoration, and predictable keyboard dismissal; portals alone do not provide these behaviors.
sources:
  - how-to/react-cheat-sheet/05-dialogs.md
kind: concept
createdAt: "2026-11-11T10:59:16.626Z"
updatedAt: "2026-11-11T10:59:16.626Z"
tags:
  - accessibility
  - dialogs
  - keyboard-navigation
aliases:
  - accessible-dialog-behavior
  - ADB
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Accessible dialog behavior

Přístupný dialog řeší kromě otevření a zavření také focus, ovládání klávesnicí a přístupné označení. Tyto povinnosti patří do dialog primitive nebo vlastní implementace dialogu. ^[how-to/react-cheat-sheet/05-dialogs.md:3-3, how-to/react-cheat-sheet/05-dialogs.md:54-61, how-to/react-cheat-sheet/05-dialogs.md:144-154]

## Označení a ovládání

Dialog má mít `role="dialog"` a `aria-modal="true"`. Musí mít také přístupný název, například prostřednictvím `aria-labelledby` nebo textového labelu. Dialog se nemá používat pro běžný obsah, který může být přímo na stránce. ^[how-to/react-cheat-sheet/05-dialogs.md:146-154]

Po otevření má focus získat smysluplný prvek uvnitř dialogu. Dialog primitive zajišťuje focus trap a po zavření se focus vrací na prvek, který dialog otevřel. Klávesa Escape dialog zavírá, pokud toto chování není záměrně zakázané; overlay i zavírací tlačítko musí mít jasné ovládání klávesnicí. ^[how-to/react-cheat-sheet/05-dialogs.md:54-61, how-to/react-cheat-sheet/05-dialogs.md:148-153]

## Zavření a životní cyklus

Zavření musí navazovat na [[Dialog state ownership and lifecycle|vlastnictví stavu a životní cyklus dialogu]]. U globálního rendereru je potřeba odstranit konkrétní dialog podle jeho `id`. Vlastní `onOpenChange` se kombinuje s interním close handlerem, aby jej tiše nepřepsal; podrobněji viz [[Dialog close-handler composition]]. Confirm dialog se po potvrzení zavře a teprve potom podle potřeby provede navazující akci. ^[how-to/react-cheat-sheet/05-dialogs.md:18-23, how-to/react-cheat-sheet/05-dialogs.md:114-117]

## Portál a jeho omezení

Dialog se často vykresluje přes portál do `document.body`, aby nebyl oříznutý rodičovským `overflow: hidden` nebo omezený lokálním stacking contextem. Portál mění umístění v DOM, ale zachovává React strom, jeho context i propagaci událostí. Samotný portál nezajišťuje focus trap ani ARIA; ty musí dodat implementace dialogu. Další souvislosti popisuje [[React portals and context propagation]]. ^[how-to/react-cheat-sheet/05-dialogs.md:121-144]

## Sources

- [Dialogs](how-to/react-cheat-sheet/05-dialogs.md)
