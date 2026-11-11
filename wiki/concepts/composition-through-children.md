---
title: Composition Through Children
summary: Let visual wrappers accept children so they remain independent of the specific content they contain.
sources:
  - how-to/react-cheat-sheet/02-components.md
kind: concept
createdAt: "2026-11-11T10:58:00.575Z"
updatedAt: "2026-11-11T10:58:00.575Z"
tags:
  - components
  - composition
aliases:
  - composition-through-children
  - CTC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Composition Through Children

Composition přes `children` umožňuje oddělit vizuální wrapper od konkrétního obsahu. Wrapper určuje obalovou strukturu, zatímco obsah dostává prostřednictvím prop `children`. ^[how-to/react-cheat-sheet/02-components.md:41-55]

## Příklad

Komponenta `Card` přijímá `children` typu `React.ReactNode` a vykresluje je uvnitř elementu `article`. Při použití lze jako obsah předat například komponentu `UserSummary`. ^[how-to/react-cheat-sheet/02-components.md:45-55]

```tsx
const Card = ({ children }: { children: React.ReactNode }) => {
  return <article className="card">{children}</article>;
};

export { Card };

<Card>
  <UserSummary />
</Card>;
```

## Kdy composition použít

Pokud se dvě použití liší pouze několika řádky JSX, zvaž nejprve composition. Samostatná znovupoužitelná komponenta má mít stabilní účel, jasný kontrakt a více reálných použití; samotná snaha odstranit opakování podle DRY není dostatečným důvodem pro vytvoření abstrakce. Souvisejícím tématem je [[Criteria for Reusable Components]]. ^[how-to/react-cheat-sheet/02-components.md:64-66]

Při návrhu wrapperu zůstávají props jeho veřejným API. Preferované malé a explicitní rozhraní rozebírá také [[Component Props as a Public Contract]]. ^[how-to/react-cheat-sheet/02-components.md:3-5]

## Sources

- [how-to/react-cheat-sheet/02-components.md](how-to/react-cheat-sheet/02-components.md)
