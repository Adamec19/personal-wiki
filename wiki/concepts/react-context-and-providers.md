---
title: React Context and Providers
summary: Context passes values deeply without prop drilling, and changes to provider values rerender consuming components.
sources:
  - how-to/react-cheat-sheet/09-hooks-and-context.md
kind: concept
createdAt: "2026-11-11T11:00:40.793Z"
updatedAt: "2026-11-11T11:00:40.793Z"
tags:
  - react
  - context
  - data-sharing
aliases:
  - react-context-and-providers
  - Providers and React Context
  - RCAP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# React Context and Providers

React Context předává hodnotu hluboko v komponentovém stromu bez prop drillingu, tedy předávání přes mezilehlé komponenty pomocí props. Sám o sobě není automaticky globálním storem. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:150-152]

## Vytvoření contextu a Provideru

Context vytvoříš pomocí `createContext`. Provider poskytuje hodnotu komponentám ve svém podstromu a ty ji čtou pomocí `useContext`. Následující příklad drží uživatele v lokálním state Provideru a zpřístupňuje jej společně s funkcí pro odhlášení. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:154-176]

```tsx
type AuthValue = {
  user: User | null;
  logout: () => void;
};

const AuthContext = createContext<AuthValue | null>(null);

const AuthProvider = ({ children }: { children: React.ReactNode }) => {
  const [user, setUser] = useState<User | null>(null);

  const value = {
    user,
    logout: () => setUser(null),
  };

  return (
    <AuthContext.Provider value={value}>
      {children}
    </AuthContext.Provider>
  );
};

const useAuth = () => {
  const value = useContext(AuthContext);

  if (!value) {
    throw new Error("useAuth must be used inside AuthProvider");
  }

  return value;
};

export { AuthProvider, useAuth };
```

Vlastní hook `useAuth` zapouzdřuje čtení contextu a vyhodí chybu při použití mimo odpovídající Provider. Tento vzor propojuje [[Context s vlastním hookem|context s vlastním hookem]] a poskytuje konzumentům společné rozhraní. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:169-175]

## Aktualizace a opětovné vykreslování

Když se hodnota Provideru změní, znovu se vykreslí komponenty, které daný context čtou. Proto je vhodné rozdělit nesouvisející contexty a podle potřeby stabilizovat složité hodnoty předávané přes `value`. Se stabilitou hodnot a funkcí souvisí [[Memoization with useMemo and useCallback]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:88-109, how-to/react-cheat-sheet/09-hooks-and-context.md:178-178]

## Zápis Provideru v React 19

V React 19 lze místo `<AuthContext.Provider value={value}>` použít také `<AuthContext value={value}>`. Zápis s `.Provider` je vhodný pro codebase podporující více verzí Reactu. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:180-180]

## Context a sdílení logiky

[[Custom Hooks]] sdílejí logiku, nikoli instance state: každá komponenta, která custom hook zavolá, má vlastní hook state. V uvedeném příkladu je state uložen v `AuthProvider` a `useAuth` čte hodnotu poskytovanou contextem. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:159-173, how-to/react-cheat-sheet/09-hooks-and-context.md:182-184]

## Sources

- [Hooks and Context](how-to/react-cheat-sheet/09-hooks-and-context.md)
