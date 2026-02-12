---
layout: default
title: "JSON-LD Extensions for AI/ML (jsonld-ex)"
---

# JSON-LD Extensions for AI/ML (jsonld-ex)

**Status:** Draft Specification v0.1.0  
**Date:** 2026-02-12  
**Authors:** Muntaser Syed, Marius Silaghi, Sheikh Abujar, Rwaida Alssadi  
**Affiliation:** Florida Institute of Technology  
**License:** [MIT](https://opensource.org/licenses/MIT)

## Abstract

This specification defines backward-compatible extensions to [JSON-LD 1.1](https://www.w3.org/TR/json-ld11/) that enable AI/ML metadata to be embedded alongside symbolic linked data. The extensions address critical gaps in confidence representation, provenance tracking, temporal validity, vector embeddings, validation, and security — providing a rigorous, interoperable vocabulary for machine learning data exchange.

## Status of This Document

This is a **draft specification** produced by researchers at Florida Institute of Technology. It has **not** been endorsed by the W3C or any standards body. The authors intend to pursue standardization through the W3C Community Group process following peer review and community feedback.

The key words "MUST", "SHOULD", "MAY", "MUST NOT", and "SHOULD NOT" in the specification documents are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

## Namespace

| Property | Value |
|----------|-------|
| **Namespace IRI** | `https://w3id.org/jsonld-ex/` |
| **Preferred prefix** | `jex:` |
| **JSON-LD Context** | [`https://w3id.org/jsonld-ex/context/v1.jsonld`](context/v1.jsonld) |
| **Ontology (Turtle)** | [`https://w3id.org/jsonld-ex/ontology/jsonld-ex.ttl`](ontology/jsonld-ex.ttl) |

Until the [w3id.org](https://w3id.org/) permanent identifier is registered, the temporary namespace resolves via: `https://jsonld-ex.github.io/ns/`

## Specification Documents

| Document | Description |
|----------|-------------|
| [Vocabulary](vocabulary) | Complete vocabulary — all classes and properties with definitions, types, and examples |
| [Confidence Algebra](confidence-algebra) | Formal algebra for uncertainty representation and propagation, grounded in Jøsang's Subjective Logic |
| [Validation](validation) | Shape-based constraint language for JSON-LD documents |
| [Security](security) | Context integrity verification, allowlists, and resource limits |
| [Temporal](temporal) | Time-aware assertions: validity intervals and point-in-time queries |
| [Transport](transport) | CBOR-LD binary encoding and MQTT topic/QoS derivation |
| [Interoperability](interoperability) | Bidirectional mappings to PROV-O, SHACL, OWL, RDF-star, and SSN/SOSA |

## Design Principles

1. **Backward compatibility.** Every jsonld-ex document is valid JSON-LD 1.1. Standard processors treat extension terms as regular properties; extended processors interpret them with the defined semantics.
2. **Minimal footprint.** Extensions use the established `@`-keyword convention and standard JSON-LD mechanisms (value objects, context definitions). No new syntax or processing algorithms are required.
3. **Mathematical rigor.** The confidence algebra is grounded in Jøsang's Subjective Logic (2016), with formally proven properties and explicit documentation of all approximations.
4. **Interoperability.** Every extension term maps bidirectionally to at least one established standard (PROV-O, SHACL, OWL, SSN/SOSA, or RDF-star).
5. **Practicality.** The vocabulary is driven by real-world use cases in healthcare IoT, knowledge graph extraction, multi-model fusion, and sensor pipelines.

## Quick Example

```json
{
  "@context": [
    "http://schema.org/",
    "https://w3id.org/jsonld-ex/context/v1.jsonld"
  ],
  "@type": "Person",
  "name": {
    "@value": "Jane Doe",
    "@confidence": 0.98,
    "@source": "https://model.example.org/ner-v4",
    "@extractedAt": "2026-01-15T10:30:00Z",
    "@method": "NER",
    "@humanVerified": true
  }
}
```

A standard JSON-LD 1.1 processor treats `@confidence`, `@source`, etc. as regular properties mapped by the context. A jsonld-ex-aware processor interprets them with the semantics defined in the [Vocabulary](vocabulary) specification.

## Reference Implementation

| Resource | Link |
|----------|------|
| **PyPI package** | [`jsonld-ex`](https://pypi.org/project/jsonld-ex/) |
| **Source code** | [github.com/jemsbhai/jsonld-ex](https://github.com/jemsbhai/jsonld-ex) |
| **Test coverage** | 832+ passing tests |

## Relationship to Existing Standards

jsonld-ex is designed to **complement**, not compete with, existing standards:

- **PROV-O** — jsonld-ex provenance annotations map bidirectionally to PROV-O entities, agents, and activities. jsonld-ex provides a more compact inline syntax for common annotation patterns.
- **SHACL** — jsonld-ex validation shapes map to SHACL node shapes and property shapes. jsonld-ex provides a JSON-LD-native syntax that avoids the need for separate RDF-based shape graphs.
- **OWL** — jsonld-ex constraint types map to OWL class restrictions where applicable.
- **RDF-star** — jsonld-ex annotations are serializable as RDF-star embedded triples, enabling statements-about-statements in RDF 1.2 stores.
- **SSN/SOSA** — jsonld-ex IoT and sensor terms map bidirectionally to the W3C Semantic Sensor Network ontology.
- **Croissant (MLCommons)** — jsonld-ex operates at the assertion level (per-value confidence, provenance, temporal validity), complementing Croissant's dataset-level metadata for discoverability.

## Citation

If you use jsonld-ex in academic work, please cite:

> Syed, M., Silaghi, M., Abujar, S., & Alssadi, R. (2026). JSON-LD Extensions for AI/ML: Confidence-Aware Knowledge Fusion in Linked Data. *Draft specification.* https://w3id.org/jsonld-ex/

## Contact

- **Issues and feedback:** [github.com/jsonld-ex/ns/issues](https://github.com/jsonld-ex/ns/issues)
- **Main repository:** [github.com/jemsbhai/jsonld-ex](https://github.com/jemsbhai/jsonld-ex)
