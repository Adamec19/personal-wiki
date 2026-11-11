---
title: Type-safe dialog stores
summary: A discriminated union connects each dialog type to its required props, while unique IDs identify individual open dialogs.
sources:
  - how-to/react-cheat-sheet/05-dialogs.md
kind: concept
createdAt: "2026-11-11T10:58:59.162Z"
updatedAt: "2026-11-11T10:58:59.162Z"
tags:
  - typescript
  - state-management
  - dialogs
aliases:
  - type-safe-dialog-stores
  - TDS
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Type-safe dialog stores

A type-safe dialog store associates each dialog type with its required props, maintains the open dialogs, and gives each instance a unique `id`. In a [[Global dialog service architecture|global dialog service]], it connects a typed `openDialog(type, props)` call to a renderer that selects the appropriate dialog component. ^[how-to/react-cheat-sheet/05-dialogs.md:44-60, how-to/react-cheat-sheet/05-dialogs.md:65-89]

## Type model

Define a map of dialog types to their props, then derive a union of dialog instances using [[TypeScript Mapped Types]] and [[TypeScript Indexed Access Types]]. The generic `openDialog` signature ties its `props` argument to the selected `type`. ^[how-to/react-cheat-sheet/05-dialogs.md:67-81]

```tsx
type DialogMap = {
  info: { title: string; content: React.ReactNode };
  confirm: { title: string; onConfirm: () => void };
};

type Dialog = {
  [K in keyof DialogMap]: { id: string; type: K; props: DialogMap[K] };
}[keyof DialogMap];

type DialogStore = {
  dialogs: Dialog[];
  openDialog: <T extends keyof DialogMap>(type: T, props: DialogMap[T]) => string;
  closeDialog: (id: string) => void;
};
```

Here, an `info` dialog requires `title` and `content`, while a `confirm` dialog requires `title` and `onConfirm`. Each stored instance preserves the relationship between its discriminator and props, following the [[Discriminated Unions]] pattern. Opening a dialog returns a string identifier; closing one accepts that identifier. ^[how-to/react-cheat-sheet/05-dialogs.md:68-81]

## Responsibilities and integration

The store owns the list of open dialogs and their identifiers. A provider exposes it to the React tree, and a global renderer maps each dialog type to a component. The dialog primitive handles overlay behavior, focus trapping, Escape, outside clicks, and animation. This separation allows the visual implementation to change without updating every trigger. ^[how-to/react-cheat-sheet/05-dialogs.md:54-63]

Use [[Feature hooks for dialogs]] to assemble translated titles, content, and callbacks instead of repeating direct store calls across many components. Translations belong in the i18n layer rather than the global store. ^[how-to/react-cheat-sheet/05-dialogs.md:91-110, how-to/react-cheat-sheet/05-dialogs.md:119-119]

## State ownership and closing

React state should remain the single source of truth: avoid controlling the same dialog through an `open` prop, unsynchronized internal state, and a global store simultaneously. The provider must wrap both the triggers and the global renderer. When a dialog closes, the renderer must remove its specific `id`, and any supplied `onOpenChange` callback must be composed with the internal close handler. ^[how-to/react-cheat-sheet/05-dialogs.md:23-23, how-to/react-cheat-sheet/05-dialogs.md:114-116]

For a confirmation dialog, close the dialog before performing the confirmation action as needed. These lifecycle responsibilities accompany the typed store contract. ^[how-to/react-cheat-sheet/05-dialogs.md:117-117]

## When to use it

A global dialog service suits repeated informational or confirmation dialogs and cases where triggers are far from the renderer. Prefer [[Local dialog state]] when one component owns the dialog, its content depends on local state, and there is no need for distant triggers or a stack of dialogs. ^[how-to/react-cheat-sheet/05-dialogs.md:29-29, how-to/react-cheat-sheet/05-dialogs.md:44-46, how-to/react-cheat-sheet/05-dialogs.md:156-163]

## Sources

- [Dialogs](how-to/react-cheat-sheet/05-dialogs.md)
