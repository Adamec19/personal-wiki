---
title: Component Props as a Public Contract
summary: Define component APIs with small, explicit props instead of broad objects containing many optional values.
sources:
  - how-to/react-cheat-sheet/02-components.md
kind: concept
createdAt: "2026-11-11T10:57:55.486Z"
updatedAt: "2026-11-11T10:57:55.486Z"
tags:
  - components
  - api-design
aliases:
  - component-props-as-a-public-contract
  - CPAAPC
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Component Props as a Public Contract

Props define a component’s public API. A clear contract favors a small, explicit set of props over a universal object containing many optional values. ^[how-to/react-cheat-sheet/02-components.md:3-5]

## Expressing the contract

A `SaveButton` can expose optional `disabled` and `isSaving` flags alongside a required `onSave` callback. Both flags default to `false`; either flag disables the button, while `isSaving` also changes its label. This makes the component’s supported inputs and interaction explicit. ^[how-to/react-cheat-sheet/02-components.md:8-20]

```tsx
type SaveButtonProps = {
  disabled?: boolean;
  isSaving?: boolean;
  onSave: () => void;
};

const SaveButton = ({
  disabled = false,
  isSaving = false,
  onSave,
}: SaveButtonProps) => {
  return (
    <button type="button" disabled={disabled || isSaving} onClick={onSave}>
      {isSaving ? "Ukládám…" : "Uložit"}
    </button>
  );
};
```

## State ownership

When a parent needs to know or control a value, use a controlled component: receive the value through props and report changes through a callback. Copying props into local state merely for convenience creates a synchronization problem. See [[Controlled Components and State Ownership]]. ^[how-to/react-cheat-sheet/02-components.md:25-39]

## Composition and callbacks

A visual wrapper can accept `children` without knowing its specific content. This allows its contract to describe the wrapper while callers supply what appears inside it. See [[Composition Through Children]]. ^[how-to/react-cheat-sheet/02-components.md:41-55]

Name event handlers after actions, such as `onSubmit`, `onRemove`, or `onChange`. Keep callbacks with the component that owns the decision, and keep business decisions out of generic buttons and inputs. See [[Event Callbacks and Decision Ownership]]. ^[how-to/react-cheat-sheet/02-components.md:57-61]

## Reusability

A reusable component should have a stable purpose, a clear contract, and multiple real uses. When implementations differ by only a couple of JSX lines, consider composition before introducing an abstraction solely to avoid duplication. See [[Criteria for Reusable Components]]. ^[how-to/react-cheat-sheet/02-components.md:64-66]

## Sources

- [Components](how-to/react-cheat-sheet/02-components.md)
