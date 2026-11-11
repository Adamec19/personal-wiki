---
title: Shared logic extraction
summary: Move genuinely general logic used in multiple places into the shared layer.
sources:
  - how-to/react-cheat-sheet/01-architecture.md
kind: concept
createdAt: "2026-11-11T10:57:40.357Z"
updatedAt: "2026-11-11T10:57:40.357Z"
tags:
  - code-reuse
  - modularity
aliases:
  - shared-logic-extraction
  - SLE
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Shared logic extraction

Shared logic extraction means moving the genuinely general part of logic used in multiple places into a shared layer. Feature-specific code remains grouped by domain or feature, rather than only by file type. ^[how-to/react-cheat-sheet/01-architecture.md:3-21, how-to/react-cheat-sheet/01-architecture.md:31-31]

## Dependency boundaries

A feature may use the shared layer, but shared code should not import a concrete feature. Two features should also avoid direct coupling. Extracting their genuinely common logic into shared code supports these boundaries; see [[Layered dependencies and feature isolation]]. ^[how-to/react-cheat-sheet/01-architecture.md:23-31]

## Placement and responsibility

The illustrated structure places globally shared UI in `components/`, general utilities and infrastructure in `lib/`, and global services and integrations in `services/`. Individual features retain their own components, hooks, models, and services. This combines shared facilities with [[Feature-based code organization]]. ^[how-to/react-cheat-sheet/01-architecture.md:5-21]

## Review criteria

When reviewing an extraction, check that each module has one clear responsibility, shared code does not import a specific feature, and the feature can be tested without starting the entire application. Business logic should also remain outside route and layout files. ^[how-to/react-cheat-sheet/01-architecture.md:58-64]

## Sources

- [Architecture](how-to/react-cheat-sheet/01-architecture.md)
