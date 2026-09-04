<div align="center">

<a href="https://github.com/Phantom-Con-Artist/Orbis">
  <img src="docs/orbisprojectcover.png" alt="Orbis Project" width="900">
</a>

<br>

<a href="https://github.com/Phantom-Con-Artist/Orbis">
  <img src="docs/orbis-project-krono.png" alt="Orbis Project Logo" width="900">
</a>

# Orbis Project

### **An open architecture for structured, connected knowledge.**

[![Status](https://img.shields.io/badge/status-active--development-2ea44f?style=for-the-badge)](https://github.com/Phantom-Con-Artist/Orbis)
[![Architecture](https://img.shields.io/badge/architecture-MIT-0cc0df?style=for-the-badge)](#tier-i--the-orbis-project)
[![Orb Engine](https://img.shields.io/badge/orb%20engine-AGPL--3.0-0cc0df?style=for-the-badge&logo=gnu)](https://github.com/Phantom-Con-Artist/Orb)
[![Ecosystem](https://img.shields.io/badge/ecosystem-product--specific-0cc0df?style=for-the-badge)](#tier-iii--the-orbis-ecosystem)

[![Orbpad](https://img.shields.io/badge/orbpad-v1.0.1--stable-2ea44f?style=flat-square)](https://github.com/Phantom-Con-Artist/Orbpad)
[![Discord](https://img.shields.io/badge/discord-join%20the%20community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/Em2ur4J8PF)
[![GitHub](https://img.shields.io/badge/github-phantom--con--artist-black?style=flat-square&logo=github)](https://github.com/Phantom-Con-Artist)

<br>

**Architecture · Engine · Ecosystem**

</div>

---


<div align="center">

### 🔗 Quick Links

[**Orbis Project**](https://github.com/Phantom-Con-Artist/Orbis) ·
[**Orb Engine**](https://github.com/Phantom-Con-Artist/Orb) ·
[**Orbpad**](https://github.com/Phantom-Con-Artist/Orbpad) ·
[**Discord**](https://discord.gg/Em2ur4J8PF)

</div>

## Branding Asset Map

<div align="center">

| Asset | File | Intended Use |
|---|---|---|
| **Orbis Project Cover** | `docs/orbisprojectcover.png` | README hero / project identity |
| **Orbis Project Logo** | `docs/orbisprojectlogo.png` | Orbis Project branding |
| **Orb Engine Cover** | `docs/orbenginecover.png` | Orb Engine feature/project section |
| **Orb Engine Logo** | `docs/orbenginelogo.png` | Orb Engine identity |
| **Orbpad Icon** | `docs/orb_v256.png` | Orbpad application identity |
| **Orbis Ecosystem Logo** | `docs/orbisecosystemlogo.png` | Ecosystem tier identity |
| **Powered By Orb Engine** | `docs/powered-by-orb-engine.png` | Canonical visual attribution |
| **Orbis Logo** | `docs/orbislogo.png` | General Orbis branding where appropriate |
| **Orbis Project Cover (v2)** | `docs/orbis-project-krono.png` | new Orbis Project hero cover (1600×500) |
| **Orb Engine 2 / Krono Cover** | `docs/orb-engine-krono.png` | Orb.Engine 2 (Krono) cover (1600×500) |
| **Orbis Ecosystem Cover** | `docs/orbisecosystemcover.png` |  Orbis Ecosystem tier cover (1600×500) |

</div>

The README uses repository-relative paths so GitHub renders the assets directly from the
repository's `docs/` directory.

---
## Architecture Documentation

The formal Orbis architecture is maintained in the repository-root
`architecture/` directory, and now spans two generations: the **v1
architecture** and the **Krono architecture** (2nd Gen).

### v1 Architecture

These documents are the **Tier I — The Orbis Project** v1 specifications and
are released under the **MIT License**:

| Specification | Description | License |
|---|---|---|
| [Graph Architecture](architecture/graph.md) | Core graph model, entities, relationships, properties, identity, traversal, and graph semantics | MIT |
| [.entity Specification](architecture/entity.md) | Standalone `.entity` document structure, typed values, validation, and interoperability | MIT |
| [.lore Specification](architecture/lore.md) | Complete `.lore` graph structure, entities, relationships, validation, and graph serialization | MIT |

### Krono Architecture (2nd Gen)

**Krono** is the second-generation architecture implemented by **Orb.Engine
2**. It builds on the v1 graph engine — without turning it into a monolith —
and introduces explicit, first-class models for entities, connected lore,
event-driven evolution, relationship history, and semantic time.

Krono documents are maintained under `architecture/Krono/` and, like the v1
specifications, are **Tier I — The Orbis Project** material released under
the **MIT License**:

| Specification | Model | Description | License |
|---|---|---|---|
| [Krono Architecture](architecture/Krono/ARCHITECTURE.md) | Krono Architecture Model | Defines the architectural boundaries of The Orbis Project: Krono — canonical vs. derived state, the `OrbGraph` boundary, and the relationship-evolution, history, temporal, entity, and event boundaries | MIT |
| [Krono Entity Model](architecture/Krono/ENTITY_MODEL.md) | Krono Entity Model | Expanded `OrbEntity` semantics — identity, name, type, description, properties, tags, and embedded documents, independent of graph membership | MIT |
| [Krono Lore Model](architecture/Krono/LORE_MODEL.md) | Krono Lore Model | Connected-information semantics for `.lore` and `OrbGraph` — relationships as first-class data with their own identity, type, properties, and validity | MIT |
| [Krono Events & Evolution Model](architecture/Krono/EVENTS_AND_EVOLUTION.md) | Krono Event Evolution Model | Explicit state-transition model separating event entities, declarative evolution operations, and the executor that mutates the graph | MIT |
| [Krono Historical State Model](architecture/Krono/HISTORY.md) | Krono History Model | Immutable, append-only relationship history via `OrbRelationshipFact` and `OrbRelationshipHistory`, kept separate from active relationship state | MIT |
| [Krono Temporal Model](architecture/Krono/TEMPORAL_MODEL.md) | Krono Temporal Model | Semantic time system — `OrbTime`, temporal schemas, units, precision, and position definitions, so timelines are never assumed to be wall-clock time | MIT |


These documents define the **architecture and data specifications** that Orb
Engine (v1) and Orb.Engine 2 (Krono) implement.

### Architecture vs. Implementation

```text
Orbis Project
│
├── v1 Architecture
│   ├── Graph Architecture
│   ├── .entity Specification
│   └── .lore Specification
│           │
│           │ MIT
│           ▼
│      Orb Engine
│
└── Krono Architecture (2nd Gen)
    ├── Krono Architecture Model
    ├── Krono Entity Model
    ├── Krono Lore Model
    ├── Krono Event Evolution Model
    ├── Krono History Model
    └── Krono Temporal Model
            │
            │ MIT
            ▼
       Orb.Engine 2
            │
            │ AGPL-3.0
            ▼
     Orbis Ecosystem
```

The MIT-licensed architecture — v1 and Krono alike — may be independently
implemented, extended, modified, or adapted.

The Orb Engine implementation itself, in either generation, remains licensed
under **GNU AGPL-3.0**.

Using the architecture does not require using Orb Engine.

Using Orb Engine requires compliance with its AGPL-3.0 license.

> **Architecture defines Orbis. Orb Engine implements Orbis.**

---

## Table of Contents

- What is Orbis?
- The Three-Tier Architecture
- Architecture Documentation
- Krono Architecture (2nd Gen)
- Orbis Project
- Orb Engine & Future Releases
- Orbis Ecosystem
- Tier I — The Orbis Project
- Tier II — Orb Engine
- Tier III — The Orbis Ecosystem
- Licensing Model
- What Each Tier Allows
- What Each Tier Does Not Allow
- Powered By Orb Engine Policy
- Attribution Requirements
- Product Classification
- Architecture Reimplementation
- Relationship to the .entity Model
- Relationship to the .lore Model
- Graph Architecture
- Data and File Formats
- Orb Engine Compliance
- Ecosystem Compliance
- Branding
- Third-Party Applications
- Forks
- Independent Implementations
- Hosted Services
- Commercial Products
- Closed-Source Products
- Open-Source Products
- Documentation Requirements
- Examples
- Compliance Matrix
- Contributor Guidance
- Long-Term Vision
- Repository Structure
- Current Projects
- Status
- Community

## What is Orbis?

Orbis is a software architecture and ecosystem for structured, connected knowledge.

Orbis treats knowledge as a graph of explicit objects and relationships rather than
as a collection of unrelated pages or flat records.

The original motivation came from worldbuilding.

Characters relate to characters.

Characters belong to organizations.

Organizations control locations.

Locations exist within regions.

Events occur at particular points in time.

Lore changes state over time.

Those relationships are valuable data in their own right.

The Orbis architecture exists to preserve that structure.

Orbis is intentionally broader than worldbuilding.

The same architectural ideas can support research software, knowledge management,
graph analysis, simulation, documentation systems, and other structured-information
applications.

Orbis therefore does not define itself as a single application.

Orbpad is one application.

Orb Engine is one implementation.

The Orbis Project is the architecture.

The Orbis Ecosystem is the family of products built with or around that foundation.

---

## Core Philosophy

Orbis follows several architectural principles.

### Structure Over Flat Storage

Meaningful relationships should survive serialization.

Information should not be reduced to disconnected text merely because a flat file
is easier to implement.

### Relationships Are First-Class

A relationship is not merely text embedded in a note.

It is a structured connection between objects.

### Data Should Outlive Applications

Applications should not become the sole authority over the meaning of a user's data.

An application may provide an experience.

The architecture provides persistent meaning.

### Implementations Are Replaceable

The architecture must be capable of being implemented by software other than Orb Engine.

This is why the architectural tier is MIT licensed.

### The Reference Engine Remains Open

Orb Engine is AGPL-3.0 licensed so that the reference implementation remains free
software and modifications remain available under the terms of that license.

### Products Remain Independent

Applications in the ecosystem may have their own licensing and commercial models,
subject to the licenses of the Orbis components they actually use.

---

## Orbis Project

<div align="center">

<a href="https://github.com/Phantom-Con-Artist/Orbis">
  <img src="docs/orbisprojectcover.png" alt="Orbis Project" width="900">
</a>

<br><br>

<img src="docs/orbis-project-krono.png" alt="Orbis Project — New cover" width="900">


</div>

The Orbis Project is the architecture tier: the graph model, the `.entity`
and `.lore` specifications, and — as of this revision — the Krono
architecture that Orb.Engine 2 implements.

---

## Orb Engine & Future Releases

<div align="center">

<a href="https://github.com/Phantom-Con-Artist/Orb">
  <img src="docs/orbenginecover.png" alt="Orb Engine" width="900">
</a>

<br><br>

<img src="docs/orb-engine-krono.png" alt="Orb.Engine 2 (Krono)" width="900">

</div>

Orb Engine is the reference-implementation tier, licensed **AGPL-3.0**.

---

## Orbis Ecosystem

<div align="center">

<img src="docs/orbisecosystemcover.png" width="900">


</div>

The Orbis Ecosystem is the applications tier — Orbpad and future
product-specific applications built with or around Orb Engine and
Orb.Engine 2.

---

## The Three-Tier Architecture

Orbis is deliberately separated into three tiers.

<div align="center">

<table>
<tr>
<td align="center" width="30%">

<a href="#tier-i--the-orbis-project">
<img src="docs/orbisprojectlogo.png" alt="The Orbis Project" width="96">
</a>

### Tier I

**The Orbis Project**

Architecture & Shared Design

**MIT**

</td>
<td align="center" width="10%">

### ↓

</td>
<td align="center" width="30%">

<a href="https://github.com/Phantom-Con-Artist/Orb">
<img src="docs/orbenginelogo.png" alt="Orb Engine" width="96">
</a>

### Tier II

**Orb Engine**

Reference Implementation

**AGPL-3.0**

</td>
<td align="center" width="10%">

### ↓

</td>
<td align="center" width="30%">

<a href="#tier-iii--the-orbis-ecosystem">
<img src="docs/orbisecosystemlogo.png" alt="The Orbis Ecosystem" width="96">
</a>

### Tier III

**Orbis Ecosystem**

Applications & Products

**Product-Specific**

</td>
</tr>
</table>

</div>

### The Boundary in One Diagram

```text
┌───────────────────────────────────────────────────────────────────────┐
│ TIER I — THE ORBIS PROJECT                                           │
│                                                                       │
│ Graph architecture · .entity · .lore · relationships · specifications │
│                                                                       │
│ LICENSE: MIT                                                          │
└───────────────────────────────────────┬───────────────────────────────┘
                                        │
                                        │ implemented by
                                        ▼
┌───────────────────────────────────────────────────────────────────────┐
│ TIER II — ORB ENGINE                                                  │
│                                                                       │
│ APIs · runtime · graph operations · serialization · storage · queries │
│                                                                       │
│ LICENSE: AGPL-3.0                                                     │
└───────────────────────────────────────┬───────────────────────────────┘
                                        │
                                        │ used by
                                        ▼
┌───────────────────────────────────────────────────────────────────────┐
│ TIER III — THE ORBIS ECOSYSTEM                                       │
│                                                                       │
│ Orbpad · applications · tools · integrations · services · products    │
│                                                                       │
│ LICENSE: PRODUCT-SPECIFIC                                             │
│ ATTRIBUTION: **Powered By Orb Engine** when the policy applies         │
└───────────────────────────────────────────────────────────────────────┘
```

### What Each Tier Actually Is

| Tier | What it contains | License | Primary question |
|---|---|---|---|
| **Tier I** | Graph architecture, `.entity`, `.lore`, relationships, specifications, shared design | **MIT** | *What is the Orbis architecture?* |
| **Tier II** | Orb Engine source code, APIs, runtime systems, implementation details | **AGPL-3.0** | *How is the architecture implemented?* |
| **Tier III** | Applications, services, tools, integrations, products | **Product-specific** | *What can be built with it?* |

### The Critical Rule

**Do not collapse the three tiers into one license.**

The MIT license of Tier I does **not** make Tier II MIT.

The AGPL-3.0 license of Tier II does **not** make Tier I AGPL.

A Tier III product does **not** inherit a universal Orbis license.

Each tier has its own boundary.

---

## Tier I — The Orbis Project

### Definition

The Orbis Project is the graph architecture and shared design on which Orb Engine is built.

It is not merely the GitHub organization.

It is not merely documentation.

It is the architectural body of ideas, specifications, models, conventions,
and design materials that define what an Orbis-compatible system is intended to represent.

### Core Architectural Scope

The Orbis Project particularly covers:

- The graph-oriented architecture.
- The .entity design concept.
- The .lore design concept.
- Structured objects.
- Relationships between objects.
- Relationship semantics.
- Shared conceptual vocabulary.
- Structural conventions.
- Interoperability principles.
- Serialization concepts.
- Architectural rules necessary to preserve meaning.

### The .entity Concept

The .entity model establishes a structured representation for an identifiable object
within the Orbis architecture.

An entity may represent a character, place, organization, artifact, concept, object,
institution, or another domain-specific object.

The specific fields and implementation may evolve.

The architectural concept remains intentionally reusable.

### The .lore Concept

The .lore model represents structured information about relationships, events, states,
claims, or world knowledge in a form intended to remain connected to the graph.

The .lore concept originated in worldbuilding but is intentionally designed as a broader
structured-knowledge mechanism.

### MIT License

The Orbis Project is released under the MIT License.

The purpose of this permissive license is deliberate.

You may:

- Study the architecture.
- Copy architectural material covered by the MIT license.
- Modify it.
- Extend it.
- Adapt it.
- Reimplement it.
- Translate it into another programming language.
- Build a new implementation from it.
- Use it commercially.
- Use it privately.
- Combine it with other software.
- Create proprietary implementations.
- Create open implementations.
- Create alternative file tooling.
- Create alternative graph engines.
- Create competing applications.

The architectural tier is not intended to force downstream implementations to use MIT.

The MIT license applies to the copyrightable materials distributed under that license.

### What Tier I Does Not Require

Using an architectural concept does not by itself require:

- Using Orb Engine.
- Using C#.
- Using the Orb Engine APIs.
- Using the Orb Engine source code.
- Licensing an independent implementation under AGPL-3.0.
- Publishing an independent implementation under MIT.
- Making the product open source.
- Making the application free of charge.
- Using Orbpad.

The architecture is intentionally implementation-independent.

---

## Tier II — Orb Engine

### Definition

Orb Engine is the reference software implementation of the Orbis architecture.

It is the actual software technology that applications can execute, reference, link
against, embed, bundle, extend, or otherwise incorporate.

Orb Engine may provide:

- Entity management.
- Relationship management.
- Graph operations.
- Data models.
- Serialization.
- Parsing.
- Storage.
- Querying.
- Validation.
- APIs.
- Runtime services.
- Supporting infrastructure.

### AGPL-3.0

Orb Engine is licensed under the GNU Affero General Public License, Version 3.

AGPL-3.0 governs the Orb Engine software itself and covered modifications to it.

The AGPL is a copyleft software license.

It grants broad freedoms, but those freedoms come with corresponding obligations when
covered software is conveyed or made available under the circumstances specified by
the license.

The AGPL also contains specific provisions concerning network interaction.

Use of Orb Engine must therefore be evaluated against the actual AGPL-3.0 license text
and the structure of the software being used.

### Tier II Is Not the Same Thing as Tier I

The architecture and implementation are deliberately separated.

You may independently implement the Orbis architecture without copying Orb Engine source.

That independent implementation is governed by its own license, subject to the materials
from which it was actually derived.

By contrast, if you use Orb Engine code, the Orb Engine code remains governed by AGPL-3.0.

### Core Rule

**The MIT license of the Orbis Project does not convert Orb Engine into MIT software.**

**The AGPL-3.0 license of Orb Engine does not convert the architectural specification
into AGPL-3.0 software.**

Each tier retains its own licensing boundary.

---

## Tier III — The Orbis Ecosystem

### Definition

The Orbis Ecosystem is the collection of applications, products, services, tools,
integrations, libraries, visualizers, experiments, and other software built with
or around Orbis technology.

The ecosystem is product-specific.

There is no single mandatory application license for the entire ecosystem.

A product can have its own:

- License.
- Business model.
- User interface.
- Distribution model.
- Pricing model.
- Hosting model.
- Product name.
- Brand.
- Feature set.
- Target audience.

Subject to the licenses of components it uses.

### Examples

An ecosystem product may be:

- An MIT application.
- An Apache-2.0 application.
- A GPL application.
- An AGPL application.
- Another compatible open-source model.
- A proprietary product, where legally compatible with the components used.

The individual product license does not replace the licenses of incorporated Orbis components.

### The Ecosystem Is Not a License

The term 'Orbis Ecosystem' is a classification.

It does not automatically grant permission to relicense Orb Engine.

It does not replace AGPL-3.0.

It does not turn MIT architectural materials into proprietary material.

It does not create a universal license for third-party products.

---

## Three-Tier Permission Model

The easiest way to understand Orbis is to think in terms of what you are taking.

### Taking the Architecture

If you take the Orbis architectural design and implement it yourself without copying
copyrightable Orb Engine source code, the architectural materials are available under MIT
where the relevant material is distributed under that license.

### Taking the Engine

If you take Orb Engine code, you are taking AGPL-licensed software.

The AGPL obligations associated with that software apply according to the license.

### Taking an Ecosystem Product

If you take an existing ecosystem application, you must comply with that application's
license as well as the licenses of its dependencies.

---

## What Each Tier Allows

### Tier I — The Orbis Project — Allowed

Allowed under the MIT license, subject to its terms:

- Copying covered architectural materials.
- Modifying covered architectural materials.
- Adapting the architectural concepts.
- Creating a new implementation.
- Creating a competing implementation.
- Creating a proprietary implementation.
- Creating an open-source implementation.
- Commercial use.
- Private use.
- Distribution.
- Modification.
- Integration.
- Research.
- Education.
- Forking architectural documentation.

### Tier I — Not Automatically Granted

The MIT license does not automatically grant:

- Trademark rights.
- Rights to misrepresent authorship.
- Rights over materials not actually included under MIT.
- Rights over third-party components.
- Rights over patents beyond what the applicable license provides.

### Tier II — Orb Engine — Allowed

AGPL-3.0 grants rights subject to its conditions to:

- Run the covered software.
- Study the covered software.
- Modify the covered software.
- Share copies under the license.
- Build covered modifications under the license.
- Deploy covered software under the license.

### Tier II — Orb Engine — Not Allowed

You may not treat AGPL-covered Orb Engine code as though it were MIT code.

You may not remove the AGPL obligations from covered software merely by declaring your
application to be proprietary.

You may not impose additional restrictions that contradict the AGPL.

You may not claim that the entire Orb Engine codebase is MIT licensed.

You may not replace the Orb Engine license text with your own license.

You may not distribute a modified covered version while falsely claiming that it is
an unrelated proprietary implementation.

### Tier III — Ecosystem — Allowed

An ecosystem product may choose its own product license where that choice is compatible
with the licenses of the Orbis components it uses.

A product may be:

- Commercial.
- Free of charge.
- Subscription-based.
- Open source.
- Source-available.
- Internal.
- Hosted.
- Desktop.
- Mobile.
- Web-based.
- Command-line.
- Embedded.

Subject to all applicable component licenses.

---

## What Each Tier Does Not Allow

### The Orbis Project

Does not automatically grant ownership of Orb Engine.

Does not grant permission to copy Orb Engine source under MIT.

Does not grant permission to use Orbis trademarks without authorization.

Does not eliminate third-party component licenses.

### Orb Engine

Does not grant permission to ignore AGPL-3.0.

Does not grant permission to impose downstream restrictions inconsistent with AGPL-3.0.

Does not give ownership of Orbis trademarks merely because code is used.

### Orbis Ecosystem

Does not mean every product is open source.

Does not mean every product is proprietary.

Does not mean every product is AGPL.

Does not mean every product is MIT.

Does not mean an ecosystem product owns Orb Engine.

Does not replace a product's own license.

---

## Orbis Ecosystem Attribution Badge

<div align="center">

<a href="https://github.com/Phantom-Con-Artist/Orb">
  <img src="docs/powered-by-orb-engine.png" alt="Powered By Orb Engine" width="720">
</a>

<br>

**Powered By Orb Engine**

<br>

[![Orb Engine](https://img.shields.io/badge/Orb%20Engine-AGPL--3.0-0cc0df?style=flat-square&logo=gnu)](https://github.com/Phantom-Con-Artist/Orb)

</div>

The phrase above is the canonical attribution.

For ecosystem products using Orb Engine, the phrase should appear as written:

> **Powered By Orb Engine**

The visual artwork in `docs/powered-by-orb-engine.png` may be used as the canonical
visual attribution. A product may also use a badge or other approved visual treatment.

The visual artwork or badge does not replace the exact textual attribution where the policy
requires the phrase itself to be presented.

Recommended repository-local artwork:

```html
<a href="https://github.com/Phantom-Con-Artist/Orb">
  <img src="docs/powered-by-orb-engine.png"
       alt="Powered By Orb Engine"
       width="720">
</a>
```

Recommended Markdown badge:

```md
[![Powered By Orb Engine](https://img.shields.io/badge/Powered%20By-Orb%20Engine-0cc0df?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Phantom-Con-Artist/Orb)
```

Recommended HTML badge:

```html
<a href="https://github.com/Phantom-Con-Artist/Orb">
  <img
    src="https://img.shields.io/badge/Powered%20By-Orb%20Engine-0cc0df?style=for-the-badge&logo=github&logoColor=white"
    alt="Powered By Orb Engine">
</a>
```

---

## Powered By Orb Engine Policy

### Purpose

The phrase **Powered By Orb Engine** identifies software that relies on Orb Engine.

It is intended to provide users with clear provenance information.

It also establishes a visible relationship between an ecosystem product and the engine
that provides its Orbis functionality.

### The Required Attribution

The exact attribution phrase is:

> **Powered By Orb Engine**

The wording must not be replaced with:

- 'Made with Orb Engine'.
- 'Uses Orbis'.
- 'Built on Orbis'.
- 'Powered by Orbis'.
- 'Orb Engine inside'.
- 'Based on Orb'.

When the policy requires the attribution, the exact phrase **Powered By Orb Engine**
must appear.

### No Creative Rewording

Products must not satisfy the policy solely by using a substantially different phrase.

The required phrase is an explicit identifier.

### Branding Versus Software License

This requirement is intentionally separated from AGPL-3.0.

AGPL-3.0 governs the copyright license of Orb Engine.

The Powered By Orb Engine requirement is an Orbis ecosystem and branding policy.

This distinction is essential because the AGPL does not become a vehicle for adding
arbitrary restrictions to the software license.

GNU's GPLv3 guidance explains that further restrictions on the exercise of rights under
the license are not generally permitted, while trademark and attribution-related matters
can be handled separately. citeturn166872search22turn166872search26

### Ecosystem Recognition

An application may describe itself as an **Orbis Ecosystem product** only if it complies
with the ecosystem attribution policy applicable to that product.

A product that does not wish to use the ecosystem designation may operate under the
licenses applicable to the software it uses, but it must not falsely claim official
Orbis Ecosystem status.

### Required Placement

The attribution must be displayed in a place reasonably visible to the relevant audience
for the medium in which the product is delivered.

For a graphical application, the preferred locations include:

- About screen.
- Application information dialog.
- Credits screen.
- Settings or legal information screen.
- Startup or splash screen where practical.

For a web product:

- Footer.
- About page.
- Legal page.
- Product information page.

For a command-line product:

- Help output.
- Version output.
- Startup information.
- Documentation.

For a library:

- Package documentation.
- README.
- API documentation.
- Package metadata where practical.

For a hosted service:

- Product information page.
- About page.
- Documentation.
- Legal or credits page.

For a distribution package:

- Package documentation.
- Product README.
- Installer or distribution information where practical.

### Ubiquitous Attribution Principle

The intent is not to force an unreadable phrase into every pixel of an application.

The intent is that a user, developer, distributor, or evaluator encountering the product
in its normal form can reasonably discover that it is Powered By Orb Engine.

The phrase should not be hidden solely to technically claim compliance.

A collapsed legal menu, buried source comment, or inaccessible internal file should not
be treated as the preferred presentation when a user-facing attribution location exists.

### Multiple Mediums

If the same product is distributed through multiple materially different mediums, the
attribution should be maintained across those mediums.

Examples:

- Desktop build.
- Web build.
- CLI distribution.
- Documentation site.
- Package registry.
- Repository.
- Installer.

The principle is consistency.

### Exact Phrase

**Powered By Orb Engine**

Capitalization should be preserved.

The wording should remain intact.

Additional explanatory text may be placed around the phrase.

Example:

> This application is Powered By Orb Engine.

Example:

> Powered By Orb Engine — see the Orb Engine project for licensing and source information.

### Attribution Is Not Ownership

Displaying the phrase does not mean Orbis owns the product.

It means the product acknowledges the engine used by the product.

### Attribution Is Not Endorsement

Unless separately authorized, displaying the required attribution does not mean that
the Orbis Project endorses, certifies, audits, or guarantees a third-party product.

### No False Affiliation

A product must not claim to be an official Orbis application merely because it displays
the attribution.

Official status must be separately granted.

---

## When the Powered By Orb Engine Phrase Applies

The ecosystem policy is intentionally broad.

A product is considered to use Orb Engine when it:

- Links directly to Orb Engine.
- Embeds Orb Engine.
- Bundles Orb Engine.
- Distributes Orb Engine with the product.
- Includes Orb Engine as a runtime dependency.
- Loads Orb Engine as a plugin or module.
- Uses Orb Engine APIs.
- Uses Orb Engine assemblies.
- Uses modified Orb Engine code.
- Uses an internal fork of Orb Engine.
- Hosts an Orb Engine-powered service.
- Uses Orb Engine as a backend component.
- Uses Orb Engine to read or write Orbis structures as part of its product functionality.

The attribution policy also applies where a product presents itself as an Orbis Ecosystem
application and uses Orb Engine as part of that product's operation.

### What Does Not Count as Engine Use

Merely discussing Orb Engine does not make a product an engine-dependent product.

Examples:

- A blog post about Orb Engine.
- A tutorial describing Orbis concepts.
- A paper citing the architecture.
- A toy reimplementation that does not include Orb Engine code.
- A standalone implementation inspired by the MIT architecture.

However, trademark and ecosystem-branding rules may still apply if the author presents
the work as an official Orbis product.

---

## Architecture Reimplementation

One of the most important properties of Tier I is that it is reusable.

A developer may implement the architectural ideas in another language.

Examples:

- Rust.
- Go.
- Java.
- TypeScript.
- Python.
- C++.
- Swift.
- Kotlin.

A new implementation can use the Orbis architecture under the MIT license covering the
relevant architectural materials.

The developer does not have to use Orb Engine.

The developer does not automatically inherit AGPL merely because the implementation follows
the same architectural concepts.

### Important Boundary

**Architecture is not source code.**

**A concept is not automatically a copied implementation.**

**An independent implementation must still avoid copying copyrightable source material
when it is not licensed for that use.**

### Independent Implementations

Independent implementations are welcome.

They may be:

- Open source.
- Commercial.
- Proprietary.
- Academic.
- Experimental.

They should accurately describe whether they are compatible with the Orbis architecture and
whether they use Orb Engine.

---

## Independent Reimplementation and Reverse Engineering

The Orbis Project explicitly permits independent implementations of the Orbis architecture.

The purpose of the Orbis Project is to make its architectural concepts, document structures, graph model, and associated specifications available for experimentation, implementation, interoperability, modification, and extension under the MIT License.

You may study the public Orbis architecture and specifications, inspect and analyze `.entity` and `.lore` documents, observe the externally visible behavior of Orbis-compatible data, and independently implement the architectural concepts and documented semantics described by the Orbis Project.

This permission expressly includes the creation of independent and compatible implementations of the Orbis graph architecture, `.entity` format, `.lore` format, entity model, relationship model, property model, typed-value model, validation rules, serialization behavior, and other architectural concepts described in the MIT-licensed Orbis Project specifications.

### Independent Engine Implementations

You may create your own implementation of the Orbis architecture.

This may include:

- A completely new Orbis-compatible engine.
- A reimplementation written in another programming language.
- A different internal architecture providing equivalent documented behavior.
- A different graph-processing implementation.
- A different storage or database implementation.
- A different parser or serializer.
- A different query system.
- A compatibility layer.
- A translation or migration system.
- A competing implementation of the Orbis architecture.
- A commercial implementation.
- A proprietary implementation.
- An open-source implementation.

You are not required to use Orb Engine.

You are not required to depend on Orb Engine.

You are not required to reproduce Orb Engine source code.

You are not required to reproduce the internal class structure, private APIs, internal algorithms, or other implementation-specific details of Orb Engine.

You are not required to publish an independent implementation under AGPL-3.0 merely because it implements the Orbis architecture.

An independently created implementation may use its own license, including an open-source, source-available, or proprietary license, provided that the implementation does not incorporate material whose separate license requires otherwise.

### Reverse Engineering for Independent Compatibility

The Orbis Project permits independent reverse engineering performed for the purpose of understanding, reproducing, testing, implementing, or achieving compatibility with the Orbis architecture and its publicly described or externally observable behavior.

This may include:

- Analyzing `.entity` files.
- Analyzing `.lore` files.
- Examining serialized graph structures.
- Observing externally visible behavior.
- Testing interoperability.
- Determining data-model semantics.
- Determining relationship semantics.
- Determining property semantics.
- Reproducing documented validation behavior.
- Reproducing documented serialization behavior.
- Building black-box compatible implementations.
- Creating alternative implementations based on observed behavior.
- Creating independent parsers, serializers, graph engines, and applications.

The purpose of this permission is to allow independent implementation, interoperability, experimentation, and competition.

Any reverse engineering activity remains subject to applicable laws and regulations in the jurisdiction in which it is performed.

### No Requirement to Reproduce Orb Engine Internals

Independent implementations are not required to reproduce the internal source code, private architecture, private APIs, internal class structures, internal algorithms, or other implementation-specific details of Orb Engine.

A compatible implementation may achieve equivalent documented or observable behavior through completely different internal code, algorithms, data structures, or architectural decisions.

### Architecture Is Not Orb Engine Source Code

The Orbis Project architecture and the Orb Engine implementation are separate layers.

The Orbis Project architecture, including the graph architecture, `.entity` model, `.lore` model, relationships, properties, and other materials distributed as part of the Tier I specification, is licensed under the MIT License.

Orb Engine is the reference implementation of that architecture and is separately licensed under GNU AGPL-3.0.

The MIT license of the Orbis Project does not relicense Orb Engine source code.

The AGPL-3.0 license of Orb Engine does not impose AGPL-3.0 on an independent implementation merely because that implementation follows the Orbis architecture.

### You May Build Your Own Engine

You are explicitly free to build your own engine based on the Orbis architecture.

You may:

- Implement `.entity` yourself.
- Implement `.lore` yourself.
- Implement the graph model yourself.
- Implement relationship handling yourself.
- Implement property handling yourself.
- Implement typed values yourself.
- Implement validation yourself.
- Implement serialization yourself.
- Implement querying yourself.
- Implement storage yourself.
- Extend the architecture.
- Modify the architecture.
- Create domain-specific extensions.
- Create a competing implementation.
- Commercialize the implementation.
- Keep the implementation proprietary.
- Release the implementation as open source.

You may build an implementation that provides equivalent or compatible functionality to Orb Engine without using Orb Engine source code.

### No Competition Restriction

The Orbis Project does not prohibit competition.

You may create:

- A competing graph engine.
- A competing Orbis-compatible engine.
- A competing `.entity` implementation.
- A competing `.lore` implementation.
- A competing knowledge-management application.
- A competing worldbuilding application.
- A competing commercial product.
- A competing proprietary product.

The existence of Orb Engine or Orbpad does not prevent independent developers from creating alternatives.

### No Requirement to Use Orb Engine

Implementing the Orbis architecture does not require the use of Orb Engine.

A developer may implement the architecture independently and distribute that implementation under a separate license, subject to the actual materials used and their applicable licenses.

An independent implementation does not become Orb Engine merely because it implements the same architecture.

### Powered By Orb Engine Boundary

An independent implementation that does not use Orb Engine is not required to display the `Powered By Orb Engine` attribution.

The `Powered By Orb Engine` attribution applies to products that actually use, incorporate, depend upon, embed, bundle, link to, host, or otherwise operate using Orb Engine, in accordance with the Orbis Ecosystem attribution policy.

Implementing the Orbis architecture independently does not by itself create an obligation to display that attribution.

### Important Boundary

This permission applies to the MIT-licensed Orbis Project architecture and specifications.

It does not grant permission to copy, incorporate, redistribute, or relicense Orb Engine source code as though it were MIT licensed.

Orb Engine source code remains governed by GNU AGPL-3.0.

Accordingly:

**You may study the architecture.**

**You may study and analyze `.entity` and `.lore`.**

**You may inspect serialized graph structures.**

**You may observe externally visible behavior.**

**You may reverse engineer for independent compatibility where permitted by applicable law.**

**You may implement your own engine.**

**You may create a proprietary engine.**

**You may create a competing engine.**

**You may modify or extend the architecture.**

**You may commercially distribute your independent implementation.**

**You may create an implementation that is compatible with Orbis.**

**You may implement `.entity` and `.lore` without using Orb Engine.**

**You may not take Orb Engine's AGPL-licensed implementation and relicense it as MIT.**

### The Principle

The Orbis Project intentionally separates architectural freedom from implementation licensing.

Understand the architecture.

Study the formats.

Reimplement it.

Improve it.

Extend it.

Compete with it.

Build something entirely new from it.

Just do not misrepresent Orb Engine's AGPL-licensed implementation as MIT-licensed material.

---

## The .entity Architecture

The .entity format and model are among the foundational architectural concepts of Orbis.

The .entity model is intended to represent structured entities in a graph-oriented system.

### Permitted Use

You may create:

- Your own .entity parser.
- Your own .entity writer.
- Your own .entity editor.
- Your own .entity database.
- Your own .entity-compatible application.
- Your own alternative implementation.

Subject to the license of the actual architectural material used.

### Modification

You may alter the design.

You may add fields.

You may remove fields.

You may extend semantics.

You may create domain-specific extensions.

You may reinterpret implementation details.

The goal is to permit experimentation.

### Compatibility

Compatibility should be documented honestly.

If your implementation intentionally diverges from the specification, document the divergence.

---

## The .lore Architecture

The .lore model is another core architectural concept.

It provides a structured way to represent connected lore and related information.

The design may support:

- Claims.
- States.
- Events.
- Relationships.
- Temporal context.
- Structured descriptions.
- Domain-specific metadata.

The precise implementation belongs to the implementation tier when implemented in Orb Engine.

The architectural model belongs to the Orbis Project when distributed as architectural material.

### Freedom to Experiment

Developers may create alternative .lore systems.

Developers may add capabilities.

Developers may build domain-specific variants.

Developers may create competing applications.

Developers may create tools that translate between .lore and other representations.

---

## Graph Architecture

Orbis is fundamentally graph-oriented.

Objects are nodes.

Relationships are explicit edges.

Structured information can be attached to those objects and relationships.

This makes the architecture suitable for knowledge whose meaning depends on connection.

### Why the Graph Matters

A flat note can say:

> Alice belongs to the House of North.

A graph can represent:

```text
Alice ──memberOf──> House of North
House of North ──controls──> Northhold
Northhold ──locatedIn──> Northern March
```

The relationship itself is data.

This architectural decision is one of the defining characteristics of Orbis.

### Relationship Semantics

Relationship types can be:

- Domain-specific.
- Temporal.
- Directional.
- Annotated.
- Queryable.
- Versioned.
- Context-dependent.

Exact semantics belong to the specification and implementation layers as appropriate.

---

## Data Ownership and Application Independence

Orbis is designed around user-owned knowledge.

A product should not be the only thing capable of interpreting the user's graph.

This is why stable structures and explicit relationships matter.

### Application Independence

Orbpad is an application.

Another product can interpret the same architecture.

A research application may read the same entity structures.

A graph visualizer may display the same relationships.

A command-line tool may manipulate them.

The value of the architecture grows when knowledge survives individual applications.

---

<div align="center">

[![Orbis Project License](https://img.shields.io/badge/Orbis%20Project-MIT-0cc0df?style=for-the-badge)](#tier-i--the-orbis-project)
[![Orb Engine License](https://img.shields.io/badge/Orb%20Engine-AGPL--3.0-0cc0df?style=for-the-badge)](https://github.com/Phantom-Con-Artist/Orb)
[![Ecosystem License](https://img.shields.io/badge/Ecosystem-Product--Specific-0cc0df?style=for-the-badge)](#tier-iii--the-orbis-ecosystem)

</div>

## Licensing Model

### Tier I

**The Orbis Project — MIT License.**

The architectural materials distributed under MIT may be reused under the terms of MIT.

### Tier II

**Orb Engine — GNU AGPL-3.0.**

The implementation is governed by AGPL-3.0.

### Tier III

**Orbis Ecosystem — Product-Specific.**

Each product has its own license and compliance requirements.

### Dependency Principle

A product's own license does not erase the license of a component it incorporates.

Likewise, using an MIT architectural concept does not automatically impose the license
of an implementation that happens to share that architecture.

---

## Licensing Decision Tree

Use the following decision process.

### Question 1

Did you copy or incorporate Orb Engine source code?

If yes, inspect AGPL-3.0 obligations.

If no, continue.

### Question 2

Did you copy architectural materials distributed under the Orbis Project MIT license?

If yes, comply with MIT.

If no, continue.

### Question 3

Are you simply implementing the architecture independently?

If yes, the implementation may have its own license.

### Question 4

Are you claiming the product is part of the Orbis Ecosystem?

If yes, comply with applicable ecosystem branding and attribution policies.

### Question 5

Does the product use Orb Engine?

If yes, the Powered By Orb Engine attribution policy applies to ecosystem products
as described in this document.

---

## Compliance Matrix

| Action | Tier I | Tier II | Tier III |
|---|---|---|---|
| Study architecture | Allowed | Allowed | Depends on product license |
| Reimplement architecture | Allowed | N/A | Allowed subject to components |
| Modify architectural materials | Allowed | N/A | Depends on source |
| Copy Orb Engine source | N/A | AGPL-3.0 | AGPL-3.0 applies |
| Modify Orb Engine source | N/A | AGPL-3.0 | AGPL-3.0 applies |
| Make proprietary architecture implementation | Allowed | N/A | Depends on components |
| Make proprietary product using only independent implementation | Generally allowed | N/A | Product-specific |
| Use Orb Engine in proprietary product | See AGPL-3.0 | AGPL-3.0 | Requires AGPL compliance |
| Use .entity concept independently | Allowed | N/A | Allowed |
| Use .lore concept independently | Allowed | N/A | Allowed |
| Use Orb Engine branding | Separate policy | Separate policy | Requires compliance |
| Claim official endorsement | Not automatic | Not automatic | Not automatic |
| Display Powered By Orb Engine | N/A | Recommended where appropriate | Required for ecosystem products using engine |

---

## What a Product Using Orb Engine Must Do

A product using Orb Engine must first comply with AGPL-3.0.

Then, where the product is participating in the Orbis Ecosystem or presenting itself under
Orbis ecosystem branding, it must comply with the ecosystem attribution policy.

The product should:

1. Preserve required license notices.
2. Provide the source and corresponding-source information required by AGPL-3.0 where applicable.
3. Preserve applicable copyright notices.
4. Preserve applicable third-party notices.
5. Display **Powered By Orb Engine** in the practical user-facing or distribution-facing
location appropriate to the product.
6. Avoid implying official endorsement unless separately authorized.
7. Identify significant modifications where required by the applicable licenses.
8. Provide accurate dependency and license information.

---

## Hosted and Network Services

Orb Engine is AGPL-3.0 licensed.

The AGPL contains provisions addressing modified versions interacted with over a network.

Therefore, a hosted product using a modified Orb Engine must carefully evaluate the network
source-offer obligations under AGPL-3.0.

GNU describes the AGPL as specifically strengthening copyleft for software used interactively
over a network. citeturn166872search23

The ecosystem branding requirement is separate.

A hosted product that uses Orb Engine as part of its product should identify the engine clearly
and display **Powered By Orb Engine** in an accessible product-facing location.

### SaaS

A SaaS product does not become exempt from the AGPL merely because users do not download
the product.

The exact obligations depend on how Orb Engine is used and modified.

The authoritative source is the AGPL-3.0 license text.

---

## Commercial Products

Commercial use is compatible with the MIT license.

Commercial use is also possible under AGPL-3.0, provided the AGPL terms are followed.

Commercial software may charge:

- Subscription fees.
- License fees for separate proprietary components.
- Support fees.
- Hosting fees.
- Consulting fees.
- Other lawful commercial charges.

The presence of commercial activity does not itself eliminate the open-source license
obligations of covered components.

### Proprietary Ecosystem Products

A proprietary product may exist in the ecosystem where its composition and dependencies
permit that licensing model.

If it incorporates Orb Engine in a way governed by AGPL-3.0, the proprietary product must
not simply assume that the entire combined work can be relicensed as proprietary.

The precise legal analysis depends on the software structure and applicable law.

---

## Closed-Source Products

The ecosystem does not automatically ban closed-source software.

The distinction is between:

1. An independent implementation of the MIT-licensed architecture.
2. A product incorporating AGPL-licensed Orb Engine code.

The first may have a proprietary license.

The second must comply with AGPL-3.0 for the covered software.

---

## Open-Source Products

Open-source applications are welcome.

They may use:

- MIT.
- Apache-2.0.
- GPL-compatible licenses.
- AGPL.
- Other appropriate licenses.

Compatibility must be checked at the component level.

---

## Forks

### Orb Engine Fork

A fork of Orb Engine is still based on AGPL-licensed software.

Fork authors must follow AGPL-3.0.

Fork authors may create their own project identity.

They may not automatically claim that the fork is an official Orbis Project release.

They should clearly distinguish their fork from upstream Orb Engine.

### Architectural Fork

A fork of architectural documentation or design material distributed under MIT may
be modified under the terms of MIT.

Independent implementations remain free to choose their own license.

---

## Third-Party Applications

Third-party developers are welcome to build around Orbis.

They may create:

- Knowledge-management applications.
- Worldbuilding software.
- Graph databases.
- Graph visualization tools.
- Research tools.
- Data editors.
- Import/export utilities.
- Command-line applications.
- APIs.
- Server applications.
- Data migration tools.
- Educational applications.
- Simulation environments.

Third-party applications should clearly identify their relationship with Orb Engine.

Where the ecosystem policy applies, they must use the exact attribution:

> **Powered By Orb Engine**

---

## Official Versus Third-Party

Not every ecosystem product is official.

### Official Product

An official product is separately designated by the Orbis Project.

### Community Product

A community product is independently developed and may participate in the ecosystem
without being an official first-party application.

### Third-Party Product

A third-party product is developed outside the direct Orbis Project development effort.

Using the engine does not make a company part of the Orbis organization.

---

## Branding Rules

Software licenses and trademarks are different systems.

The MIT license does not automatically grant trademark rights.

The AGPL does not automatically grant permission to imply endorsement.

### Name Usage

Developers should accurately distinguish:

- Orbis Project.
- Orb Engine.
- Orbis Ecosystem.
- Orbpad.

### No Misrepresentation

An independent product must not state or imply that it is officially maintained by
the Orbis Project unless that statement is true.

### Required Attribution

Where the ecosystem attribution policy applies:

> **Powered By Orb Engine**

must be presented clearly.

---

## Attribution Examples

### Desktop Application

```text
About

Powered By Orb Engine
Orb Engine is licensed under AGPL-3.0.
```

### Web Application

```text
© 2026 Example Product
Powered By Orb Engine
```

### CLI

```text
Example Tool 2.0
Powered By Orb Engine
License information: --license
```

### Documentation

```text
Architecture and graph features powered by Orb Engine.
Powered By Orb Engine
```

### Package

```text
Example Product
Powered By Orb Engine
See THIRD-PARTY-NOTICES for license information.
```

---

## Attribution Anti-Patterns

The following should not be treated as sufficient where the exact phrase is required:

```text
Built on Orbis
```

```text
Powered by Orbis```

```text
Uses Orb```

```text
Engine: Orb```

```text
Orbis compatible```

These may be useful supplemental descriptions.

They do not replace:

> **Powered By Orb Engine**

---

## Hidden Attribution

Putting the phrase only in an obscure internal source file while leaving a normal user
interface with no visible attribution is discouraged and should not be treated as the
preferred compliance method where a practical user-facing location exists.

The objective of the policy is actual provenance.

Users should be able to understand what technology powers the product.

---

## Product License Notices

Every ecosystem product should maintain its own LICENSE or clearly equivalent licensing
documentation.

The product documentation should distinguish:

- The product's own license.
- Orb Engine's AGPL-3.0 license.
- Orbis Project architectural materials under MIT, if used.
- Other third-party licenses.

This makes the dependency boundary obvious.

---

## Documentation Requirements

A mature ecosystem should make licensing easy to understand.

A recommended product documentation section is:

```text
## Orbis / Orb Engine

This product is Powered By Orb Engine.

Orb Engine is licensed under the GNU Affero General Public License, Version 3.

See the Orb Engine repository and license for the complete terms.
```

If architectural materials are also used:

```text
The Orbis architectural materials used by this project are distributed
under the MIT License where identified as such.
```

---

## Repository Requirements

An Orb Engine repository should include:

- LICENSE.
- Appropriate source notices.
- Dependency notices.
- README licensing information.
- Build instructions.
- Source availability information where required.

An Orbis Project architecture repository should identify the MIT license clearly.

An ecosystem application repository should identify its own license and dependencies.

---

## Recommended Application README

An ecosystem application can use wording similar to:

```text
## Licensing

This application is licensed under [PRODUCT LICENSE].

This product uses Orb Engine.
Powered By Orb Engine.

Orb Engine is licensed under the GNU Affero General Public License, Version 3.

The Orbis Project architecture is licensed under the MIT License where applicable.

See the corresponding license files for the complete legal terms.
```

---

## Architectural Compatibility

Not every application must implement every Orbis concept.

An application may support a subset.

An application may implement extensions.

An application may define additional relationships.

However, compatibility claims should be honest.

### Compatible

Use this when the product can meaningfully exchange or interpret data according to the
documented compatibility target.

### Inspired By

Use this when the product uses ideas but intentionally does not claim compatibility.

### Powered By Orb Engine

Use this when the product actually relies on Orb Engine.

---

## Versioning

Orbis architecture and Orb Engine versions are not automatically the same thing.

An architectural specification can evolve separately from the implementation.

An engine release can implement an earlier or newer architectural revision.

Products should document the versions they support.

### Example

```text
Product: Example Graph Studio
Orb Engine: 1.2.x
Orbis Architecture: Entity/Lore revision 2
Product License: MIT
Attribution: Powered By Orb Engine
```

---

## Backward Compatibility

Knowledge systems benefit from durable formats.

Orbis aims to preserve compatibility where practical.

Breaking changes should be documented.

Migration paths should be explicit.

Applications should avoid silently corrupting unknown data.

---

## Serialization

Serialization is part of the implementation layer when provided by Orb Engine.

Serialization concepts and formats may also be described as part of the architecture.

The license of the actual serialized format specification must be checked independently
from the license of the implementation that reads or writes it.

---

## Interoperability

Interoperability is a central purpose of Orbis.

Different applications should be able to understand shared structures.

This does not require every application to share source code.

It requires a sufficiently stable conceptual and structural language.

---

## Data Portability

Users should be able to export their structured knowledge.

An application should not intentionally make the underlying graph impossible to recover.

Long-term portability is part of the Orbis philosophy.

---

## Security

Applications using Orb Engine are responsible for securing how they expose the engine.

Hosted deployments should consider:

- Authentication.
- Authorization.
- Data isolation.
- Input validation.
- Dependency management.
- Network security.
- Resource limits.
- Backup and recovery.

Orb Engine's license does not itself constitute a security guarantee.

---

## Performance

Performance characteristics belong to implementation.

The architecture defines meaning.

The engine chooses algorithms.

Applications choose user experience.

This separation allows optimized implementations without changing the conceptual model.

---

## Extensibility

Orbis is intentionally extensible.

Applications can add domain-specific concepts.

Examples:

- Medical research entities.
- Academic publications.
- Fictional characters.
- Legal entities.
- Manufacturing assets.
- Software components.
- Historical events.

The graph remains the common foundation.

---

## Domain Independence

Worldbuilding was the origin.

It is not the boundary.

Orbis should be capable of modeling both fictional and real structured knowledge.

That is why the architecture avoids defining the graph entirely in terms of fiction.

---

## What Orbis Is Not

Orbis is not:

- A single application.
- A closed platform.
- A proprietary-only file format.
- A requirement to use Orbpad.
- A requirement to use a single programming language.
- A universal product license.
- An automatic endorsement program.

---

## Relationship Between Orbpad and Orbis

Orbpad is a first-party application built within the ecosystem.

Orbpad demonstrates the architecture in practical use.

Orbpad does not define the entire ecosystem.

Future applications may use the same engine.

Alternative applications may use the same architecture.

---

## Orbpad Licensing Boundary

Orbpad has its own product license.

Orb Engine remains AGPL-3.0 licensed.

Orbpad should not describe the entire combined distribution as simply 'MIT' without
clearly separating the product's own license from the engine's license.

Orbpad should display:

> **Powered By Orb Engine**

because it uses the engine.

---

## Contributor Guidance

Contributors may work on different parts of Orbis.

### Architecture Contributors

Work on:

- Specifications.
- Graph semantics.
- .entity.
- .lore.
- Compatibility.
- Documentation.

### Engine Contributors

Work on:

- APIs.
- Storage.
- Serialization.
- Querying.
- Runtime behavior.
- Performance.

### Ecosystem Contributors

Work on:

- Applications.
- Integrations.
- Tooling.
- Visualizations.
- User experiences.

---

## Contribution Does Not Mean Ownership

Contributing to an ecosystem product does not automatically make the contributor an
owner of Orb Engine or the Orbis Project as a whole.

Each repository must define its contribution and copyright policies.

---

## Governance

The architecture may evolve through discussion, implementation experience, compatibility
requirements, and documented proposals.

Changes should be deliberate where they affect interoperability.

---

## Proposed Architectural Changes

A proposed change should identify:

- The problem.
- The current behavior.
- The proposed behavior.
- Compatibility impact.
- Migration impact.
- Serialization impact.
- Relationship impact.
- Implementation impact.

This creates a paper trail for decisions.

---

## Specification Versus Implementation

A specification describes intended meaning.

An implementation describes executable behavior.

These are related but not identical.

One specification can have multiple implementations.

One implementation can support multiple specifications.

This is a core reason for the three-tier architecture.

---

## Legal Boundary Summary

Keep this simple:

**Architecture:** MIT.

**Engine:** AGPL-3.0.

**Products:** their own license, subject to dependencies.

**Engine attribution for ecosystem products:** Powered By Orb Engine.

**Trademark / branding:** separate from software copyright licensing.

**AGPL compliance:** mandatory for uses governed by AGPL-3.0.

---

## Practical Do / Don't Table

| Do | Don't |
|---|---|
| Implement the architecture independently | Claim the architecture is proprietary |
| Read and follow AGPL-3.0 for Orb Engine | Treat Orb Engine as MIT |
| Display Powered By Orb Engine when required | Hide the attribution in an obscure location |
| Use your own product license | Claim your license overrides dependencies |
| Clearly distinguish official products | Imply endorsement without authorization |
| Preserve license notices | Remove required notices |
| Document modifications | Misrepresent modified engine code as upstream |
| Build competing products | Assume competition is prohibited |

---

## Examples of Valid Architectures

### Example A — Independent Implementation

Developer A studies the MIT-licensed architecture and writes a new Rust engine from scratch.

The new implementation does not copy Orb Engine source.

Developer A releases it under a proprietary license.

This is conceptually compatible with Tier I because the architecture is permissively licensed,
subject to the actual materials and legal facts involved.

### Example B — Orb Engine Application

Developer B links an application against Orb Engine.

The application must comply with AGPL-3.0 as applicable to the combined software and deployment.

The application displays:

> Powered By Orb Engine

where the ecosystem attribution policy applies.

### Example C — Hosted Service

Developer C modifies Orb Engine and runs it as a network service.

Developer C must evaluate the AGPL-3.0 network-interaction provisions.

Developer C should display:

> Powered By Orb Engine

in the service's product-facing documentation or interface where the ecosystem policy applies.

---

## Examples of Invalid Interpretations

### Invalid Interpretation A

> 'The architecture is MIT, therefore Orb Engine is MIT.'

Incorrect.

The engine is separately AGPL-3.0 licensed.

### Invalid Interpretation B

> 'Our app is MIT, therefore all dependencies become MIT.'

Incorrect.

A dependency keeps its own license.

### Invalid Interpretation C

> 'We mentioned Orbis somewhere in the source code, therefore we satisfy Powered By Orb Engine.'

Not sufficient where the product is required to display the exact ecosystem attribution in
a practical user-facing or distribution-facing location.

### Invalid Interpretation D

> 'We use Orb Engine but we are not an Orbis ecosystem product, so we may call ourselves an
official Orbis application.'

Incorrect.

Official status is separate from software dependency.

---

## The Architecture Is Meant to Escape the Application

This is one of the central ideas of Orbis.

The architecture should be useful even if Orbpad disappears.

The engine should be useful even if one ecosystem product disappears.

The user's knowledge should remain understandable.

That means:

```text
Architecture
    ↓
Multiple Implementations
    ↓
Multiple Applications
    ↓
Long-Lived Knowledge
```

---

## Long-Term Vision

The ultimate goal is a durable connected-knowledge ecosystem.

A user may eventually have:

```text
                 Orbis Architecture
                        │
                        ▼
                    Orb Engine
                        │
        ┌───────────────┼────────────────┐
        │               │                │
        ▼               ▼                ▼
      Orbpad       Research Tool      Graph Studio
        │               │                │
        └───────────────┼────────────────┘
                        │
                        ▼
               Shared Knowledge
```

The applications may look completely different.

The graph can remain compatible.

---

## Long-Term Sustainability

Structured knowledge may outlive the application that created it.

Therefore Orbis values:

- Stable concepts.
- Explicit relationships.
- Versioned formats.
- Documented migrations.
- Backward compatibility where practical.
- Open architectural definitions.
- Multiple implementations.

---

## Repository Structure

The documentation repository keeps the architecture specifications separate
from branding assets and general documentation.

```text
Orbis Documentation/
│
├── README.md
├── LICENSE
│
├── architecture/
│   ├── graph.md
│   ├── entity.md
│   ├── lore.md
│   │
│   └── Krono/
│       ├── ARCHITECTURE.md
│       ├── ENTITY_MODEL.md
│       ├── LORE_MODEL.md
│       ├── EVENTS_AND_EVOLUTION.md
│       ├── HISTORY.md
│       └── TEMPORAL_MODEL.md
│
└── docs/
    ├── branding/
    ├── diagrams/
    └── images/
```

The repository-root `architecture/` directory is the authoritative location
for the Tier I graph, `.entity`, and `.lore` specifications, as well as the
Krono architecture under `architecture/Krono/`.

Krono's serialization, testing, and roadmap documentation is implementation-
tier material and is intentionally kept out of `architecture/Krono/`.

The `docs/` directory is reserved for supporting documentation assets,
branding, diagrams, and other non-specification material.

Orb Engine maintains its own repository and its own AGPL-3.0 source and license
boundaries.

Ecosystem applications maintain their own repositories, licenses, and product
documentation.

---

## Orbis Project Family

<div align="center">

<a href="https://github.com/Phantom-Con-Artist/Orb">
  <img src="docs/orbenginelogo.png" alt="Orb Engine" width="110">
</a>

<a href="https://github.com/Phantom-Con-Artist/Orbpad">
  <img src="docs/orb_v256.png" alt="Orbpad" width="110">
</a>

<a href="https://github.com/Phantom-Con-Artist/Orbis">
  <img src="docs/orbisprojectlogo.png" alt="Orbis Project" width="110">
</a>

</div>

<div align="center">

| Project | Role | License | Repository |
|---|---|---|---|
| **Orbis Project** | Shared graph architecture | MIT | [GitHub](https://github.com/Phantom-Con-Artist/Orbis) |
| **Orb Engine** | Reference implementation | AGPL-3.0 | [GitHub](https://github.com/Phantom-Con-Artist/Orb) |
| **Orbpad** | First ecosystem application | MIT* | [GitHub](https://github.com/Phantom-Con-Artist/Orbpad) |

\* Orbpad's own application code is MIT; Orb Engine remains separately governed by AGPL-3.0.

</div>

---

## Current Projects

### Orb Engine

<div align="center">

<a href="https://github.com/Phantom-Con-Artist/Orb">
  <img src="docs/orbenginecover.png" alt="Orb Engine" width="820">
</a>

<br>

<a href="https://github.com/Phantom-Con-Artist/Orb">
  <img src="docs/orbenginelogo.png" alt="Orb Engine" width="120">
</a>

<br>

[![AGPL-3.0](https://img.shields.io/badge/license-AGPL--3.0-0cc0df?style=flat-square)](https://github.com/Phantom-Con-Artist/Orb)
[![Repository](https://img.shields.io/badge/source-GitHub-181717?style=flat-square&logo=github)](https://github.com/Phantom-Con-Artist/Orb)

</div>

Core implementation.

License: **AGPL-3.0**.

Repository:

https://github.com/Phantom-Con-Artist/Orb

### Orbpad

<div align="center">

<a href="https://github.com/Phantom-Con-Artist/Orbpad">
  <img src="docs/orb_v256.png" alt="Orbpad" width="120">
</a>

<br>

[![MIT](https://img.shields.io/badge/license-MIT-0cc0df?style=flat-square)](https://github.com/Phantom-Con-Artist/Orbpad)
[![Release](https://img.shields.io/badge/release-v1.0.1--stable-2ea44f?style=flat-square)](https://github.com/Phantom-Con-Artist/Orbpad)
[![Powered By Orb Engine](https://img.shields.io/badge/Powered%20By-Orb%20Engine-0cc0df?style=flat-square)](https://github.com/Phantom-Con-Artist/Orb)

</div>

Desktop knowledge-management application.

License: **MIT for the application itself, with Orb Engine separately governed by AGPL-3.0**.

Repository:

https://github.com/Phantom-Con-Artist/Orbpad

Attribution:

> **Powered By Orb Engine**

---

## Status

Orbis is actively developing.

The architecture, specifications, implementation, documentation, and ecosystem will evolve.

Some features described by future specifications may not yet exist in the current engine.

Documentation should distinguish current behavior from planned behavior.

---

## Community

The Orbis community is currently centered around Discord.

Development discussion:

https://discord.gg/Em2ur4J8PF

---

## Contact

Development and project inquiries can be made through the project's community and published
contact channels.

---

## Final Three-Tier Rule

Remember these three sentences:

> **The Orbis Project defines the architecture.**

> **Orb Engine implements the architecture.**

> **The Orbis Ecosystem builds products with or around the engine.**

And remember the corresponding licenses:

> **Architecture — MIT.**

> **Engine — AGPL-3.0.**

> **Products — Product-Specific.**

And where the ecosystem attribution policy applies:

> **Powered By Orb Engine.**

---

## Legal Notice

This README is a project policy and documentation statement, not legal advice.

The full legal terms of the GNU Affero General Public License, Version 3, control the
licensing of Orb Engine.

The MIT license controls the materials actually distributed under the MIT license.

Other components may have other licenses.

Where a question involves a combined work, distribution structure, trademark rights,
copyright scope, or jurisdiction-specific law, obtain professional legal advice.

---


<div align="center">

<a href="https://github.com/Phantom-Con-Artist/Orbis">
  <img src="docs/orbisprojectlogo.png" alt="Orbis Project" width="140">
</a>

<br>

**[Orbis Project](https://github.com/Phantom-Con-Artist/Orbis)**  
**[Orb Engine](https://github.com/Phantom-Con-Artist/Orb)**  
**[Orbpad](https://github.com/Phantom-Con-Artist/Orbpad)**

<br>

[![Powered By Orb Engine](https://img.shields.io/badge/Powered%20By-Orb%20Engine-0cc0df?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Phantom-Con-Artist/Orb)

</div>

## End

**Orbis Project**

> An open architecture for structured and connected knowledge.

**Architecture. Implementation. Ecosystem.**

**Open by design. Connected by structure. Built to outlive the application.**

---

## Expanded Tier Reference

### Tier I Reference — Architecture

Tier I answers the question:

> What concepts and structures define Orbis?

It is concerned with meaning.

It is concerned with shared structure.

It is concerned with interoperability.

It is concerned with the conceptual model.

It is not concerned with whether an individual implementation uses one library or another.

### Tier II Reference — Engine

Tier II answers the question:

> How does Orbis actually execute?

It is concerned with code.

It is concerned with runtime behavior.

It is concerned with APIs.

It is concerned with storage and serialization implementations.

It is concerned with queries.

It is concerned with software distribution.

### Tier III Reference — Ecosystem

Tier III answers the question:

> What can people build with this technology?

It is concerned with products.

It is concerned with user experience.

It is concerned with business models.

It is concerned with integrations.

It is concerned with specialized applications.

---

## Expanded Permission Reference

### Architecture Permission

A developer can use the architectural model as a foundation.

A developer can change it.

A developer can extend it.

A developer can publish a different implementation.

A developer can compete with Orb Engine.

A developer can compete with Orbpad.

A developer can create commercial tooling.

A developer can create internal enterprise tooling.

A developer can create academic software.

A developer can create research implementations.

A developer can teach the architecture.

A developer can write about the architecture.

### Engine Permission

A developer can run Orb Engine under AGPL-3.0.

A developer can inspect Orb Engine source.

A developer can modify Orb Engine under the terms of AGPL-3.0.

A developer can distribute covered versions under the terms of AGPL-3.0.

A developer can deploy covered versions subject to the license's obligations.

### Ecosystem Permission

A developer can create a new application.

A developer can create a plugin.

A developer can create a visualizer.

A developer can create a data editor.

A developer can create a web service.

A developer can create a commercial product.

A developer can create a noncommercial product.

A developer can create an open-source project.

A developer can create a proprietary product where the component licenses allow it.

---

## Expanded Restriction Reference

### Architecture Restrictions

Do not claim that unrelated proprietary materials are automatically MIT.

Do not assume a trademark right merely from copying an architectural concept.

Do not imply official certification without authorization.

### Engine Restrictions

Do not strip AGPL obligations from covered Orb Engine software.

Do not replace the Orb Engine license with an incompatible proprietary declaration.

Do not distribute modified covered code while pretending no source obligations apply.

Do not add restrictions that conflict with the AGPL.

### Ecosystem Restrictions

Do not claim that all ecosystem products share one license.

Do not claim that the ecosystem is synonymous with Orbpad.

Do not claim that the ecosystem designation automatically means official.

Do not use the ecosystem attribution to imply endorsement.

---

## Expanded Attribution Reference

The phrase is:

**Powered By Orb Engine**

The phrase identifies the dependency relationship.

It should be:

- Exact.
- Visible.
- Legible.
- Discoverable.
- Persistent across normal distribution channels.

It should not be:

- Hidden.
- Altered beyond recognition.
- Replaced by a vague synonym.
- Used to imply official endorsement.

### Desktop

Prefer the About or legal information interface.

### Web

Prefer a footer, About page, or legal page.

### CLI

Prefer help, version, or startup output.

### Library

Prefer README and package documentation.

### Installer

Prefer product information or license information.

### Documentation

Prefer the primary documentation site or README.

---

## Product Lifecycle

An ecosystem product should maintain attribution through its lifecycle.

### Development

Include dependency and licensing information early.

### Beta

Verify attribution placement.

### Release

Verify the final distribution includes the attribution.

### Updates

Keep attribution intact after product redesigns.

### Fork

Re-evaluate whether the fork remains an ecosystem product and whether the attribution
policy still applies.

---

## Migration Guidance

If an old application used a previous naming convention, migrate gradually.

Replace generic attribution with:

> **Powered By Orb Engine**

Do not silently remove license notices during migration.

---

## Audit Checklist

A product maintainer can use this checklist.

- Is the product's own license clearly stated?
- Is Orb Engine identified as AGPL-3.0 where used?
- Is the Powered By Orb Engine attribution present where required?
- Is the attribution visible in the appropriate interface or documentation?
- Are source and corresponding-source obligations evaluated?
- Are third-party notices preserved?
- Are modified engine components documented?
- Is official affiliation represented accurately?
- Are the Orbis architecture and Orb Engine clearly distinguished?

---

## Maintainer Checklist

Before shipping an ecosystem release:

1. Check dependencies.
2. Check license files.
3. Check attribution.
4. Check source availability obligations.
5. Check third-party notices.
6. Check branding statements.
7. Check documentation.
8. Check installer/package metadata.
9. Check hosted documentation.
10. Check release notes.

---

## Developer Checklist

Before starting development:

1. Decide whether you are implementing the architecture or importing the engine.
2. Identify the license boundary.
3. Identify the product license.
4. Plan attribution.
5. Plan source compliance if Orb Engine is used.
6. Document architecture versions.
7. Document engine versions.

---

## Distribution Checklist

Before distributing software:

- Include applicable license text.
- Include copyright notices.
- Include required source information.
- Include dependency information.
- Include Powered By Orb Engine when applicable.
- Avoid false endorsement.
- Document material modifications.

---

## Architecture Change Checklist

Before changing .entity:

- Define the semantic change.
- Define compatibility impact.
- Define serialization impact.
- Define migration impact.
- Define implementation impact.

Before changing .lore:

- Define semantic change.
- Define compatibility impact.
- Define temporal impact.
- Define migration impact.
- Define query impact.

---

## Data Model Philosophy

Orbis prefers explicit data over implicit assumptions.

An explicit relationship can be queried.

An explicit state can be versioned.

An explicit event can be referenced.

An explicit identity can survive application changes.

---

## Temporal Information

Orbis architectures may represent changing information over time.

A relationship may have a validity interval.

An entity may have different states.

A lore statement may become valid or invalid in a particular context.

The architecture can therefore model evolving knowledge.

The exact implementation belongs to Orb Engine or other implementations.

---

## Contextual Information

Knowledge may be valid only within a particular context.

Examples include:

- Time.
- Location.
- Perspective.
- Narrative state.
- Research state.
- Version.

Contextual graph semantics are one of the areas where Orbis can become significantly
more expressive than flat note systems.

---

## Querying

Graph queries should operate on structure rather than only text.

Applications may ask questions such as:

- Which entities belong to an organization?
- Which locations are controlled by a faction?
- Which relationships were valid at a given time?
- Which lore records reference an entity?
- Which objects have changed state?

Orb Engine provides implementation mechanisms for these operations.

The architecture provides the conceptual basis.

---

## Storage

Storage is an implementation concern.

The architecture should not depend on one physical storage engine where avoidable.

Possible implementations may use:

- Files.
- Databases.
- Embedded stores.
- Servers.
- Cloud storage.

The same conceptual graph can survive different storage technologies.

---

## Error Handling

Applications should distinguish malformed data from unknown data.

Unknown fields should not be silently destroyed when a safe preservation strategy exists.

Migration should be explicit when information cannot be represented by a newer version.

---

## Fidelity

Round-trip fidelity is a core Orbis priority.

Reading and writing a knowledge graph should avoid silent information loss.

If a serializer cannot preserve something, the limitation should be documented.

---

## Extensible Relationships

Relationship systems should permit future extension.

Applications should avoid treating every relationship as an unstructured string if it can
be represented meaningfully as a structured object.

---

## Ecosystem Diversity

An ecosystem should not become a monoculture.

A graph visualization product may prioritize visual exploration.

A research product may prioritize reproducibility.

A worldbuilding product may prioritize narrative workflows.

A developer tool may prioritize automation.

All can share a common graph foundation.

---

## Why the License Split Exists

The split is deliberate.

MIT on architecture encourages adoption and experimentation.

AGPL on the reference engine keeps the central implementation under strong copyleft.

Product-specific ecosystem licensing gives applications room to choose their own model.

The result is a layered system instead of a single giant license.

---

## The One-Sentence Interpretation

**Take the architecture freely under MIT, use the engine under AGPL-3.0, and build your own
product under a license compatible with the components you actually use.**

Where the ecosystem attribution policy applies:

**Say clearly that it is Powered By Orb Engine.**

---

## Closing Statement

Orbis exists to make connected knowledge durable.

The architecture should be reusable.

The engine should remain open.

The applications should remain diverse.

The data should remain meaningful.

The ecosystem should remain understandable.

That is the purpose of the three-tier design.

---

**Orbis Project**

**The architecture defines the graph.**

**Orb Engine brings the graph to life.**

**The ecosystem takes it everywhere.**

### Policy Question: Can I implement Orbis in another language?

Yes. The architecture is MIT-licensed where the relevant material is distributed under that license.


### Policy Question: Can I make my independent implementation proprietary?

Yes, provided it is genuinely independent and the applicable architectural materials permit that use.


### Policy Question: Can I fork Orb Engine?

Yes, but the fork of AGPL-covered engine code remains subject to AGPL-3.0.


### Policy Question: Can I sell Orb Engine?

Commercial activity is possible under AGPL-3.0, subject to its terms.


### Policy Question: Can I build a SaaS product with Orb Engine?

Yes, but evaluate and satisfy the AGPL-3.0 network-interaction provisions applicable to the deployment.


### Policy Question: Can I call my product Orbis?

Only where the applicable naming and branding permissions allow it; software licensing and branding are separate.


### Policy Question: Can I call my application official?

Not automatically. Official status is separately designated.


### Policy Question: What phrase should an ecosystem product display when required?

Powered By Orb Engine.


### Policy Question: Can I replace Powered By Orb Engine with Powered by Orbis?

No, not where the exact ecosystem attribution is required.


### Policy Question: Can I hide the phrase in source code only?

That is not the intended compliance presentation when a practical user-facing or distribution-facing location exists.


### Policy Question: Does the MIT architecture force my product to be MIT?

No.


### Policy Question: Does using Orb Engine make my source code automatically MIT?

No.


### Policy Question: Does Orbpad define the ecosystem?

No. Orbpad is one ecosystem application.


### Policy Question: Does the Orbis Project mean the GitHub repository only?

No. In this architecture it means the shared graph architecture and design.


### Policy Question: What defines Tier I?

Architecture, concepts, specifications, and shared design.


### Policy Question: What defines Tier II?

The executable reference implementation known as Orb Engine.


### Policy Question: What defines Tier III?

Applications and products built with or around the engine.


### Policy Question: Can two unrelated implementations share the same architecture?

Yes. That is a central goal of the architecture tier.


### Policy Question: Can products use only .entity and not Orb Engine?

Yes, through independent implementations or compatible tooling, subject to the relevant license.


### Policy Question: Can products extend .lore?

Yes, the architecture is intended to be extensible.


### Policy Question: Can a product be commercial and still be in the ecosystem?

Yes, subject to component licenses and applicable policies.


### Policy Question: Can a product be closed source?

Potentially, where its actual dependencies and license obligations permit it.


### Policy Question: Does AGPL allow me to add arbitrary extra restrictions?

No; do not use ecosystem policy language to contradict the AGPL. Keep branding policy separate.


### Policy Question: Why is Powered By Orb Engine separate?

Because the attribution/branding policy must not be presented as an extra restriction on AGPL rights.


### Policy Question: What happens if a product stops displaying the attribution?

It should stop presenting itself as compliant with the applicable Orbis Ecosystem branding policy until corrected.


### Policy Question: What if the product no longer uses Orb Engine?

The engine attribution should be reviewed and removed or updated based on the actual dependency.


### Policy Question: What if a product only mentions Orb Engine in documentation?

Documentation can identify the engine, but where ecosystem attribution is required the exact phrase should be presented in an appropriate practical location.


### Policy Question: Can independent implementations call themselves Orb Engine?

They should not imply that they are the official Orb Engine implementation.


### Policy Question: Can a fork be called Orb Engine Pro?

That could create branding confusion and should be evaluated under the applicable naming/trademark policy.


### Policy Question: Can I make a compatible engine without using Orb Engine code?

Yes.


### Policy Question: Can I use the architecture in academic research?

Yes.


### Policy Question: Can I use the architecture in a game?

Yes.


### Policy Question: Can I use the architecture in a CRM?

Yes.


### Policy Question: Can I use the architecture in a scientific data tool?

Yes.


### Policy Question: Can I use the architecture in a simulation?

Yes.


### Policy Question: Can I create a visualization-only application?

Yes.


### Policy Question: Can I create a migration tool?

Yes.


### Policy Question: Can I create a proprietary graph editor around an independent implementation?

Yes, subject to the actual materials and licenses used.


### Policy Question: Can I package Orb Engine with an application?

Yes only with compliance with AGPL-3.0 and applicable ecosystem policy.


### Policy Question: Can I distribute a modified Orb Engine binary?

Yes where permitted by AGPL-3.0 and with its required corresponding-source and notice obligations satisfied.


### Policy Question: Can I remove the Orb Engine license file?

No where the license requires its preservation.


### Policy Question: Can I remove copyright notices?

Not where applicable license terms require preservation.


### Policy Question: Can I claim the engine is mine?

No; do not misrepresent authorship or provenance.


### Policy Question: Can I claim an independent implementation is mine?

Yes, for your own original code, subject to accurate attribution of borrowed architectural material.


### Policy Question: Can I contribute improvements to the architecture?

Yes.


### Policy Question: Can I propose .entity extensions?

Yes.


### Policy Question: Can I propose .lore extensions?

Yes.


### Policy Question: Can I create a competing ecosystem?

You may create independent software, but you should not misrepresent it as the official Orbis Ecosystem.


### Policy Question: Can I criticize Orbis?

Yes. The architecture is intended to be open to discussion and improvement.


### Policy Question: Can I build a better engine?

Yes. Independent implementations are welcome.


### Policy Question: Can I build a better worldbuilding app?

Yes.


### Policy Question: Can I build a graph database using the architectural concepts?

Yes.


### Policy Question: Can I build a proprietary company around an independent implementation?

Potentially yes.


### Policy Question: Can I use a different data store?

Yes.


### Policy Question: Can I write a plugin system?

Yes.


### Policy Question: Can I build a cloud-hosted editor?

Yes, subject to the engine and product licensing requirements.


### Policy Question: Can I build a mobile application?

Yes.


### Policy Question: Can I build a desktop application?

Yes.


### Policy Question: Can I build a command-line tool?

Yes.


### Policy Question: Can I build a library?

Yes.


### Policy Question: Can I write bindings for another language?

Yes, subject to the license of the code being bound.


### Policy Question: Can I wrap Orb Engine?

Yes, but the underlying engine license remains applicable.


### Policy Question: Can I use a modified internal engine?

Yes, with AGPL-3.0 compliance where it applies.


### Policy Question: Can I use the engine without joining a community?

Software licensing does not require social membership; branding/ecosystem recognition is a separate policy matter.


### Policy Question: Can I build an internal company system?

Yes, subject to the licenses of the actual components used.


### Policy Question: Can I publish an internal system publicly later?

Re-evaluate the applicable license obligations before distribution.


### Policy Question: Can I use Orb Engine for a paid service?

Commercial use can be possible under AGPL-3.0; satisfy its conditions.


### Policy Question: Can I charge for support?

Yes, subject to ordinary legal and license constraints.


### Policy Question: Can I charge for hosting?

Yes, subject to ordinary legal and license constraints.


### Policy Question: Can I sell an independent implementation?

Yes.


### Policy Question: Can I modify the Orbis architecture?

Yes, under the terms of the MIT-licensed architectural materials.


### Policy Question: Can I remove features from an independent implementation?

Yes.


### Policy Question: Can I add features to an independent implementation?

Yes.


### Policy Question: Can I change the relationship model?

Yes in an independent implementation, while documenting compatibility differences.


### Policy Question: Can I claim full compatibility after changing semantics?

Only if the claim remains technically accurate.


### Policy Question: Can I document partial compatibility?

Yes.


### Policy Question: Can I translate the specification?

Yes, subject to the MIT license and any separate rights involved.


### Policy Question: Can I publish tutorials?

Yes.


### Policy Question: Can I publish books about Orbis?

Yes, subject to applicable copyright in the specific material reproduced.


### Policy Question: Can I create commercial training?

Yes.


### Policy Question: Can I create consulting around Orbis?

Yes.


### Policy Question: Can I offer an alternative to Orbpad?

Yes.


### Policy Question: Can I call it official Orbpad 2?

Not without authorization.


### Policy Question: Can I create a fork of Orbpad?

Yes, subject to Orbpad's own license and notices.


### Policy Question: Can I remove the Orbpad branding from my fork?

Follow the license and applicable branding rules; do not misrepresent origin.


### Policy Question: Can I use Orbis logos?

Only under whatever separate branding permissions apply.


### Policy Question: Does MIT automatically grant logo rights?

No.


### Policy Question: Can I create my own product logo?

Yes.


### Policy Question: Can I display Powered By Orb Engine beside my logo?

Yes, where required or desired by policy.


### Policy Question: Can I display additional text beside it?

Yes, provided the required phrase remains intact.


### Policy Question: Can the phrase be localized?

A translation may be supplemental, but the exact required phrase should remain available where the policy demands it.


### Policy Question: Can accessibility change the presentation?

Yes; accessibility may determine the practical presentation medium, while preserving the required wording.


### Policy Question: Can a screen reader read the attribution?

It should where practical.


### Policy Question: Can I use the attribution in a splash screen?

Yes.


### Policy Question: Can I use the attribution in an About screen?

Yes.


### Policy Question: Can I put it in the footer?

Yes for web products where that is a practical visible location.


### Policy Question: Can I put it in --version?

Yes for CLI products where that is appropriate.


### Policy Question: Can I put it only in a third-party notice file?

Not as the preferred method when a visible interface or documentation location exists.


### Policy Question: Can I put it only in release notes?

No, not as a substitute for persistent product attribution when the policy applies.


### Policy Question: Can I put it on the installer?

Yes.


### Policy Question: Can I put it on the download page?

Yes.


### Policy Question: Can I put it in the package README?

Yes.


### Policy Question: Can I hide it after installation?

No, not as the intended behavior.

