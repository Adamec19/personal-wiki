---
title: Controlled Components and State Ownership
summary: Use controlled components when parents need to know or manage values, and avoid copying props into local state because it creates synchronization problems.
sources:
  - how-to/react-cheat-sheet/02-components.md
kind: concept
createdAt: "2026-11-11T10:57:56.322Z"
updatedAt: "2026-11-11T10:57:56.322Z"
tags:
  - components
  - state-management
aliases:
  - controlled-components-and-state-ownership
  - State Ownership and Controlled Components
  - CCASO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Controlled Components and State Ownership

A controlled component receives its value from a parent and reports requested changes through a callback. Use this pattern when the parent needs to know or control the value. ^[how-to/react-cheat-sheet/02-components.md:25-37]

## Value and change contract

The `Toggle` example receives `isOn` as a prop and calls `onChange(!isOn)` when clicked. The parent controls the value supplied to the component, while the component exposes the interaction through its callback. These props form the component’s public API; keeping them small and explicit makes the contract clear. See [[Component Props as a Public Contract]]. ^[how-to/react-cheat-sheet/02-components.md:5-5, how-to/react-cheat-sheet/02-components.md:27-37]

```tsx
type ToggleProps = {
  isOn: boolean;
  onChange: (isOn: boolean) => void;
};

const Toggle = ({ isOn, onChange }: ToggleProps) => {
  return (
    <button onClick={() => onChange(!isOn)}>
      {isOn ? "On" : "Off"}
    </button>
  );
};

export { Toggle };
```

## Avoid duplicate state

Do not copy props into local state merely to make them easier to work with: doing so introduces a synchronization problem. For a controlled component, use the supplied value directly rather than maintaining a second local copy. See [[Odvozené hodnoty a jediný zdroj pravdy]]. ^[how-to/react-cheat-sheet/02-components.md:27-39]

## Decision ownership

Keep callbacks with the component that owns the decision, and name event handlers after the action, such as `onSubmit`, `onRemove`, or `onChange`. General-purpose buttons and inputs should not contain business decisions. See [[Event Callbacks and Decision Ownership]] and [[Oddělení business logiky od generického UI]]. ^[how-to/react-cheat-sheet/02-components.md:57-61]

## Sources

- how-to/react-cheat-sheet/02-components.md
