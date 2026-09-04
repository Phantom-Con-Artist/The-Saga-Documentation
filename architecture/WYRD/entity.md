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

# Orbis `.entity` Specification

### The standalone document model for an individual Orbis entity.

**Orbis Project · MIT Licensed Architecture Specification**

[![Specification](https://img.shields.io/badge/specification-BETA-F0AD00?style=for-the-badge)](https://github.com/Phantom-Con-Artist/Orbis-Documentation)
[![License: MIT](https://img.shields.io/badge/Specification-MIT-0cc0df?style=for-the-badge)](../LICENSE)
[![Implementation: Orb Engine](https://img.shields.io/badge/implementation-Orb%20Engine%20AGPL--3.0-0cc0df?style=for-the-badge)](https://github.com/Phantom-Con-Artist/Orb)

</div>

---


## 1. Purpose

An `.entity` document represents one independently identifiable entity.

The architecture treats the entity as a first-class object that can exist outside
a graph and later participate in one or more graph contexts.

The format is intended to preserve:

```text
identity
name
type
properties
typed values
nested structured values
format version
```

This document describes the architectural `.entity` format and its current
reference behavior.

---

## 2. Licensing Boundary

This specification is part of **Tier I — The Orbis Project**.

It is licensed under the **MIT License**.

The specification is intentionally separate from Orb Engine's implementation.

```text
.entity specification
        │
        └── MIT

Orb Engine implementation
        │
        └── AGPL-3.0
```

This document does not grant or alter rights to Orb Engine source code.

A developer may independently implement `.entity` support using this MIT-licensed
specification.

---

## 3. What an `.entity` Document Is

An `.entity` document is the serialized representation of one entity.

Conceptually:

```text
Entity
  ↓
.entity document
```

and:

```text
.entity document
  ↓
Entity
```

The format does not require the entity to already belong to a `.lore` graph.

This makes `.entity` appropriate for:

- Individual records.
- Entity libraries.
- Independent entity editing.
- Import/export.
- Temporary entity construction.
- Cross-application exchange.

---

## 4. Conceptual Model

An entity consists of:

```text
Entity
├── Identity
├── Name
├── Type
└── Properties
```

### Identity

A stable GUID.

### Name

A human-readable label.

### Type

An optional classification.

### Properties

A collection of named typed values.

---

## 5. Canonical Top-Level Structure

The current `.entity` representation uses this conceptual JSON shape:

```json
{
  "formatVersion": 1,
  "id": "GUID",
  "name": "Entity Name",
  "type": "Entity Type",
  "properties": {}
}
```

The exact field names are:

```text
formatVersion
id
name
type
properties
```

Consumers should preserve these names for format compatibility.

---

## 6. `formatVersion`

`formatVersion` identifies the document format revision.

The current reference implementation uses:

```text
formatVersion = 1
```

The field is required for current deserialization.

A current engine instance rejects an unsupported format version instead of silently
interpreting it.

This makes version handling explicit.

---

## 7. `id`

`id` is the unique identity of the entity.

The current engine expects a non-empty GUID.

Example:

```json
{
  "id": "1fa3a1b2-c2e5-42d7-8d1b-1f4cc2a8e15a"
}
```

The identifier should be treated as opaque.

Applications should not encode business meaning into the GUID unless they own
that convention independently.

---

## 8. Identity Semantics

Changing:

```text
name
type
properties
```

does not inherently change:

```text
id
```

The ID identifies the entity.

Therefore:

```text
same ID + changed name
```

represents the same entity with updated descriptive information.

Where an application needs immutable identities, that is a higher-level policy.

---

## 9. `name`

`name` is the human-readable identity label.

The current engine model permits a nullable name.

For interoperability, applications should generally provide a meaningful name
when one exists.

The name should not be used as the primary graph reference.

Do not assume:

```text
"name" == unique identity
```

unless the application explicitly imposes that rule.

---

## 10. `type`

`type` is an optional classification.

Examples:

```text
Character
City
Kingdom
Organization
Artifact
Concept
```

It is a semantic label, not a required global ontology.

Different applications may use different type vocabularies.

---

## 11. `properties`

`properties` is a JSON object whose keys identify property names.

Each property contains:

```text
type
value
```

Example:

```json
{
  "properties": {
    "language": {
      "type": "String",
      "value": "Avarian"
    }
  }
}
```

---

## 12. Property Names

Property names must not be empty.

The current implementation also treats the property's dictionary key and its
internal property name as the same identity.

Conceptually:

```text
"population"
   ↓
Property.Name = "population"
```

An implementation should not create a hidden second naming system.

---

## 13. Property Type

The property `type` identifies the canonical Orb value category.

Current canonical categories are:

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

The type name is serialized as text.

---

## 14. Property Value

The `value` field contains the serialized representation appropriate for the
declared type.

Examples:

```text
String   → JSON string
Boolean  → JSON true/false
Integer  → JSON integer number
Decimal  → JSON decimal-compatible number
DateTime → JSON string
Guid     → JSON string
List     → JSON array
Object   → JSON object
Null     → JSON null
```

The declared type and the JSON token must agree.

---

## 15. Null

A null property is explicitly represented by:

```json
{
  "type": "Null",
  "value": null
}
```

The current engine rejects a non-null JSON value declared as `Null`.

---

## 16. String

Example:

```json
{
  "type": "String",
  "value": "Avarian"
}
```

A string value must be a JSON string.

---

## 17. Boolean

Example:

```json
{
  "type": "Boolean",
  "value": true
}
```

The JSON value must be a boolean token.

---

## 18. Integer

Example:

```json
{
  "type": "Integer",
  "value": 42
}
```

The current implementation uses signed 64-bit integer semantics as the canonical
integer representation.

---

## 19. Decimal

Example:

```json
{
  "type": "Decimal",
  "value": 19.95
}
```

The current implementation uses decimal semantics for the canonical `Decimal`
category.

Nested floating-point primitives can be normalized to this category with
additional CLR subtype metadata.

---

## 20. DateTime

A date-time property is represented as a JSON string that the implementation can
parse as a valid date-time value.

Example:

```json
{
  "type": "DateTime",
  "value": "2026-09-01T12:30:00"
}
```

Consumers should use a documented interoperable date-time representation and
should not assume that arbitrary free-form strings are valid.

---

## 21. Guid

A GUID property is represented as a JSON string containing a valid GUID.

Example:

```json
{
  "type": "Guid",
  "value": "1fa3a1b2-c2e5-42d7-8d1b-1f4cc2a8e15a"
}
```

---

## 22. List

Lists are arrays containing recursively typed nested values.

Conceptually:

```text
List
├── Integer
├── String
├── Object
└── List
```

The implementation preserves nested type information rather than assuming
the JSON array alone provides enough semantic information.

---

## 23. Object

Objects are string-keyed collections whose values are recursively typed.

Conceptually:

```text
Object
├── name
├── age
└── active
```

Each value remains typed.

---

## 24. Nested Value Representation

For nested list and object values, the current engine uses typed nested records
containing metadata equivalent to:

```json
{
  "Type": "Integer",
  "ClrType": "Int32",
  "Value": 42
}
```

or:

```json
{
  "Type": "String",
  "ClrType": null,
  "Value": "Avarian"
}
```

The nested document metadata allows the implementation to preserve CLR subtype
information where necessary.

An independent implementation can use a compatible representation or explicitly
document a different architectural revision.

---

## 25. Floating-Point Nested Values

Current nested serialization can encounter CLR:

```text
Single
Double
```

values.

They are normalized to:

```text
OrbValueType.Decimal
```

with subtype metadata such as:

```text
Single
Double
```

This is important because there is no separate public top-level `Double` enum
member in the current engine implementation.

---

## 26. Nested Integer Fidelity

Nested integer primitives can be normalized to the canonical integer category
while preserving CLR subtype metadata such as:

```text
Byte
SByte
Int16
UInt16
Int32
UInt32
Int64
UInt64
```

This allows a round trip to restore the original compatible CLR primitive
where the encoded value can be represented safely.

---

## 27. Recursive Structure

A nested object may contain a list.

A list may contain an object.

An object may contain another object.

Example:

```text
Object
└── biography
    └── milestones
        ├── Object
        │   ├── year
        │   └── title
        └── Object
            ├── year
            └── title
```

The recursion is part of the data model.

---

## 28. Example Complete `.entity`

```json
{
  "formatVersion": 1,
  "id": "1fa3a1b2-c2e5-42d7-8d1b-1f4cc2a8e15a",
  "name": "Avaria",
  "type": "Kingdom",
  "properties": {
    "language": {
      "type": "String",
      "value": "Avarian"
    },
    "population": {
      "type": "Integer",
      "value": 2400000
    },
    "independent": {
      "type": "Boolean",
      "value": true
    }
  }
}
```

---

## 29. Minimal `.entity`

A minimal valid document needs the format version, entity identity, and a valid
property container.

Conceptually:

```json
{
  "formatVersion": 1,
  "id": "1fa3a1b2-c2e5-42d7-8d1b-1f4cc2a8e15a",
  "properties": {}
}
```

The current serializer model allows `name` and `type` to be nullable.

Applications may impose stricter domain requirements.

---

## 30. Entity Validation

The reference implementation validates:

```text
formatVersion
id
properties
property names
property types
serialized property values
```

A malformed entity should be rejected.

The serializer does not treat arbitrary JSON as a valid `.entity` merely because
the JSON parser accepts it.

---

## 31. Format Version Validation

Current reference behavior:

```text
formatVersion == 1
    ↓
supported

formatVersion != 1
    ↓
unsupported
```

This gives applications a deterministic way to reject documents they cannot
interpret correctly.

---

## 32. Property Validation

Invalid examples include:

```text
empty property name
null property document
missing type
unknown type
type/value mismatch
```

Example:

```json
{
  "type": "Integer",
  "value": "forty-two"
}
```

is invalid because the value is textual while the declared type is Integer.

---

## 33. Type Safety

The format deliberately separates:

```text
"type"
"value"
```

This avoids making consumers guess whether:

```text
42
```

means:

```text
Integer
Decimal
String
```

The schema itself carries the semantic answer.

---

## 34. Round-Trip Fidelity

The intended serialization process is:

```text
Entity
  ↓
Serialize
  ↓
.entity JSON
  ↓
Deserialize
  ↓
Entity
```

The semantic content should survive this cycle.

The current engine tests nested values, GUIDs, date-time values, primitive numeric
types, lists, objects, and typed values as part of round-trip behavior.

---

## 35. Standalone Entity Storage

The reference engine can persist an individual entity document independently
from a graph.

Conceptually:

```text
Entity
  ↓
EntityStorage
  ↓
.entity file
```

and:

```text
.entity file
  ↓
EntityStorage
  ↓
Entity
```

Storage is separate from the conceptual `.entity` format.

---

## 36. File Extension

The conventional file extension is:

```text
.entity
```

The extension identifies the document kind.

The extension does not replace `formatVersion`.

Both are useful:

```text
.entity
+
formatVersion
```

---

## 37. Text Encoding

The reference implementation serializes the document as JSON text.

An interoperable ecosystem should standardize encoding policy separately if a
formal cross-platform interchange profile is required.

---

## 38. Whitespace

Whitespace is not semantically significant to JSON parsing.

The reference implementation emits indented JSON for readability.

A consumer should not attach semantic meaning to indentation or line breaks.

---

## 39. Property Order

Property order should not be treated as semantic.

Consumers should retrieve properties by key rather than by their serialized
position.

---

## 40. Unknown Properties

Applications extending the model should consider how unknown properties are
preserved.

A strict consumer may reject unknown fields.

A tolerant consumer may preserve them.

The behavior should be documented by the interoperability profile.

---

## 41. Entity Type Registries

A product may define:

```text
Character
Location
Faction
Artifact
```

as a controlled registry.

That registry is outside the base `.entity` document requirement.

The core format stores the value.

Higher-level semantics define what the value means.

---

## 42. Domain-Specific Properties

A property such as:

```text
population
```

is not part of the universal Orbis architecture.

It is an example of application-level data.

The format exists to carry such information without requiring the base engine
to understand every domain.

---

## 43. Relationship-Free Entity Documents

An `.entity` document does not contain graph relationships.

That is intentional.

If relationships are needed, they belong to the graph / `.lore` representation.

An entity document therefore remains portable and self-contained.

---

## 44. Reference Semantics

An entity document may contain a GUID property that refers to another object.

That does not create a graph relationship automatically.

For example:

```text
property:
    mentorId = GUID(...)
```

is merely a typed property unless the application defines additional semantics.

A relationship becomes graph-structural only when represented as a relationship.

---

## 45. Entity Equality

The architecture does not require object reference equality.

Identity should be understood primarily through:

```text
entity.id
```

Two deserialized instances with the same valid ID can represent the same
logical entity even if they are different runtime objects.

---

## 46. Mutation

Entity properties may be mutable.

Changing a property does not change the entity's identity.

Applications may impose immutable policies above the format.

---

## 47. Interchange Principle

A valid `.entity` should be understandable without opening the application's
source code.

That is a core reason for explicit field names and typed values.

---

## 48. Current Reference Behavior

The current implementation uses:

```text
JSON
formatVersion = 1
Guid identity
optional name
optional type
typed property values
recursive nested values
```

This section describes behavior, not implementation source code.

---

## 49. Independent Implementation Guidance

An independent implementation should separate:

```text
Document parser
Entity model
Typed value model
Validation
Storage
```

The architecture does not require these to be separate classes.

It requires the semantic boundaries to remain understandable.

---

## 50. Version Evolution

A future `.entity` revision may add:

```text
new fields
new value types
new metadata
new structural features
```

Such changes should increment the format version when they change interpretation
in an incompatible way.

---

## 51. Compatibility Statement

An implementation claiming `.entity` V1 compatibility should state:

```text
Supported formatVersion: 1
Supported canonical value types: ...
Nested value support: ...
Unknown-field behavior: ...
```

This makes interoperability measurable instead of rhetorical.

---

## 52. `.entity` Conformance Checklist

- [ ] `formatVersion` is recognized.
- [ ] Entity ID is parsed as a GUID.
- [ ] Entity identity is stable.
- [ ] Properties are represented by names.
- [ ] Each property provides a type.
- [ ] Type/value combinations are validated.
- [ ] Nested lists are supported if claimed.
- [ ] Nested objects are supported if claimed.
- [ ] GUID values round-trip correctly.
- [ ] DateTime values round-trip correctly.
- [ ] Integer values remain semantically integer.
- [ ] Invalid documents are rejected deterministically.

---

## 53. Architecture Versus Orb Engine

The `.entity` architecture is MIT-licensed.

The reference implementation that currently serializes and deserializes `.entity`
documents belongs to Orb Engine and is AGPL-3.0 licensed.

The distinction is:

```text
Specification     → MIT
Implementation    → AGPL-3.0
```

This document intentionally describes the first.

---

## 54. Final Statement

> **An `.entity` document is the portable, versioned representation of one
> identifiable Orbis entity, carrying optional classification and a collection
> of explicitly typed, recursively structured properties.**

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
