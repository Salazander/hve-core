---
title: C4 Modelling instructions
description: C4 Modelling instructions
author: Microsoft
ms.date: 2026-08-11
ms.topic: reference
---

This file lists extended modelling rules to apply when creating a C4 model.

## Mandatory modelling uncertainty gate

Before producing diagrams, identify decisions about:

- system boundaries and ownership
- internal containers versus external systems
- data-store ownership
- component relationships and relationship technologies
- current versus planned architecture
- abstraction level and diagram scope

MUST ask the user before proceeding when:

- documentation and implementation disagree
- ownership is not explicitly evidenced
- one platform hosts both repository-owned and externally owned data
- component responsibilities are known but their interactions are not evidenced
- two or more classifications are plausible
- planned and implemented elements coexist
- the selected system boundary materially changes the diagrams

Do not infer data ownership from the hosting platform. Determine who defines,
migrates, seeds, and operates each schema. Model separately owned data as
separate C4 elements even when it shares the same database platform.

When asking, state the evidence and provide the plausible options. Do not create
or modify diagrams until the user resolves the decision.

## Mandatory deployment diagram offer

When the provided context contains infrastructure-as-code or deployment code,
MUST ask the user whether to include a deployment diagram before producing the
report. Evidence includes cloud resource definitions, deployment manifests,
container orchestration configuration, CI/CD deployment workflows, and
deployment scripts. State the evidence found and the environment or environments
that can be modeled. Do not ask again when the user has already explicitly
requested or declined a deployment diagram.

Generate the deployment diagram only when the user opts in. Model only topology
supported by the provided evidence; do not infer deployed nodes, environments,
regions, instance counts, or network boundaries from application code alone.
Place each container instance only inside a deployment node that the evidence
identifies as its execution environment. A user-facing name or responsibility
does not establish browser execution; use a browser deployment node only when
the evidence states that the container code executes there. When deployment
sources disagree about placement, stop and ask the user to resolve the conflict.

## Naming consistency rule

Use the same name for an element in every C4 diagram where it appears, including system context, container, and component diagrams. When code or documentation already names the element, use that established name instead of introducing a synonym or abbreviation. Before finalizing the model, verify that repeated elements use identical names across all diagram levels.

## Element introduction rule

Introduce each element at its owning diagram level: users and software systems first appear at L1 (system context), containers first appear at L2 (container), and components first appear at L3 (component). A lower-level diagram may repeat a higher-level element only when that element already appears in the corresponding higher-level diagram; it must not introduce a new higher-level element.

For example, do not add a user or software system to a container or component diagram unless it appears in the system context diagram. Likewise, do not add a container to a component diagram unless it appears in the container diagram. When a lower-level view requires an element that is missing from its owning level, update the higher-level diagram first.

## Component relationship evidence rule

Create a component relationship only when code, configuration, or documentation
identifies the interaction. Component responsibilities, names, and membership in
the same container do not establish control flow or dependencies. Use a
relationship technology only when the evidence identifies it; otherwise omit
the technology details. When missing relationship evidence materially affects the
component diagram, state the evidence gap and plausible interactions, then ask
the user before producing diagrams.

## Edge direction rule

Every arrow starts at the **initiator** (the actor, system, container, or component that begins the interaction or owns the dependency) and points to the **dependency** (the thing being called, consumed, or relied upon). Direction encodes "who depends on whom".

## Cross-level role consistency rule

An initiating client system or user at L1 MUST stay an initiating client system or user at L2.
A dependency or external system at L1 MUST stay a dependency or external system at L2.
NEVER change an element's role (initiator vs dependency) between the System Context and Container Diagram.

## External system rules

- **Ownership decides External System vs Container.** If it stores your data or executes code you wrote, it is a **container** (inside the system boundary). If it is a capability you call but do not own or deploy, it is an **external system**. A managed cloud service you provision and deploy your own schema, functions, or code into is a container; a third-party API or shared service you merely call is external. When in doubt, ask: "Did we deploy code or data into this, or do we just call it?"
- Only depict an external system when a container or component in the codebase actively uses it (the integration is observable in code, config, or manifests). Do not include external systems that are merely possible, aspirational, or transitively reachable but never called by this system.
- An external system the in-focus system calls out to is a **dependency**. An external system that initiates the interaction — it calls into the in-focus system rather than being called — is an **actor** for layout purposes.

## Sources

* [C4 Model](https://c4model.com/)
