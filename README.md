# High Quality Data Model <!-- omit in toc -->

The High Quality Data Model (HQDM) is a well-documented heavyweight foundational ontology, that aims to support large scale data integration across enterprises.
The original model was developed by Matthew West based on lessons learnt from his efforts with BORO and ISO 15926-2:2003.

The original documentation was produced using EXPRESS, and whilst the concepts and approach retains its significance, approaches like semantic web have overtaken in popularity with more tooling and support.

> [!NOTE]
> This repository provides a linked data version representation of HQDM in RDF(S), converted from the original EXPRESS schema to take advantage of this foundational approach.

Whilst effort has been made to stay true to the source material, documentation has been produced to explain the initial migration to this form. This is found in the docs folder [here](/docs/TheMigrationToSemanticWeb.md).

## Documentation

HQDM is a well-documented data model within the [published book](https://shop.elsevier.com/books/developing-high-quality-data-models/west/978-0-12-375106-5) and should always be used when discussing any deviations of the model.

The main RDFS version of the model can be found in [src/ontology](./src/ontology/hqdm.ttl).

In addition, further sources are still available:

- the [EXPRESS file](https://github.com/hqdmTop/hqdmFramework/blob/main/hqdm_framework.txt)
- a [HTML version](https://hqdmtop.github.io/hqdmFramework/)
- a markdown [wiki](https://github.com/hqdmTop/hqdmFramework/wiki)

_Over-time it is anticipated that this model will be a singular reference for the model._

### Current Omissions

Whilst RDF(S) captures most of the model, relationship cardinalities are currently missing from the model.
The current use of this model should still adhere to the form in the original documentation.
Experimentation is being made with the [Shapes Constraint Language](https://www.w3.org/TR/shacl/) (SHACL) to capture this area of the model definition.
Some low-level subtype relationships have also been removed due to the better expression possible in RDF(S); mostly those with underscore permutations as described by the [migration doc](/docs/TheMigrationToSemanticWeb.md).

## Contributing

Contributions are welcome by raising issues, starting discussions or creating pull requests. Please follow the [contributing](CONTRIBUTING.md) documentation for guidance.

## License

HQDM is free and open to the public under the Creative Commons Attribution 4.0 International.
