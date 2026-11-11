---
title: Independent feature testability
summary: Design features so they can be tested without starting the entire application.
sources:
  - how-to/react-cheat-sheet/01-architecture.md
kind: concept
createdAt: "2026-11-11T10:57:50.576Z"
updatedAt: "2026-11-11T10:57:50.576Z"
tags:
  - testing
  - modularity
aliases:
  - independent-feature-testability
  - IFT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Independent feature testability

Independent feature testability means being able to test a feature without starting the entire application. It is an explicit check in the architecture checklist, alongside clear module responsibilities, separation of business logic from routes and layouts, and controlled dependency boundaries. ^[how-to/react-cheat-sheet/01-architecture.md:58-64]

## Feature organization

A [[Feature-based code organization|feature-based structure]] groups code by domain or feature rather than only by file type. A feature can contain its own components, hooks, models, and services, while application routes and layouts belong in `app/` and globally shared code has separate locations. This organization keeps the feature’s related parts together. ^[how-to/react-cheat-sheet/01-architecture.md:3-21]

## Dependency boundaries

[[Layered dependencies and feature isolation|Dependency boundaries]] support feature isolation: a feature may use the shared layer, but shared code should not import a specific feature, and separate features should not be directly coupled. When logic is used in multiple places, move the genuinely general part into the shared layer. ^[how-to/react-cheat-sheet/01-architecture.md:23-31]

Each module should have one clear responsibility, and business logic should remain outside route and layout files. These are architectural checks to consider alongside whether the feature can be tested without running the whole application. ^[how-to/react-cheat-sheet/01-architecture.md:58-64]

## Server and client responsibilities

Where a framework provides server/client boundaries, keep the client boundary as deep as practical. Server components prepare data and compose the page; client components own interactivity, events, and browser APIs. Avoid applying `use client` automatically to an entire feature. See [[Server and client component boundaries]]. ^[how-to/react-cheat-sheet/01-architecture.md:33-39]

## Sources

- [Architecture](how-to/react-cheat-sheet/01-architecture.md)
