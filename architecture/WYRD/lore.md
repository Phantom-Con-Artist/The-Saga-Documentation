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

# Orbis `.lore` Specification

### The complete graph document model for interconnected Orbis knowledge.

**Orbis Project · MIT Licensed Architecture Specification**

[![Specification](https://img.shields.io/badge/specification-BETA-F0AD00?style=for-the-badge)](https://github.com/Phantom-Con-Artist/Orbis-Documentation)
[![License: MIT](https://img.shields.io/badge/Specification-MIT-0cc0df?style=for-the-badge)](../LICENSE)
[![Implementation: Orb Engine](https://img.shields.io/badge/implementation-Orb%20Engine%20AGPL--3.0-0cc0df?style=for-the-badge)](https://github.com/Phantom-Con-Artist/Orb)

</div>

---


## 1. Purpose

A `.lore` document represents an entire Orbis graph.

Where `.entity` describes one identifiable object, `.lore` describes a connected
collection of:

```text
Entities
+
Relationships
```

The format is therefore the primary portable representation for an interconnected
body of Orbis knowledge.

---

## 2. Licensing Boundary

This specification is part of **Tier I — The Orbis Project** and is released
under the **MIT License**.

The reference implementation in Orb Engine is separately licensed under
**GNU AGPL-3.0**.

This document describes the `.lore` architecture and observable document model.
It does not reproduce or relicense Orb Engine source code.

```text
.lore specification     → MIT
Orb Engine .lore code   → AGPL-3.0
```

An independent implementation may implement this specification under the terms
applicable to the architecture material, without taking Orb Engine source code.

---

## 3. What a `.lore` Document Is

A `.lore` document is a serialized graph.

Conceptually:

```text
OrbGraph
   ↓
.lore document
```

and:

```text
.lore document
   ↓
OrbGraph
```

The document contains the complete set of entities and relationships represented
by that graph snapshot.

---

## 4. Canonical Top-Level Structure

The current format uses:

```json
{
  "formatVersion": 1,
  "entities": [],
  "relationships": []
}
```

The top-level fields are:

```text
formatVersion
entities
relationships
```

---

## 5. `formatVersion`

The current reference format version is:

```text
1
```

The current engine explicitly rejects unsupported versions.

This avoids accidental interpretation of a document according to the wrong schema.

A future incompatible change should use a new format version.

---

## 6. `entities`

`entities` is an array of entity records.

Conceptually:

```text
lore
├── entities
│   ├── entity A
│   ├── entity B
│   └── entity C
└── relationships
    ├── relationship R1
    └── relationship R2
```

Each entity record contains the data necessary to reconstruct the entity.

---

## 7. Lore Entity Record

A lore entity has the shape:

```json
{
  "id": "GUID",
  "name": "Entity Name",
  "type": "Entity Type",
  "properties": {}
}
```

Unlike a standalone `.entity` document, the lore entity record does not require
its own `formatVersion` field because the document-level version applies to the
entire `.lore` structure.

---

## 8. Entity Identity in Lore

Every entity in a `.lore` document must have a valid non-empty GUID.

The current engine validates duplicate entity IDs.

Therefore:

```text
Entity A.id
!=
Entity B.id
```

for all distinct entities in the document.

---

## 9. Lore Entity Name

Current reference validation requires a non-empty entity name inside a `.lore`
document.

This is stricter than the standalone runtime model's nullable name property.

The distinction is important:

```text
Standalone entity model
    → name may be nullable

Current .lore validation
    → entity name must be non-empty
```

An application should therefore not assume that every runtime entity necessarily
came from a valid V1 `.lore` document.

---

## 10. Lore Entity Type

The `type` field is an optional classification.

Examples:

```text
Kingdom
City
Character
Organization
Artifact
```

No universal ontology is imposed by the core format.

---

## 11. Lore Entity Properties

Each entity carries its own property dictionary.

Example:

```json
{
  "id": "GUID",
  "name": "Avaria",
  "type": "Kingdom",
  "properties": {
    "language": {
      "type": "String",
      "value": "Avarian"
    }
  }
}
```

The same typed-value rules used by `.entity` apply here.

---

## 12. `relationships`

`relationships` is an array of relationship records.

Each relationship describes a directed edge between two entity IDs.

Conceptually:

```text
Source Entity
      │
      │ relationship
      ▼
Target Entity
```

---

## 13. Lore Relationship Record

A relationship has this shape:

```json
{
  "id": "RELATIONSHIP-GUID",
  "type": "capital_of",
  "sourceId": "SOURCE-GUID",
  "targetId": "TARGET-GUID",
  "properties": {}
}
```

The required structural fields are:

```text
id
type
sourceId
targetId
properties
```

---

## 14. Relationship Identity

Every relationship has its own GUID.

The relationship ID must be unique within the `.lore` document.

This means:

```text
Entity identity
and
Relationship identity
```

are separate identity domains.

A relationship can therefore be uniquely referenced even when multiple edges
connect the same entities.

---

## 15. Relationship Type

`type` is a semantic relationship label.

Example:

```text
capital_of
```

The current engine requires a non-empty relationship type.

---

## 16. `sourceId`

`sourceId` identifies the origin entity of the relationship.

Example:

```text
Avaria
   │
   └──capital_of──>
```

The GUID stored in `sourceId` must correspond to an entity in the same document.

---

## 17. `targetId`

`targetId` identifies the destination entity.

Example:

```text
──capital_of──> Valor
```

The GUID stored in `targetId` must correspond to an entity in the same document.

---

## 18. Endpoint Referential Integrity

A `.lore` relationship is invalid if:

```text
sourceId does not exist
```

or:

```text
targetId does not exist
```

The current serializer explicitly validates both endpoints.

This prevents a `.lore` document from containing relationships pointing into
nonexistent graph nodes.

---

## 19. Duplicate Entity IDs

The current `.lore` serializer rejects duplicate entity IDs.

Invalid:

```text
Entity A.id = X
Entity B.id = X
```

Valid:

```text
Entity A.id = X
Entity B.id = Y
```

This is a core identity invariant.

---

## 20. Duplicate Relationship IDs

The current `.lore` serializer also rejects duplicate relationship IDs.

Invalid:

```text
Relationship R1.id = X
Relationship R2.id = X
```

Valid:

```text
Relationship R1.id = X
Relationship R2.id = Y
```

---

## 21. Relationship Direction

Relationships are directional.

Example:

```text
A ──controls──> B
```

does not imply:

```text
B ──controls──> A
```

If the reverse meaning is needed, it should be represented explicitly by a
relationship or by an application-defined symmetric interpretation.

---

## 22. Multiple Relationships

Multiple relationship records may connect the same source and target.

Example:

```text
A ──knows────> B
A ──trusts───> B
A ──employs──> B
```

Each relationship has a distinct identity and may carry different properties.

---

## 23. Self-Relationships

A `.lore` document may contain a self-link:

```text
A ──references──> A
```

The current reference tests explicitly preserve self-links through serialization.

Compatible implementations should not reject self-links solely because both
endpoint IDs are equal.

---

## 24. Relationship Properties

A relationship can contain its own structured properties.

Example:

```json
{
  "id": "RELATIONSHIP-GUID",
  "type": "rules",
  "sourceId": "KING-GUID",
  "targetId": "KINGDOM-GUID",
  "properties": {
    "since": {
      "type": "DateTime",
      "value": "2020-01-01T00:00:00"
    },
    "title": {
      "type": "String",
      "value": "Sovereign"
    }
  }
}
```

The relationship metadata belongs to the edge.

---

## 25. Complete Minimal `.lore`

Conceptually:

```json
{
  "formatVersion": 1,
  "entities": [],
  "relationships": []
}
```

This represents an empty graph document.

The current engine's document validation accepts the structural collections as
long as they are present and valid.

---

## 26. Complete One-Entity `.lore`

```json
{
  "formatVersion": 1,
  "entities": [
    {
      "id": "11111111-1111-1111-1111-111111111111",
      "name": "Avaria",
      "type": "Kingdom",
      "properties": {}
    }
  ],
  "relationships": []
}
```

This represents a graph containing one entity and no relationships.

---

## 27. Complete Connected `.lore`

```json
{
  "formatVersion": 1,
  "entities": [
    {
      "id": "11111111-1111-1111-1111-111111111111",
      "name": "Avaria",
      "type": "Kingdom",
      "properties": {}
    },
    {
      "id": "22222222-2222-2222-2222-222222222222",
      "name": "Valor",
      "type": "City",
      "properties": {}
    }
  ],
  "relationships": [
    {
      "id": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "type": "capital_of",
      "sourceId": "11111111-1111-1111-1111-111111111111",
      "targetId": "22222222-2222-2222-2222-222222222222",
      "properties": {}
    }
  ]
}
```

---

## 28. Graph Semantics Inside `.lore`

A `.lore` document can be interpreted as:

```text
V = Entities
E = Relationships
G = (V, E)
```

The JSON structure provides a storage/interchange representation of that graph.

The semantics come from:

```text
entity IDs
+
relationship source IDs
+
relationship target IDs
+
relationship type
```

---

## 29. Entity Table Concept

The `entities` collection can be thought of as:

| ID | Name | Type |
|---|---|---|
| A | Avaria | Kingdom |
| B | Valor | City |

The relationships then refer to those IDs.

This creates a normalized graph representation.

---

## 30. Relationship Table Concept

The `relationships` collection can be thought of as:

| ID | Type | Source | Target |
|---|---|---|---|
| R1 | capital_of | A | B |

Additional relationship properties extend the edge.

---

## 31. Properties in Lore

Both:

```text
entities
```

and:

```text
relationships
```

can contain properties.

This yields two levels of metadata:

```text
Node metadata
Edge metadata
```

---

## 32. Typed Values in Lore

The typed-value categories are the same conceptual value categories used by
`.entity`:

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

Nested values are recursively encoded.

---

## 33. Nested Values in Lore

A relationship property can contain an object.

An entity property can contain a list.

The recursive value system is not limited to `.entity`.

It applies to both document families.

---

## 34. Document-Level Validation

The current `.lore` implementation validates:

```text
formatVersion
entities collection
relationships collection
entity IDs
entity names
entity properties
relationship IDs
relationship types
relationship endpoints
relationship properties
typed property values
```

This produces a stronger structural contract than merely parsing JSON.

---

## 35. Invalid Entity Example

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "name": "Invalid"
}
```

The current `.lore` rules reject a GUID-empty entity.

---

## 36. Invalid Relationship Example

```json
{
  "id": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
  "type": "controls",
  "sourceId": "11111111-1111-1111-1111-111111111111",
  "targetId": "99999999-9999-9999-9999-999999999999",
  "properties": {}
}
```

If the target ID is absent from `entities`, the relationship is invalid.

---

## 37. Empty Relationship Type

A relationship with:

```json
{
  "type": ""
}
```

is invalid under the current reference validation.

Relationship types are semantic identifiers and therefore must contain usable
information.

---

## 38. Property Type Validation

A property declared:

```json
{
  "type": "Guid",
  "value": true
}
```

is invalid because the JSON representation does not match the declared type.

Typed values must remain internally consistent.

---

## 39. Format Version as a Contract

`formatVersion` is not decorative metadata.

It determines which document rules a consumer should apply.

This principle supports:

```text
version detection
compatibility checks
migration
controlled evolution
```

---

## 40. `.lore` Storage

The current engine provides a dedicated lore storage abstraction.

Conceptually:

```text
OrbGraph
  ↓
LoreSerializer
  ↓
LoreStorage
  ↓
.lore file
```

and:

```text
.lore file
  ↓
LoreStorage
  ↓
LoreSerializer
  ↓
OrbGraph
```

The storage abstraction does not redefine the graph model.

---

## 41. Serialization Round Trip

The intended cycle is:

```text
Graph
  ↓
Serialize
  ↓
.lore JSON
  ↓
Deserialize
  ↓
Graph
```

The semantic graph should survive the round trip.

This includes:

```text
entity IDs
entity data
properties
relationship IDs
relationship endpoints
relationship properties
typed values
nested values
```

---

## 42. Graph Reconstruction

Deserialization reconstructs:

```text
entities first
relationships second
```

This ordering is important because relationships require valid endpoints.

An implementation may use another internal order as long as the resulting graph
is semantically equivalent and invalid references are not silently accepted.

---

## 43. Relationship Reconstruction

For each relationship:

```text
sourceId
targetId
```

must resolve to entities already reconstructed into the graph.

Otherwise deserialization must fail.

---

## 44. Relationship Metadata Preservation

Relationship properties are reconstructed as properties on the relationship
object itself.

They should not be silently moved onto the source or target entity.

This preserves the graph's semantic distinction between:

```text
node metadata
```

and:

```text
edge metadata
```

---

## 45. Entity Ordering

The `.lore` format uses an array for entities.

The format should not assign semantic meaning to array position.

Entity identity comes from:

```text
id
```

not:

```text
array index
```

---

## 46. Relationship Ordering

The `.lore` format uses an array for relationships.

Relationship identity comes from:

```text
id
```

not:

```text
array index
```

Applications should avoid using serialized order as semantic meaning unless an
application-specific specification explicitly introduces such semantics.

---

## 47. Graph Connectivity

A `.lore` document can describe:

```text
one connected component
```

or:

```text
multiple disconnected components
```

Example:

```text
A ──> B

C ──> D
```

This is still one `.lore` document containing one graph with multiple connected
components.

The format does not require the graph to be fully connected.

---

## 48. Orphans

An entity with no relationships is valid.

Example:

```text
A
```

within:

```text
.lore
```

is a legitimate graph state.

The graph does not require every entity to participate in an edge.

---

## 49. Dangling Relationships

A relationship with a missing endpoint is not a valid V1 `.lore` graph.

This distinction matters because an application may allow unresolved references
at a higher layer, but the current core `.lore` serializer does not treat them
as valid graph relationships.

---

## 50. Directed Graph

`.lore` describes a directed graph.

This means graph algorithms can distinguish:

```text
incoming
```

from:

```text
outgoing
```

connections.

Neighbor discovery may treat adjacency around a node symmetrically, but the
underlying relationship remains directional.

---

## 51. Traversal Semantics

When a `.lore` graph is loaded into the current engine, traversal follows outgoing
relationships.

Thus:

```text
A ──> B
```

allows a traversal from `A` to `B`.

It does not create reverse traversal automatically.

---

## 52. Reachability Semantics

Reachability similarly follows outgoing paths.

Example:

```text
A ──> B ──> C
```

gives:

```text
A → C = reachable
C → A = not reachable
```

unless another directed path exists.

---

## 53. Neighbor Semantics

Neighbor discovery checks both endpoint sides.

Example:

```text
A ──> B
C ──> A
```

makes both:

```text
B
C
```

neighbors of `A`.

This distinction is important when documenting graph behavior.

---

## 54. Cascading Deletion

The current graph implementation removes relationships connected to an entity
when that entity is removed.

Therefore, after loading a `.lore` document into the reference engine:

```text
remove entity
```

also means:

```text
remove all incident relationships
```

A compatible implementation should document whether it follows the same behavior.

---

## 55. Validation as a Safety Boundary

The `.lore` format is not simply:

```text
"some JSON that looks plausible"
```

It is:

```text
versioned JSON
+
graph invariants
+
typed-value invariants
```

This makes validation part of interoperability.

---

## 56. Current Value Model in `.lore`

The current engine's canonical public categories are:

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

Nested floating-point CLR values can be represented through decimal normalization
plus subtype metadata.

---

## 57. `.lore` and `.entity` Relationship

The two formats are complementary:

```text
.entity
    ↓
one entity

.lore
    ↓
many entities + relationships
```

An application can use `.entity` documents as reusable entity units and `.lore`
documents as graph snapshots.

---

## 58. Extracting an Entity

An implementation may load a `.lore` graph and construct an `.entity`
representation for an individual node.

The relationship context is not part of the standalone entity document.

This gives:

```text
graph node
→ standalone entity document
```

while preserving the distinction between node data and graph topology.

---

## 59. Importing Entities into Lore

An application may load an `.entity` and later add it to a graph.

The entity becomes a node.

Relationships can then be created separately.

This means `.entity` is not a replacement for `.lore`.

It is a smaller document boundary.

---

## 60. Graph Snapshot Semantics

A `.lore` document should be thought of as a graph snapshot:

```text
entities at time T
+
relationships at time T
+
properties at time T
```

The format itself does not automatically impose temporal semantics.

Temporal modeling can be represented through application-defined properties or
higher-level specifications.

---

## 61. Temporal Extensions

A product may place structured temporal properties on entities or relationships.

Example:

```text
Relationship:
    start = DateTime(...)
    end   = DateTime(...)
```

Such a property does not alter the core meaning of:

```text
sourceId
targetId
type
```

without an additional specification.

---

## 62. Relationship State

Applications can also represent contextual relationship state through properties.

Example:

```text
relationship.status = "active"
```

The base format transports the information.

The application defines the domain semantics.

---

## 63. No Implicit Relationship Semantics

The string:

```text
"allied_with"
```

does not automatically grant symmetric semantics.

If an application wants:

```text
A allied_with B
=
B allied_with A
```

it must define that rule separately.

The serialized relationship remains directional.

---

## 64. Schema Evolution

Future versions may introduce new fields.

A formal schema evolution policy should specify:

```text
added fields
removed fields
renamed fields
changed semantics
migration strategy
```

Do not silently change the meaning of existing fields while retaining the same
version if interoperability depends on that meaning.

---

## 65. Unknown Fields

The current JSON serializer uses case-insensitive property handling.

That is an implementation behavior.

A formal cross-language interoperability specification may need to define
unknown-field handling independently.

Potential policies include:

```text
strict rejection
preservation
ignore-and-discard
```

The policy should be explicit.

---

## 66. Case Sensitivity

The current reference serializer is configured for case-insensitive JSON property
matching.

This is an implementation convenience.

Canonical serialized field names remain:

```text
formatVersion
entities
relationships
id
name
type
properties
sourceId
targetId
```

Writers should emit canonical names for consistent interchange.

---

## 67. JSON as Representation

`.lore` is currently represented as JSON.

The semantic architecture is not limited to JSON.

A future implementation could produce another representation while preserving
the same graph model, provided a separate interoperability profile defines it.

---

## 68. File Extension

The conventional extension is:

```text
.lore
```

The extension identifies the complete graph document family.

The format version remains necessary because an extension alone cannot define
schema revision.

---

## 69. Error Model

A `.lore` consumer should distinguish:

```text
invalid JSON
```

from:

```text
valid JSON but invalid Orbis graph
```

Both are errors, but they occur at different validation layers.

---

## 70. Parser Boundary

A useful conceptual pipeline is:

```text
bytes
 ↓
text
 ↓
JSON parser
 ↓
document model
 ↓
Orbis validation
 ↓
graph reconstruction
```

An implementation may combine stages internally, but the semantic boundaries
remain useful for diagnostics.

---

## 71. Serializer Boundary

The opposite pipeline is:

```text
graph
 ↓
graph validation
 ↓
document projection
 ↓
JSON serialization
 ↓
text / file
```

Validation before serialization helps prevent invalid graphs from being emitted
as supposedly valid `.lore` documents.

---

## 72. Document Projection

The document contains enough information to reconstruct:

```text
entity identity
entity data
relationship identity
relationship topology
relationship data
```

Internal runtime objects do not have to be serialized one-to-one with their
implementation representation.

---

## 73. Public Model Versus Serialization Plumbing

The architecture is concerned with:

```text
OrbGraph
OrbEntity
OrbRelationship
OrbProperty
OrbValue
```

Serialization helper objects are implementation details.

An interoperable implementation need not reproduce the internal helper class
structure of Orb Engine.

---

## 74. Current Reference API Concepts

The current engine exposes graph operations conceptually corresponding to:

```text
add entity
remove entity
find entity
add relationship
remove relationship
find relationship
incoming relationships
outgoing relationships
neighbors
traversal
reachability
validation
```

This document specifies the data model rather than requiring identical method
names.

---

## 75. Relationship Integrity Example

Valid:

```text
A ──R1──> B
B exists
A exists
R1 exists
```

Invalid:

```text
A ──R1──> Z
Z missing
```

The second document must be rejected under current V1 rules.

---

## 76. Multiple Connected Components

Valid `.lore`:

```text
A ──> B

C ──> D

E
```

This graph contains:

```text
component 1 = A, B
component 2 = C, D
component 3 = E
```

The document remains one `.lore` file.

---

## 77. Large Graphs

The architecture does not prescribe a maximum number of:

```text
entities
relationships
properties
```

Practical limits depend on implementation and storage.

A product should document resource constraints separately.

---

## 78. Performance Independence

The conceptual graph does not require a particular indexing strategy.

Possible implementations may use:

```text
hash maps
database indexes
adjacency lists
graph databases
custom indexes
```

The specification defines semantics, not internal complexity guarantees.

---

## 79. Query Independence

`.lore` does not embed a universal query language.

Applications may query loaded graphs according to their own capabilities.

The document merely provides structured graph information from which queries
can be performed.

---

## 80. Application-Level Schemas

A product can impose a schema:

```text
Character requires age
Kingdom requires population
Relationship rules requires start/end
```

Such rules are above the base `.lore` specification.

This keeps the core format general-purpose.

---

## 81. Domain Packages

An ecosystem may define domain profiles such as:

```text
Orbis Worldbuilding Profile
Orbis Research Profile
Orbis Organization Profile
```

Each profile can define allowed types and properties without changing the base
graph fundamentals.

---

## 82. User-Owned Knowledge

A `.lore` file should be usable as a portable knowledge representation.

Applications should avoid hiding core graph semantics exclusively in private
database tables when an interoperable `.lore` representation is available.

---

## 83. Round-Trip Fidelity Principle

A `.lore` round trip should preserve:

```text
graph topology
entity identity
relationship identity
property identity
typed values
nested values
```

Lossy transformations should be documented.

---

## 84. Invalid Mutation Principle

A failed relationship insertion must not silently leave:

```text
half a relationship
```

inside the graph.

The current engine explicitly tests that failed mutations do not leave corrupted
partial graph state.

---

## 85. Conformance Levels

A `.lore` implementation can document conformance such as:

```text
L1 — Parse
L2 — Validate
L3 — Round-trip
L4 — Graph operations
L5 — Full V1 behavioral compatibility
```

These are suggested documentation levels, not current official certification tiers.

---

## 86. `.lore` Conformance Checklist

- [ ] Supports `formatVersion`.
- [ ] Loads entities.
- [ ] Loads relationships.
- [ ] Preserves entity IDs.
- [ ] Preserves relationship IDs.
- [ ] Validates endpoint existence.
- [ ] Validates duplicate IDs.
- [ ] Validates relationship type.
- [ ] Validates typed properties.
- [ ] Supports nested values if claiming V1 full compatibility.
- [ ] Preserves self-links.
- [ ] Preserves relationship metadata.
- [ ] Supports empty graphs if claiming full V1 document compatibility.
- [ ] Round-trips topology without silent loss.

---

## 87. `.lore` Versus Database Tables

A relational backend can represent the same data as:

```text
Entities
Relationships
Properties
```

That does not change the conceptual `.lore` model.

The JSON file is an interchange representation.

The implementation can use another internal storage model.

---

## 88. `.lore` Versus Graph Databases

A graph database may provide:

```text
indexes
transactions
distributed storage
parallel queries
```

None of those are required by the core `.lore` representation.

A `.lore` implementation can be lightweight or backed by a large system.

---

## 89. `.lore` as Portable Graph State

The intended long-term role of `.lore` is to make connected knowledge portable:

```text
Application A
     ↓
   .lore
     ↓
Application B
     ↓
Different UI
```

The graph should remain recognizable across applications that implement the
same architecture.

---

## 90. Architecture and Implementation Freedom

This document intentionally gives implementation authors room to choose:

```text
language
runtime
database
UI
serialization library
graph algorithms
deployment model
```

The MIT license covers the specification material.

AGPL applies separately to Orb Engine code.

---

## 91. Current Reference Summary

The current V1 engine models `.lore` as:

```text
formatVersion
    +
entities[]
    +
relationships[]
```

Each entity contains:

```text
id
name
type
properties
```

Each relationship contains:

```text
id
type
sourceId
targetId
properties
```

---

## 92. Architectural Invariants Summary

The essential rules are:

```text
Every entity has a unique ID.
Every relationship has a unique ID.
Every relationship has a non-empty type.
Every relationship source exists.
Every relationship target exists.
Every property has a name and typed value.
```

---

## 93. Reference Implementation Notes

The current Orb Engine implementation additionally provides:

```text
graph validation
graph traversal
reachability
neighbor discovery
storage
serialization
round-trip testing
```

These are implementation capabilities built around the architectural model.

They do not need to be reproduced as source code to understand `.lore`.

---

## 94. Why `.lore` Exists

`.lore` solves a different problem from `.entity`.

`.entity` answers:

> What is this one object?

`.lore` answers:

> What does this connected graph of objects look like?

This distinction keeps document boundaries useful.

---

## 95. Example Domain

```text
Avaria
   │
   │ capital_of
   ▼
Valor

Avaria
   │
   │ language
   ▼
Avarian
```

The relationship belongs to graph topology.

The language belongs to entity properties.

These are deliberately different semantic channels.

---

## 96. Example Edge Metadata

```text
Avaria ──capital_of──> Valor

relationship:
    since = 812
    status = active
```

The metadata describes the connection.

It does not become an attribute of `Avaria` merely because `Avaria` is the source.

---

## 97. Example Multiple Edges

```text
A ──controls──> B
A ──visits────> B
A ──allied_with-> B
```

The graph can preserve all three as distinct relationship objects.

---

## 98. Example Cycle

```text
A ──> B
B ──> C
C ──> A
```

The document is valid.

Traversal must use cycle protection.

---

## 99. Example Isolated Node

```text
A
```

The document is valid as long as the entity itself satisfies the V1 document rules.

---

## 100. Final `.lore` Statement

> **A `.lore` document is a versioned, portable representation of an Orbis graph,
> containing uniquely identifiable entities and directed relationships whose
> endpoints resolve within the same document, with typed metadata preserved on
> both nodes and edges.**

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
