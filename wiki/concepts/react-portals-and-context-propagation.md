---
title: React portals and context propagation
summary: The source explains that portals relocate DOM output while preserving React context and event propagation, contradicting its earlier suggestion that portals can change context boundaries.
sources:
  - how-to/react-cheat-sheet/05-dialogs.md
kind: concept
createdAt: "2026-11-11T10:59:11.149Z"
updatedAt: "2026-11-11T10:59:11.149Z"
tags:
  - react
  - portals
  - context
aliases:
  - react-portals-and-context-propagation
  - context propagation and React portals
  - RPACP
confidence: 1
provenanceState: ambiguous
modelId: codex-cli-default
promptVersion: v7
---

# React portals and context propagation

React portál mění fyzické umístění obsahu v DOM, ale zachovává jeho místo v React stromu. Obsah portálu proto nadále vidí [[React Context and Providers|React context]] dostupný v místě, kde byl vyrenderován, a události se propagují podle React stromu. ^[how-to/react-cheat-sheet/05-dialogs.md:121-125]

## Portály v dialozích

Dialog se často vykresluje pomocí `createPortal(..., document.body)`, aby nebyl oříznutý rodičovským `overflow: hidden` nebo omezený lokálním stacking contextem. Přesunutí do `document.body` přitom nemění jeho vazbu na React strom. ^[how-to/react-cheat-sheet/05-dialogs.md:123-125]

```tsx
"use client";

import { createPortal } from "react-dom";

const Modal = ({ children }: { children: React.ReactNode }) => {
  return createPortal(
    <div role="dialog" aria-modal="true">
      {children}
    </div>,
    document.body
  );
};

export { Modal };
```

Tento příklad vytváří portál v client komponentě, protože `document.body` na serveru neexistuje. Samotný portál nezajišťuje focus trap ani ARIA; tyto části musí dodat dialog primitive nebo vlastní implementace. ^[how-to/react-cheat-sheet/05-dialogs.md:127-144]

## Dostupnost contextu a propagace událostí

Pro dostupnost feature contextu je rozhodující umístění dialogu vůči provideru v React stromu. Pokud dialog potřebuje feature store, zdroj doporučuje předat mu store explicitně nebo dialog renderovat uvnitř odpovídajícího provideru. V [[Global dialog service architecture|globální dialogové službě]] musí provider obalit triggery i globální renderer. ^[how-to/react-cheat-sheet/05-dialogs.md:114-118, how-to/react-cheat-sheet/05-dialogs.md:123-125]

Také události z obsahu portálu se propagují podle React stromu. Kliknutí uvnitř dialogu proto může probublat k jeho React rodičům, přestože je dialog v DOM umístěn jinde. ^[how-to/react-cheat-sheet/05-dialogs.md:125-125]

## Přístupnost

Portál řeší umístění obsahu, zatímco [[Accessible dialog behavior|přístupné chování dialogu]] vyžaduje další implementaci: přístupný název, smysluplný focus po otevření, zavírání klávesou Escape, návrat focusu na trigger a jasné ovládání klávesnicí. ^[how-to/react-cheat-sheet/05-dialogs.md:144-154]

## Sources

- [Dialogs](how-to/react-cheat-sheet/05-dialogs.md)
