---
title: c4-architecture
description: "Model and document existing or planned software architectures with the C4 model across System Context, Container, and Component levels plus deployment diagrams, then emit diagrams through a selected renderer. Use when an architect needs audience-appropriate software architecture documentation; use the 'architecture-diagrams' skill for infrastructure topology."
sidebar_position: 2
ms.date: 2026-08-11
---

<!-- BEGIN AUTO-GENERATED: metadata -->
| Field       | Value                                                                             |
|-------------|-----------------------------------------------------------------------------------|
| Kind        | skill                                                                             |
| Source      | `.github/skills/hve-core/c4-architecture`                                         |
| Invocation  | Invoked directly as `/c4-architecture`, or loaded on demand by referencing agents |
| Interactive | No                                                                                |
<!-- END AUTO-GENERATED: metadata -->

## What it does

<!-- BEGIN AUTO-GENERATED: overview -->
Model and document existing or planned software architectures with the C4 model across System Context, Container, and Component levels plus deployment diagrams, then emit diagrams through a selected renderer. Use when an architect needs audience-appropriate software architecture documentation; use the 'architecture-diagrams' skill for infrastructure topology.
<!-- END AUTO-GENERATED: overview -->

## When to use it

Use it to document how a software system is composed, from either existing code or a planned design. It emits System Context, Container, and Component diagrams by default; Code only on request, and Deployment only when the evidence describes where containers run.

Use `architecture-diagrams` instead for cloud infrastructure topology. Mermaid is the only supported renderer; other renderers stop with a reported limitation.

## Example usage

```text
/c4-architecture Document the architecture of the ordering service in this repo,
including a code-level view of the pricing logic.
```

The skill either returns the diagrams with a source-validation and Mermaid CLI status, or stops and asks when ownership or the system boundary is unevidenced. When `mmdc` is on your `PATH` it renders each diagram automatically to catch parse errors.
