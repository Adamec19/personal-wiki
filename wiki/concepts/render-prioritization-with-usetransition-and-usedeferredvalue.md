---
title: Render Prioritization with useTransition and useDeferredValue
summary: useTransition marks updates as nonurgent, while useDeferredValue lets expensive rendering follow a delayed version of a value.
sources:
  - how-to/react-cheat-sheet/09-hooks-and-context.md
kind: concept
createdAt: "2026-11-11T11:00:33.893Z"
updatedAt: "2026-11-11T11:00:33.893Z"
tags:
  - react
  - rendering
  - performance
aliases:
  - render-prioritization-with-usetransition-and-usedeferredvalue
  - useDeferredValue and Render Prioritization with useTransition
  - RPWUAU
confidence: 1
provenanceState: merged
modelId: codex-cli-default
promptVersion: v7
---

# Render Prioritization with useTransition and useDeferredValue

`useTransition` and `useDeferredValue` help prioritize rendering. `useTransition` marks an update as non-urgent so urgent interactions remain responsive, while `useDeferredValue` provides a deferred version of a value for expensive rendering. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:134-148]

## `useTransition`

Use `useTransition` to mark a state update as non-urgent. It controls render priority; it does not manage the loading state of an API request. This distinction separates render prioritization from [[Správa stavu API požadavků]]. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:134-143]

```tsx
const [isPending, startTransition] = useTransition();

const handleSearch = (value: string) => {
  startTransition(() => setSearch(value));
};
```

The example wraps the `setSearch` update in `startTransition`, marking that update as non-urgent. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:136-143]

## `useDeferredValue`

Use `useDeferredValue` to create a deferred version of a value for expensive rendering. The original value updates immediately, while the deferred value may temporarily lag behind. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:146-148]

## Choosing between them

Choose `useTransition` when you need to mark an update as non-urgent. Choose `useDeferredValue` when you need a deferred version of a value for expensive rendering. The distinction is whether you are prioritizing an update or deferring the value used to render. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:134-148]

These hooks address a different concern from [[Memoization with useMemo and useCallback|memoization]]: `useMemo` memoizes a calculation, and `useCallback` memoizes a function when its identity matters to a memoized child component or another hook’s dependency. ^[how-to/react-cheat-sheet/09-hooks-and-context.md:88-108, how-to/react-cheat-sheet/09-hooks-and-context.md:134-148]

## Sources

- [Hooks and Context](how-to/react-cheat-sheet/09-hooks-and-context.md)
