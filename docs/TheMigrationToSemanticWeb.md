# Introduction

This file details changes that were made to the HQDM model whilst converting from EXPRESS to this [semantic web](https://en.wikipedia.org/wiki/Semantic_Web) version.

Whilst the conversion aimed to stay faithful to the original model definition for migration purposes of existing users, there were known limitations and EXPRESS workarounds that have been addressed.

# Background

Chapter 17 of [Developing High Quality Data Models](https://shop.elsevier.com/books/developing-high-quality-data-models/west/978-0-12-375106-5) contains a foundational data model.
Whilst a [HTML version](https://github.com/hqdmTop/hqdmFramework) and a [wiki](https://github.com/hqdmTop/hqdmFramework/wiki) are good documentation sources of the model at the time of producing this RDF(S) version, the current master model source is still based upon EXPRESS that is less accessible and expressive compared to semantic web approaches for information modelling.

This original model was documented throughout the book which comprised of a complete model structure using both EXPRESS and EXPRESS-G.
Any queries or inconsistencies with the model should be resolved referring to the book as a primary source.

# Model Conversion and Refinements

During the conversion process, minor inconsistencies identified in expression of the original model have been addressed while transforming the model into RDFS.
Modeling in RDFS has a different formal structure to EXPRESS, which also has resulted in some representational differences.
Additionally, the initial release of this model leaves further opportunities at better encapsulating the ideas and concepts in the model for future iterations to aid migration from other users and systems to this model style.

Some areas of the EXPRESS model were chosen to not be incorporated with the first RDFS version, whilst other areas have been improved. For example, relationship cardinalities are not yet captured, but the relationship hierarchy structure is now formally included. The use of [Shapes Constraint Language (SHACL)](https://www.w3.org/TR/shacl/) is being explored to capture the remaining aspects of the model.

# The Changes

As part of formally evidencing the model and any changes made to it, initial changes from EXPRESS to RDFS are documented below. Where possible these are reflected back into the [origional EXPRESS file](https://github.com/hqdmTop/hqdmFramework/blob/main/hqdm_framework.txt).

- Due to EXPRESS limitations, relationships were not clearly grounded in the model. E.g. `hqdm:partOfByClass` first introduced with domain and range `hqdm:ClassOfSpatioTemporalExtent`.
  These have all been rectified following the research of a [Core Constructional Ontology (CCO)](https://gateway.newton.ac.uk/sites/default/files/asset/doc/2105/Salvatore%20Florio.pdf) grounding all relation sets to primitive logic constructs.
  The use of `rdfs:subPropertyOf` now captures this structure.

- Many relationships used combinations of additional underscores to capture the models intent and also used redeclared types through EXPRESS `SELF`.
  These have been been reduced to its first declared use with all further restrictions to be populated using SHACL.

- HQDM defined a metamodel for `Relationship` which has been deprecated in favour of the approach from the CCO.
  Implementation systems will continue to determine the way entities will be handled, however `hqdm:Relationship` and `hqdm:ClassOfRelationship` are left defined as a core element.
  This model now grounds its sole binary `universalRelationSet` from `rdf:Property`as is more commonly practiced with ontologies.
  This results in the following deprecations: `defined_relationship`, `aggregation`, `composition`, `temporal_composition`, `classification` and `specialization`.
  If `Relationship` class elements are required, then these are documented as both styles in full within the book.

- Some of the supertype structure has been identified as missing so the below is now included:

  - `hqdm:ClassOfRepresentation rdfs:subClassOf hqdm:ClassOfAssociation`
  - `hqdm:KindOfFunctionalSystem rdfs:subClassOf hqdm:KindOfOrdinaryFunctionalObject`
  - `hqdm:KindOfFunctionalSystemComponent rdfs:subClassOf hqdm:KindOfFunctionalObject`
  - `hqdm:KindOfBiologicalSystem rdfs:subClassOf hqdm:KindOfOrdinaryBiologicalObject`
  - `hqdm:KindOfBiologicalSystemComponent rdfs:subClassOf hqdm:KindOfBiologicalObject`
  - `hqdm:KindOfActivity rdfs:subClassOf hqdm:KindOfIndividual`
  - `hqdm:KindOfAssociation rdfs:subClassOf hqdm:KindOfIndividual`

- Inverse relationships as used in HQDM that are not currently captured due to not being supported by the RDFS specification. `skos:scopeNote`\`s have been used to declare these. Inverse relationships are mostly for modelling ease, however may not be required for interoperability purposes. This may be replaced with SHACL or simplified in the future.

- EXPRESS could declare ABSTRACT entities, however the term is used in many different contexts and as such ambiguous about its intention. These declarations are being deprecated which only affects three parts of the model:

  - Relationship - This is considered a fundamental construct so is a change that brings closer alignment to other foundation models such as BORO.
  - Party - The intention of HQDM was to avoid using `hqdm:Party` in favour of `hqdm:Person` or `hqdm:Organisation`. This is considered minor and in some instances overly restrictive as in some situations it is known a party must exist, but not yet whether that is a person or organisation.
  - `hqdm:AbstractObject` as a defined top-level entity is left in the initial RDFS model for migration purposes, however is being considered to be fully deprecated in a future version.

## Known Areas to be Explored Further

The initial release of the RDFS data model has stayed true to the HQDM reference material both to better document the work Matthew West provided to this field, and also aid existing systems that wish to migrate to this version of the model.
That said, there are ongoing discussions at the time of writing looking to explore the model further when example information is available prior to any changes being made:

- Within the sign pattern, the whole-life individual `hqdm:Sign` participates rather than just a state of the sign as is seen for other HQDM's objects with the `StateOfX` being the participant. This may be valid, however could also need a new subclass extending from `hqdm:StateOfSign` as the participant.

- The later parts of HQDM includes several model extensions to help convey understanding of the approach described. Whilst correct, this area of the model is not known to have been actively tried, therefore needs exploration when opportunities arise to test this semantic web approach.
