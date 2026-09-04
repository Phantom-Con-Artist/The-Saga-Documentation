<!--
Copyright (c) 2026 Subhradeep Sarkar

SPDX-License-Identifier: MIT

Permission is hereby granted, free of charge, to any person obtaining a copy
of this document and associated documentation files (the "Document"), to deal
in the Document without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Document, and to permit persons to whom the Document is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Document.

THE DOCUMENT IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE DOCUMENT OR THE USE OR OTHER DEALINGS IN THE
DOCUMENT.

This document is part of the Orbis Project Architecture Specification.
It describes architecture and data formats independently of the Orb Engine
implementation.

Orb Engine is separately licensed under GNU AGPL-3.0.
This document does not relicense, supersede, or modify the license of Orb Engine
source code, binaries, APIs, or other AGPL-covered implementation material.
-->

<div align="center">

# Orbis Graph Architecture

### A formal, implementation-independent description of the Orbis graph model.

**Orbis Project · MIT Licensed Architecture Specification**

[![Specification](https://img.shields.io/badge/specification-BETA-F0AD00?style=for-the-badge)](https://github.com/Phantom-Con-Artist/Orbis-Documentation)
[![License: MIT](https://img.shields.io/badge/Specification-MIT-0cc0df?style=for-the-badge)](../LICENSE)
[![Implementation: Orb Engine](https://img.shields.io/badge/implementation-Orb%20Engine%20AGPL--3.0-0cc0df?style=for-the-badge)](https://github.com/Phantom-Con-Artist/Orb)

</div>

---


## 1. Purpose

The Orbis graph architecture defines a structured way to represent information as
objects connected by explicit relationships.

The central architectural idea is simple:

```text
Entities       = things
Relationships  = connections
Properties     = structured information attached to either
Graph          = the container that gives the connections meaning
```

The graph is intended to preserve structure rather than flattening knowledge into
unrelated text records.

This specification describes the architecture itself.

It does not require a particular programming language, storage engine, UI toolkit,
database, or executable implementation.

---

## 2. Licensing Boundary

This document is part of **Tier I — The Orbis Project**.

The architectural specification contained in this document is released under the
**MIT License**.

The MIT license applies to the copyrightable specification material distributed
as part of this document.

**Orb Engine is Tier II and is separately licensed under GNU AGPL-3.0.**

Using the architectural concepts described here does not, by itself, make an
independent implementation a copy of Orb Engine.

Conversely, copying or incorporating Orb Engine source code remains subject to
Orb Engine's AGPL-3.0 license.

### 2.1 What this specification is

This specification is:

- An architectural definition.
- A conceptual model.
- A graph-structure specification.
- A description of entities and relationships.
- A description of graph invariants.
- A description of interoperable data concepts.
- A reference for independent implementations.

### 2.2 What this specification is not

This specification is not:

- Orb Engine source code.
- A relicensing document for Orb Engine.
- A copy of Orb Engine's internal implementation.
- A requirement to use .NET.
- A requirement to use C#.
- A requirement to use the Orb Engine APIs.
- A requirement to distribute software under AGPL-3.0 when Orb Engine itself is not used.

---

## 3. Architectural Vocabulary

The following terms have precise meanings within this specification.

| Term | Meaning |
|---|---|
| Entity | A uniquely identifiable object represented in the graph |
| Relationship | A directed connection between two entities |
| Property | A named typed value attached to an entity or relationship |
| Value | A typed piece of data |
| Graph | A collection of entities and relationships |
| Source | The entity from which a relationship originates |
| Target | The entity toward which a relationship points |
| Relationship Type | A semantic label describing a relationship |
| Entity Type | An optional classification of an entity |
| Identifier | A stable GUID identifying an object |
| `.entity` | A document representation of one entity |
| `.lore` | A document representation of a complete graph |

---

## 4. Graph as a Mathematical Structure

At the architectural level, an Orbis graph can be understood as:

```text
G = (V, E)

V = set of entities
E = set of directed relationships
```

Every relationship has:

```text
relationship.source → relationship.target
```

Both endpoints must correspond to entities contained in the graph.

A relationship is therefore not merely a string such as:

```text
"A is related to B"
```

It is structured data:

```text
Source → Relationship → Target
```

This distinction enables graph traversal, reachability, validation, querying,
and explicit relationship metadata.

---

## 5. Entity Nodes

An entity is a graph node with a stable identity.

The architectural shape is:

```text
Entity
├── id
├── name
├── type
└── properties
```

The identifier is the identity of the entity.

The name is intended for human-readable presentation.

The type provides optional classification.

Properties provide extensible structured data.

An entity does not inherently belong to a graph at creation time. It can be
constructed, serialized, stored, modified, and then inserted into a graph.

This separation is important because it allows entity documents to exist
independently from graph documents.

---

## 6. Entity Identity

An entity identity is represented by a GUID.

The identifier has two major purposes:

1. Distinguishing one entity from another.
2. Providing a stable reference for relationships.

Example:

```text
Entity A
ID = 2df2b2c3-4e8a-45d2-8e1c-b1b2a7a22b91
```

The actual GUID value has no semantic meaning unless an application assigns
meaning outside the graph.

Identifiers should therefore be treated as opaque stable identifiers.

### 6.1 Identity Invariant

A graph must not contain two different entities under the same identifier.

### 6.2 Relationship Identity

Relationships also have GUID identifiers.

This means relationships are independently addressable graph objects.

Two relationships can therefore connect the same pair of entities while remaining
distinct objects, provided each relationship has a distinct identity.

---

## 7. Entity Name

The entity model provides a human-readable `name`.

The current engine model represents the property as nullable.

Implementations should therefore distinguish:

```text
identity ≠ display name
```

Changing an entity's name does not inherently change its identity.

This is a fundamental graph-design property.

For interoperable applications, the identifier should be treated as the stable
reference and the name as a mutable presentation value.

---

## 8. Entity Type

An entity may have an optional `type`.

Examples:

```text
Character
Kingdom
City
Organization
Artifact
Event
Concept
```

The engine does not impose a universal ontology over entity types.

That allows the same architecture to operate across multiple domains.

An implementation may impose domain-specific type registries, but those registries
are application or ecosystem concerns rather than requirements of the base graph.

---

## 9. Properties

Properties attach structured information to an entity.

Conceptually:

```text
Property
├── name
└── value
```

The property name identifies the field.

The property value retains an explicit value type.

This prevents every value from degenerating into a textual string.

For example:

```text
population = Integer(2400000)
```

is structurally different from:

```text
population = String("2400000")
```

Even if a UI chooses to display both as similar text.

---

## 10. Typed Values

The current public Orb Engine value model defines these canonical categories:

```text
Null
String
Boolean
Integer
Decimal
DateTime
Guid
List
Object
```

### 10.1 Current Implementation Note: Floating-Point Values

The current public `OrbValueType` enumeration does not expose `Double` as a
separate top-level category.

The implementation can nevertheless encounter nested CLR floating-point values.
Nested `float` and `double` values are normalized through the decimal category
while retaining CLR subtype metadata for round-trip restoration.

Accordingly:

```text
Top-level canonical type:
Decimal

Nested CLR subtype:
Single or Double
```

An independent implementation may use another internal representation while
preserving the externally documented semantic distinction.

---

## 11. Value Categories

### Null

Represents the absence of a value.

```json
{
  "type": "Null",
  "value": null
}
```

### String

Textual data.

```json
{
  "type": "String",
  "value": "Avarian"
}
```

### Boolean

Logical true/false data.

```json
{
  "type": "Boolean",
  "value": true
}
```

### Integer

The canonical integer representation is signed 64-bit integer semantics.

```json
{
  "type": "Integer",
  "value": 42
}
```

### Decimal

Decimal numeric data.

```json
{
  "type": "Decimal",
  "value": 19.95
}
```

### DateTime

Date and time information represented using the implementation's supported
date-time serialization.

### Guid

A GUID value represented as a GUID string in JSON.

### List

Ordered collections of nested values.

### Object

String-keyed collections of nested values.

---

## 12. Nested Values

Lists and objects may contain structured values recursively.

Conceptually:

```text
Object
├── name       → String
├── age        → Integer
├── verified   → Boolean
├── identifier → Guid
└── history    → List
                 ├── Integer
                 ├── Object
                 └── Boolean
```

The important architectural property is that nested values retain type metadata.

A consumer should not infer the type solely from the JSON token when the format
explicitly supplies typed information.

---

## 13. Relationships

A relationship is a first-class graph object.

Its architectural shape is:

```text
Relationship
├── id
├── type
├── sourceId
├── targetId
└── properties
```

The relationship is directional.

For:

```text
A ──rules──> B
```

the source is `A` and the target is `B`.

The reverse:

```text
B ──rules──> A
```

is a different relationship.

The semantic meaning of the relationship type is domain-defined.

---

## 14. Relationship Type

The relationship `type` is a string semantic label.

Examples:

```text
member_of
controls
capital_of
located_in
parent_of
allied_with
```

The architecture does not force a universal vocabulary.

Applications may define their own relationship types.

Interoperable applications should document the semantics of the relationship
types they introduce.

---

## 15. Relationship Metadata

A relationship can contain properties in the same general way an entity can.

This means information can be attached to the connection itself.

Example:

```text
King ──rules──> Kingdom

Relationship properties:
    since  = DateTime(...)
    title  = String("Sovereign")
```

The architectural consequence is important:

**The connection itself can carry structured information.**

This is more expressive than placing every fact on either endpoint.

---

## 16. Endpoint Integrity

Every relationship must reference an existing source entity and an existing
target entity at the time the relationship is inserted into a graph.

Invalid:

```text
Relationship R

sourceId = Entity X
targetId = Entity Z

Entity Z does not exist.
```

Valid:

```text
Entity X
Entity Z
Relationship R
X ──type──> Z
```

This is a graph invariant, not merely a UI preference.

---

## 17. Relationship Multiplicity

The graph architecture does not require a one-to-one relationship between two
entities.

Multiple relationship objects may connect the same source and target:

```text
A ──employs──> B
A ──knows───> B
A ──trusts──> B
```

These are separate relationships.

They may have distinct IDs and distinct properties.

This prevents semantic information from being collapsed into a single opaque
edge.

---

## 18. Self-Relationships

A relationship may point from an entity to itself.

Example:

```text
A ──references──> A
```

The current engine's serialization tests explicitly exercise self-link
preservation.

A compatible implementation should therefore not assume:

```text
sourceId != targetId
```

unless a higher-level application explicitly imposes such a constraint.

---

## 19. Graph Container

A graph contains two primary collections:

```text
OrbGraph
├── Entities
└── Relationships
```

Conceptually:

```text
Graph
│
├── Entity A
├── Entity B
├── Entity C
│
├── Relationship R1
├── Relationship R2
└── Relationship R3
```

The graph establishes the referential context in which relationships are valid.

---

## 20. Collection Identity

The current implementation internally maintains entity and relationship
collections keyed by GUID.

The externally important invariant is:

```text
dictionary key == object's Id
```

An inconsistent state such as:

```text
Dictionary key = GUID-A
Entity.Id      = GUID-B
```

is invalid.

This identity alignment is used by validation and serialization logic.

---

## 21. Read Access and Mutation

The current engine exposes read-only views of its entity and relationship
collections while keeping mutation operations controlled by graph methods.

Architecturally, this reflects a useful principle:

```text
Read graph state
        ↓
Controlled graph mutation
        ↓
Invariant preservation
```

An independent implementation may use another mechanism, but it should preserve
the same conceptual guarantee if it claims behavioral compatibility.

---

## 22. Adding Entities

Adding an entity requires:

1. A non-null entity object.
2. A stable identifier.
3. An identifier not already present in the graph.

Conceptually:

```text
Graph.AddEntity(A)
```

If another entity already occupies `A.Id`, the insertion must fail rather than
silently replacing the existing node.

This protects identity integrity.

---

## 23. Adding Relationships

Adding a relationship requires:

1. A relationship object.
2. A unique relationship identifier.
3. An existing source entity.
4. An existing target entity.

Conceptually:

```text
Graph.AddRelationship(R)
```

The graph verifies endpoint existence before storing the relationship.

A failed insertion must not leave the graph partially mutated.

---

## 24. Removing Entities

Removing an entity also removes every relationship for which that entity is:

```text
source
```

or:

```text
target
```

Example:

```text
A ──r1──> B
A ──r2──> C
D ──r3──> A
```

Removing `A` removes:

```text
A
r1
r2
r3
```

leaving:

```text
B
C
D
```

This is relationship cascade for referential integrity.

---

## 25. Removing Relationships

Removing a relationship affects the relationship object itself.

It does not automatically remove either endpoint entity.

```text
A ──R──> B

remove R

A        B
```

The entities remain members of the graph.

---

## 26. Incoming Relationships

Incoming relationships are those where:

```text
relationship.targetId == entityId
```

Example:

```text
A ──R1──> C
B ──R2──> C
```

For `C`, both `R1` and `R2` are incoming relationships.

---

## 27. Outgoing Relationships

Outgoing relationships are those where:

```text
relationship.sourceId == entityId
```

Example:

```text
A ──R1──> B
A ──R2──> C
```

For `A`, both are outgoing relationships.

---

## 28. Incident Relationships

All relationships touching an entity are:

```text
outgoing + incoming
```

A relationship is incident on an entity if that entity appears as either endpoint.

---

## 29. Neighbor Discovery

Neighbor discovery treats connectivity around an entity as a graph-neighborhood
operation.

For:

```text
A ──> B
C ──> A
```

the neighbors of `A` are:

```text
B
C
```

The current implementation intentionally examines both source and target sides
for neighbor discovery.

This is different from directed traversal.

---

## 30. Directed Traversal

Traversal follows outgoing relationships.

Example:

```text
A ──> B ──> C
```

Starting at `A`, traversal may reach:

```text
B
C
```

Starting at `C`, it does not reach `B` unless another outgoing path exists.

Therefore:

```text
neighbor semantics != traversal semantics
```

This distinction must be preserved in compatible implementations.

---

## 31. Reachability

Reachability asks whether a target entity can be reached from a source entity by
following outgoing relationships.

Example:

```text
A ──> B ──> C ──> D
```

Then:

```text
A reaches D = true
D reaches A = false
```

unless reverse relationships are explicitly present.

The current engine uses breadth-first traversal for this operation.

---

## 32. Traversal Behavior

The current traversal behavior can be summarized as:

```text
Start
  ↓
queue source
  ↓
take current entity
  ↓
inspect outgoing relationships
  ↓
enqueue unseen targets
  ↓
repeat
```

A visited set prevents repeated processing of the same entity.

This allows cyclic graphs to be traversed safely.

---

## 33. Cycles

Cycles are valid.

Example:

```text
A ──> B
B ──> C
C ──> A
```

A traversal implementation must avoid infinite loops.

The current engine uses a visited set for this purpose.

The architectural principle is:

> Graph traversal must terminate on finite graphs even when cycles exist.

---

## 34. Validation

Graph validation checks structural invariants.

Important classes of validation include:

```text
Entity identity
Relationship identity
Endpoint existence
Property naming
Dictionary-key identity
Null object detection
```

Validation exists both as a direct graph operation and as part of serialization
boundaries.

---

## 35. Property Identity

A property has both:

```text
dictionary key
property.Name
```

The current engine requires those names to agree during validation.

Invalid:

```text
Dictionary key = "population"
Property.Name   = "Population"
```

when case-sensitive identity is required by the implementation.

Valid:

```text
Dictionary key = "population"
Property.Name   = "population"
```

This preserves property identity.

---

## 36. Serialization Boundary

The graph architecture separates conceptual graph data from physical storage.

At a high level:

```text
Graph
  ↓
Serialization
  ↓
Document
  ↓
Storage
```

and:

```text
Storage
  ↓
Document
  ↓
Deserialization
  ↓
Graph
```

This allows an implementation to change its storage mechanism independently
from the conceptual graph model.

---

## 37. `.entity` and `.lore`

Orbis currently defines two primary document concepts.

```text
.entity
    = one entity

.lore
    = one complete graph
```

The distinction is architectural.

A single entity can exist independently.

A lore document provides the connected context containing multiple entities and
relationships.

---

## 38. Graph as the Semantic Core

The document formats are representations.

The graph is the semantic model.

Therefore:

```text
JSON text
   ≠
the graph itself
```

The JSON representation is a serialized form of graph objects.

Implementations should preserve semantic meaning rather than treating the serialized
text layout as the only possible internal representation.

---

## 39. Interoperability Principles

An Orbis-compatible graph implementation should aim to preserve:

- Stable identifiers.
- Entity identity.
- Relationship identity.
- Relationship direction.
- Relationship endpoints.
- Entity type.
- Property names.
- Property types.
- Nested structured values.
- Document format versions.

---

## 40. Versioning

The current engine format version is:

```text
1
```

The serialized documents identify this with:

```json
{
  "formatVersion": 1
}
```

The current implementation rejects unsupported format versions rather than
silently interpreting unknown versions.

A future specification revision should document compatibility and migration rules.

---

## 41. Architectural Extensibility

The base architecture does not prevent applications from introducing:

```text
new entity types
new relationship types
new properties
new domain-specific semantics
```

The extension should not destroy the identity or endpoint semantics of the graph.

A domain extension should ideally be additive where compatibility matters.

---

## 42. Domain Independence

The graph model is intentionally domain-neutral.

The same graph structure can represent:

```text
Worldbuilding
Research
Organizations
Projects
Historical information
Documentation
Knowledge management
Game data
Scientific information
```

The domain-specific vocabulary sits above the base graph.

---

## 43. Deterministic Semantics

The architecture should define semantic behavior independently of UI presentation.

For example:

```text
A → B
```

means the same relationship regardless of whether an application displays it
as a card, table, diagram, or text.

---

## 44. Application Responsibilities

Applications are responsible for:

- User interface.
- Editing workflows.
- Domain-specific validation.
- Visualization.
- Permissions.
- Product-specific metadata.
- User experience.

The engine or another implementation is responsible for the graph model and its
structural invariants.

---

## 45. Architecture Versus Implementation

The following are architectural:

```text
Entity
Relationship
Property
Graph
Stable identity
Directed endpoints
Typed values
.entity concept
.lore concept
```

The following are implementation choices:

```text
Dictionary implementation
Specific traversal algorithm
Programming language
Storage backend
UI toolkit
Memory layout
```

The current Orb Engine happens to use particular mechanisms, but independent
implementations are not required to reproduce its internal code.

---

## 46. Compatibility Levels

An implementation can describe compatibility honestly as:

```text
Architecture-compatible
Format-compatible
Partially compatible
Engine-compatible
```

These terms should not be treated as interchangeable.

Architecture-compatible does not mean source-compatible.

Format-compatible does not necessarily mean behavior-compatible.

Engine-compatible should be used only when a defined behavioral target exists.

---

## 47. Current V1 Behavioral Invariants

Based on the current engine implementation, these invariants are important:

```text
1. Entity IDs are unique within a graph.
2. Relationship IDs are unique within a graph.
3. Relationship endpoints must exist.
4. Removing an entity removes its connected relationships.
5. Directed traversal follows outgoing relationships.
6. Neighbor discovery considers both endpoint directions.
7. Reachability follows outgoing relationships.
8. Graph validation detects broken references.
9. Property dictionary keys must match property names.
10. Format versioning is explicit.
11. Unsupported current document versions are rejected.
12. Serialization aims to preserve typed nested values.
```

---

## 48. Design Principle: Explicitness

An Orbis graph should prefer:

```text
explicit identity
explicit relationship
explicit type
explicit property
explicit value type
```

over ambiguous strings and implicit references.

This is one of the core reasons the graph can remain machine-queryable.

---

## 49. Design Principle: Referential Integrity

The graph should not knowingly permit:

```text
Relationship → missing entity
```

unless a higher-level, explicitly defined unresolved-reference mechanism exists.

The current engine does not use unresolved graph endpoints as valid relationship
state.

---

## 50. Design Principle: Structural Persistence

A serializer should preserve structure.

This includes:

```text
nested objects
nested lists
typed values
GUIDs
DateTime values
numeric distinctions
```

A representation that produces valid JSON but loses semantic type information
does not satisfy the intended fidelity objective.

---

## 51. Error Handling Philosophy

Malformed graph structures should fail clearly.

Examples:

```text
invalid format version
missing relationship endpoint
empty relationship type
invalid property value
unknown value type
malformed JSON
```

Silent corruption is worse than explicit rejection.

---

## 52. Security Boundary

This architecture specification does not prescribe authentication or
authorization.

Those are application or service-layer responsibilities.

An implementation exposed through a network must define appropriate access
controls independently of the graph model.

---

## 53. Storage Independence

The architecture does not require:

```text
filesystem
SQL
NoSQL
cloud object storage
embedded database
```

The same graph semantics can be persisted through many backends.

The file formats are representations, not the sole storage mechanism.

---

## 54. Graph Operations Summary

Conceptually, a conforming graph implementation should support operations in
these categories:

```text
Entity:
    add
    remove
    lookup
    exists

Relationship:
    add
    remove
    lookup
    exists

Neighborhood:
    incoming
    outgoing
    incident
    neighbors

Traversal:
    traverse
    reachability

Integrity:
    validate
```

Not every independent implementation must expose these functions with the same
API names.

The semantic responsibilities are what matter.

---

## 55. Example Graph

```text
┌──────────────┐
│   Avaria     │
│  Kingdom     │
└──────┬───────┘
       │
       │ capital_of
       ▼
┌──────────────┐
│    Valor     │
│     City     │
└──────────────┘
```

This can be represented as:

```text
Entities:
    Avaria
    Valor

Relationship:
    Avaria ──capital_of──> Valor
```

The serialized form belongs to the `.lore` document model.

---

## 56. Example Relationship Metadata

A relationship can carry metadata:

```text
A ──rules──> B

Properties:
    start = DateTime(...)
    title = "Sovereign"
```

The metadata belongs to the edge, not to either endpoint.

---

## 57. No Hidden Ontology

The base architecture does not assume that:

```text
Character
City
Kingdom
Organization
```

are globally reserved classes.

These are examples of application-level classifications.

An implementation should preserve arbitrary valid string classifications unless
a higher-level schema says otherwise.

---

## 58. Backward Compatibility

Consumers should use `formatVersion` to determine how a document is interpreted.

A consumer that does not understand a version should fail explicitly or use a
documented migration path.

It should not silently interpret unknown structure according to an older schema.

---

## 59. Forward Compatibility

Future specifications may introduce new properties or structures.

Applications should consider preservation strategies for fields they do not
understand.

However, compatibility behavior for unknown future fields must be defined by
the version of the specification being implemented.

---

## 60. Implementation Independence Statement

A developer may use this document as a basis for an independent implementation.

They may:

- Use another language.
- Use another storage system.
- Use another graph algorithm.
- Use another serialization library.
- Design a different UI.
- Create a commercial product.
- Create an open-source product.
- Create a research implementation.
- Create a competing implementation.

This freedom comes from the MIT licensing of the architecture specification.

---

## 61. Orb Engine Separation Statement

The existence of an independent implementation does not make it Orb Engine.

Orb Engine is the specific reference implementation maintained in the Orb Engine
repository.

The source code of Orb Engine is separately AGPL-3.0 licensed.

This specification deliberately avoids reproducing that source.

---

## 62. Summary

The Orbis graph architecture can be reduced to:

```text
ENTITY
  +
RELATIONSHIP
  +
PROPERTY
  +
TYPED VALUE
  ↓
GRAPH
```

With the critical invariant:

```text
RELATIONSHIP SOURCE/TARGET
        ↓
must resolve to entities in the graph
```

And the critical licensing boundary:

```text
Architecture      → MIT
Orb Engine        → AGPL-3.0
Applications      → Product-specific
```

---

## 63. Conformance Checklist

An implementation claiming architectural compatibility should document:

- [ ] How entity identity is represented.
- [ ] How relationship identity is represented.
- [ ] How relationships reference endpoints.
- [ ] How properties are represented.
- [ ] How typed values are represented.
- [ ] How lists and objects are represented.
- [ ] How relationship direction works.
- [ ] How neighbors are computed.
- [ ] How traversal works.
- [ ] How reachability works.
- [ ] How invalid relationships are handled.
- [ ] How entity removal affects relationships.
- [ ] How format versions are handled.
- [ ] Which `.entity` revision is supported.
- [ ] Which `.lore` revision is supported.

---

## 64. Final Architectural Statement

> **Orbis represents structured knowledge as a graph of identifiable entities and
> explicit, typed relationships.**

The architecture is designed so that:

```text
Applications may change.
Implementations may change.
Storage may change.
The underlying structured knowledge can remain understandable.
```

---

## License

### MIT License

Copyright (c) 2026 Subhradeep Sarkar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this document and associated documentation files (the "Document"), to deal
in the Document without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Document, and to permit persons to whom the Document is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Document.

THE DOCUMENT IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE DOCUMENT OR THE USE OR OTHER DEALINGS IN THE
DOCUMENT.
