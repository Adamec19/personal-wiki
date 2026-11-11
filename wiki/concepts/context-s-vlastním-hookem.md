---
title: Context s vlastním hookem
summary: Provider zpřístupňuje sdílený stav a operace přes Context a vlastní hook kontroluje, zda je použit uvnitř příslušného provideru.
sources:
  - how-to/react-cheat-sheet/10-component-snippets.md
kind: concept
createdAt: "2026-11-11T11:00:53.596Z"
updatedAt: "2026-11-11T11:00:53.596Z"
tags:
  - react
  - context
  - hooks
  - state-management
aliases:
  - context-s-vlastním-hookem
  - CSVH
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Context s vlastním hookem

Context s vlastním hookem zpřístupňuje sdílené hodnoty a operace prostřednictvím provideru. V ukázce košíku poskytuje `CartProvider` počet položek a funkci pro přidání produktu; komponenty k nim přistupují přes `useCart`. Souvisí s koncepty [[React Context and Providers]] a [[Custom Hooks]]. ^[how-to/react-cheat-sheet/10-component-snippets.md:49-75]

## Datový kontrakt a provider

Typ `CartContextValue` definuje veřejný kontrakt: `count` je číslo a `add` přijímá identifikátor produktu. Context má výchozí hodnotu `null`. Provider uchovává pole identifikátorů produktů pomocí `useState`, počet položek odvozuje z jeho délky a při přidání vytváří nové pole pomocí funkční aktualizace stavu. ^[how-to/react-cheat-sheet/10-component-snippets.md:52-67]

```tsx
type CartContextValue = {
  count: number;
  add: (productId: string) => void;
};

const CartContext = createContext<CartContextValue | null>(null);

const CartProvider = ({ children }: { children: React.ReactNode }) => {
  const [items, setItems] = useState<string[]>([]);
  const value = {
    count: items.length,
    add: (productId: string) => setItems((current) => [...current, productId])
  };

  return <CartContext value={value}>{children}</CartContext>;
};
```

Hodnota `count` není samostatný stav, ale výpočet z `items.length`. Tento postup souvisí s principem [[Odvozené hodnoty a jediný zdroj pravdy]]. ^[how-to/react-cheat-sheet/10-component-snippets.md:60-64]

## Vlastní hook a kontrola provideru

Hook `useCart` načte hodnotu přes `useContext`. Pokud provider chybí, vyhodí chybu s vysvětlením požadovaného použití. Jinak vrátí hodnotu contextu. Společně s providerem tvoří exportované rozhraní ukázky. ^[how-to/react-cheat-sheet/10-component-snippets.md:69-75]

```tsx
const useCart = () => {
  const context = useContext(CartContext);
  if (!context) throw new Error("useCart must be used inside CartProvider");
  return context;
};

export { CartProvider, useCart };
```

## Kdy Context použít

Při návrhu je vhodné ověřit, zda je Context skutečně potřeba, nebo zda postačí props či kompozice. Veřejný kontrakt má zůstat malý a typovaný a generická komponenta nemá obsahovat business logiku. S rozhodnutím souvisí [[Umístění a sdílení stavu v komponentovém stromu]] a [[Composition Through Children]]. ^[how-to/react-cheat-sheet/10-component-snippets.md:128-135]

Ukázka je výchozí kostra, kterou je potřeba přizpůsobit accessibility, design systému, zpracování chyb a datovému kontraktu konkrétní aplikace. ^[how-to/react-cheat-sheet/10-component-snippets.md:3-3]

## Sources

- [Component Snippets](how-to/react-cheat-sheet/10-component-snippets.md)
