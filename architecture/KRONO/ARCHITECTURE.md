<div align="center">

<img src="../docs/orbis-project-krono.png"
     alt="Orbis Project"
     width="900"/>

<p><strong>THE ORBIS PROJECT: KRONO</strong></p>

<h1>Architecture</h1>

<p>
The Orb Engine 2 · Reference Implementation
</p>

</div>

This document defines the architectural boundaries of **The Orbis Project: Krono** as implemented by Orb.Engine 2.


Krono builds on the v1 graph engine without turning the engine into a monolith.

The architecture remains intentionally layered.

## High-Level Model

```text
┌─────────────────────────────────────────────┐
│                 Applications                 │
│       Orbpad · Editors · Domain Tools       │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│                  Orb.Engine                 │
│                                             │
│  Entity · Graph · Relationship · Properties │
│  Typed Values · Tags · Time · Evolution     │
│  History · Validation                       │
└───────────────┬───────────────┬─────────────┘
                │               │
                ▼               ▼
        Serialization         Storage
                │               │
                └───────┬───────┘
                        ▼
                .entity / .lore
```

## Canonical State vs Derived State

Krono maintains an important distinction between authoritative state and derived structures.

Examples:

```text
Canonical
├── Entities
├── Relationships
└── Relationship Histories

Derived / supporting
├── Tag index
├── Relationship indexes
└── Adjacency storage
```

Derived structures exist to make access fast and deterministic. They must agree with canonical state but should not become the source of truth.

## OrbGraph

`OrbGraph` remains the canonical owner of active graph state.

It owns the lifecycle of entities and relationships and coordinates the supporting graph structures.

The partial-class decomposition exists for maintainability; the public conceptual object is still one `OrbGraph`.

## Relationship Evolution Boundary

Evolution is not folded directly into every relationship mutation method.

Instead:

```text
OrbRelationshipEvolution
        │
        ▼
OrbRelationshipEvolutionExecutor
        │
        ▼
OrbGraph
```

This keeps declarative transition descriptions separate from graph mutation mechanics.

## History Boundary

History is separate from active relationship storage.

```text
Active relationship
    = current truth

Historical fact
    = recorded previous truth

Relationship history
    = append-only sequence of facts
```

An active relationship does not require historical storage until a historical fact is recorded.

## Temporal Boundary

`OrbTime` is a semantic model rather than a generic CLR timestamp.

The graph and historical systems consume temporal values through the defined temporal contracts instead of inventing ad-hoc string timestamps.

## Entity Boundary

Entities remain independently constructible.

Graph membership does not redefine the entity's identity or require application code to create graph-specific entity subclasses.

## Event Boundary

Events are entity semantics, not a separate inheritance tree.

```text
OrbEntity
Type = Event
```

Execution remains explicit through evolution objects and the executor.

## File and Application Boundary

Applications should not need to implement a private graph engine, relationship lifecycle, typed-value system, and temporal model simply because they want to manage connected information.

The intended dependency direction is:

```text
Application
    ↓
Orb.Engine
    ↓
Structured Information
```

not:

```text
Orb.Engine
    ↓
Orbpad-specific behavior
```

## Future Snapshot Layer

The architecture intentionally leaves room for a read-only temporal projection layer:

```text
OrbGraph + History + Time
            ↓
      OrbGraphSnapshot
            ↓
      Query / Diff / Analysis
```

This is planned work, not a current public API contract.

## Design Rule

The most important architectural rule for Krono is still:

> **Keep state ownership, mutation, temporal semantics, history, serialization, and application experience separate enough that one subsystem can evolve without contaminating the others.**
