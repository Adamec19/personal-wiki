---
title: Dialog state ownership and lifecycle
summary: A single source of truth controls dialog opening, rendering, closing, and unmounting.
sources:
  - how-to/react-cheat-sheet/05-dialogs.md
kind: concept
createdAt: "2026-11-11T10:58:52.283Z"
updatedAt: "2026-11-11T10:58:52.283Z"
tags:
  - dialogs
  - state-management
  - react
aliases:
  - dialog-state-ownership-and-lifecycle
  - lifecycle and Dialog state ownership
  - DSOAL
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Dialog state ownership and lifecycle

A dialog coordinates state ownership, rendering, focus, closing behavior, content, and accessibility. React state is its source of truth: a dialog should not be controlled simultaneously by an `open` prop, unsynchronized internal state, and a global store. ^[how-to/react-cheat-sheet/05-dialogs.md:3-23]

## Choosing the state owner

Use [[Local dialog state]] when the dialog belongs to one component and does not need to open from distant parts of the application. Local ownership is also appropriate when its content depends on local state or there is no need to manage several dialogs as a stack. ^[how-to/react-cheat-sheet/05-dialogs.md:27-42, how-to/react-cheat-sheet/05-dialogs.md:156-163]

A [[Global dialog service architecture|global dialog service]] suits repeated information dialogs, confirmation dialogs, and cases where triggers and dialog rendering are far apart. Its flow is trigger → typed `openDialog(type, props)` → store → global renderer → dialog component. The store holds open dialogs and their identifiers, while the renderer maps each dialog type to a component. ^[how-to/react-cheat-sheet/05-dialogs.md:44-61]

## Opening and closing lifecycle

A user action calls `openDialog(...)` or `setIsOpen(true)`. The state change causes React to render the dialog, which establishes focus, an overlay, and close handlers. Closing flows through `onOpenChange(false)`, followed by removal of the dialog state and unmounting. ^[how-to/react-cheat-sheet/05-dialogs.md:7-21]

For a local controlled dialog, `open={isOpen}` and `onOpenChange={setIsOpen}` connect rendering and close requests to the same state owner. In a global service, each open dialog has its own `id`, and closing must remove the corresponding entry. ^[how-to/react-cheat-sheet/05-dialogs.md:31-42, how-to/react-cheat-sheet/05-dialogs.md:77-89, how-to/react-cheat-sheet/05-dialogs.md:114-115]

[[Dialog close-handler composition]] preserves internal cleanup when an external `onOpenChange` callback is supplied; the callback should be combined with the internal close handler rather than silently replacing it. A confirmation dialog should close after confirmation before performing the associated action as needed. ^[how-to/react-cheat-sheet/05-dialogs.md:116-117]

## Provider and rendering boundaries

In a global service, the provider must wrap both the triggers and the global renderer. [[Feature hooks for dialogs]] can prepare translated titles, content, and callbacks so individual triggers do not repeatedly assemble the same dialog configuration. Translations belong in the i18n layer rather than the global store. ^[how-to/react-cheat-sheet/05-dialogs.md:54-61, how-to/react-cheat-sheet/05-dialogs.md:91-110, how-to/react-cheat-sheet/05-dialogs.md:114-119]

[[React portals and context propagation|Portals]] change a dialog’s physical DOM location while preserving its position in the React tree. Context therefore comes from where the dialog is rendered in that tree. A dialog requiring a feature store must receive that store explicitly or render under the appropriate provider. ^[how-to/react-cheat-sheet/05-dialogs.md:118-125]

## Focus and accessibility lifecycle

[[Accessible dialog behavior]] includes moving focus to a meaningful element when the dialog opens, supporting Escape to close unless deliberately disabled, and returning focus to the trigger after closing. The dialog also needs an accessible title, `role="dialog"`, `aria-modal="true"`, and clear keyboard behavior for the overlay and close button. A portal alone does not provide focus trapping or ARIA behavior; the dialog primitive or custom implementation must supply them. ^[how-to/react-cheat-sheet/05-dialogs.md:144-154]

## Sources

- [Dialogs](how-to/react-cheat-sheet/05-dialogs.md)
