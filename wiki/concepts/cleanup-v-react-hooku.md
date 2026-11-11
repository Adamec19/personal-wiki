---
title: Cleanup v React hooku
summary: Efekt registrující posluchač událostí vrací cleanup funkci, která při úklidu efektu příslušný posluchač odstraní.
sources:
  - how-to/react-cheat-sheet/10-component-snippets.md
kind: concept
createdAt: "2026-11-11T11:00:53.583Z"
updatedAt: "2026-11-11T11:00:53.583Z"
tags:
  - react
  - hooks
  - effects
  - resource-management
aliases:
  - cleanup-v-react-hooku
  - CVRH
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Cleanup v React hooku

Cleanup v React hooku slouží k odstranění registrace vytvořené efektem. Ukázkový hook `useWindowWidth` sleduje šířku okna: v `useEffect` přidá listener události `resize` a vrátí funkci, která tento listener odstraní. Jde o příklad [[Synchronizace s externími systémy pomocí useEffect]]. ^[how-to/react-cheat-sheet/10-component-snippets.md:110-126]

## Příklad: sledování šířky okna

Hook inicializuje stav hodnotou `window.innerWidth`. Handler `handleResize` při změně velikosti okna aktualizuje stav a cleanup předá do `removeEventListener` stejný handler, který byl použit při registraci. Hook vrací aktuální šířku. ^[how-to/react-cheat-sheet/10-component-snippets.md:113-123]

```tsx
const useWindowWidth = () => {
  const [width, setWidth] = useState(() => window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return width;
};

export { useWindowWidth };
```

Ukázka propojuje správu stavu a registraci listeneru v jednom [[Custom Hooks|vlastním hooku]]. Stejně jako ostatní snippety ve zdroji představuje výchozí kostru, kterou je třeba přizpůsobit požadavkům konkrétní aplikace. ^[how-to/react-cheat-sheet/10-component-snippets.md:3-3, how-to/react-cheat-sheet/10-component-snippets.md:110-126]

## Sources

- [Component Snippets](how-to/react-cheat-sheet/10-component-snippets.md)
