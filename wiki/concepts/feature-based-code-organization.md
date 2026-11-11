---
title: Feature-based code organization
summary: Group code by domain or feature, keeping related components, hooks, models, and services together.
sources:
  - how-to/react-cheat-sheet/01-architecture.md
kind: concept
createdAt: "2026-11-11T10:57:37.525Z"
updatedAt: "2026-11-11T10:57:37.525Z"
tags:
  - architecture
  - code-organization
aliases:
  - feature-based-code-organization
  - FCO
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Feature-based code organization

Feature-based code organization groups code by domain or feature rather than solely by file type. Each feature keeps its components, hooks, models, and services together, while application composition and globally shared code occupy separate directories. ^[how-to/react-cheat-sheet/01-architecture.md:3-21]

## Directory structure

The suggested structure places routes, layouts, and the composition root in `app/`; globally shared UI in `components/`; general utilities and infrastructure in `lib/`; and global services and integrations in `services/`. Domain-specific code belongs under `features/`, with directories such as `checkout/` and `profile/`. ^[how-to/react-cheat-sheet/01-architecture.md:7-21]

```text
src/
├── app/
├── components/
├── lib/
├── services/
└── features/
    ├── checkout/
    │   ├── components/
    │   ├── hooks/
    │   ├── models/
    │   ├── services/
    │   └── page.tsx
    └── profile/
```

## Dependencies and shared logic

A feature may use the shared layer, but shared code should not import a specific feature. Features should also avoid direct coupling to one another. When logic is needed in multiple places, move the genuinely general portion into the shared layer. See [[Layered dependencies and feature isolation]] and [[Shared logic extraction]]. ^[how-to/react-cheat-sheet/01-architecture.md:23-31]

## Server and client responsibilities

In frameworks with a server/client boundary, keep that boundary as deep as practical. Server components prepare data and compose the page; client components own interactivity, events, and browser APIs. Avoid applying `"use client"` automatically to an entire feature. See [[Server and client component boundaries]]. ^[how-to/react-cheat-sheet/01-architecture.md:33-55]

## Design checks

Each module should have one clear responsibility, and business logic should live outside route and layout files. Check that shared code does not import specific features, client boundaries exist only where interactivity requires them, and each feature can be tested without starting the entire application. Related concepts include [[Separation of business logic from routing]] and [[Independent feature testability]]. ^[how-to/react-cheat-sheet/01-architecture.md:58-64]

## Sources

- [Architecture](how-to/react-cheat-sheet/01-architecture.md)
