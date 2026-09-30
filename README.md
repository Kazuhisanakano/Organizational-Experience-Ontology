# Organizational Experience Ontology (OEO)

OEO represents event individuation and polyvocal interpretation in organizational records. It distinguishes shared **Scenes** and **QualitativeChanges** from actor-individuated **RecognizedEvents**, and records **InterpretationActs** with provenance and interpretive context.

This repository provides the core ontology, its SHACL constraints, and seven SPARQL queries accompanying the paper:

> *Toward Polyphonic Organizations: An Ontology for Event Individuation and Polyvocal Interpretation*

## Scope of this release

This release includes the core ontology, SHACL constraints, seven primary SPARQL queries, the Enron annotation graph, a readable annotation export, supporting extension modules, and recorded evaluation results. It also includes four supplementary queries and the graph mutations specifying four controlled cases.

Source e-mail bodies, the extraction pipeline, and a complete automated execution environment are not distributed. The RDF and JSON contain selected source quotations and provenance identifiers. The supplied graph supports validation and query execution; independent reconstruction from the original corpus requires the source data and extraction/annotation procedure. Recorded result files are historical outputs. During packaging, all eleven queries were rerun with matching row counts and SHACL conformance was confirmed. HermiT was not rerun during packaging.

The OWL and SHACL modules retain their existing internal version identifier, **0.2.1**. Filenames are stable and omit development-folder version suffixes. The `https://example.org/oe#` namespace is retained to preserve compatibility with the evaluated artifacts; it is an identifier used in these files, not a claim that a resolvable ontology service is hosted at that address.

## Files

| File | Purpose |
| --- | --- |
| `ontology/oeo.ttl` | Core OWL ontology: classes, properties, hierarchy, domains, ranges, and logical axioms. |
| `ontology/oeo-shapes.ttl` | SHACL constraints for explicitly recorded data. Includes SHACL-SPARQL constraints. |
| `queries/cq01-event-individuation.rq` | CQ1: retrieve the actor, focal change, core context, and event type. |
| `queries/cq02-focal-core-reversal.rq` | CQ2: retrieve event pairs that reverse focal and core roles within a shared Scene. |
| `queries/cq03-same-wording-different-interpretations.rq` | CQ3: retrieve statements with identical wording but differing interpretive attributes. |
| `queries/cq04-provenance-and-revision.rq` | CQ4: retrieve interpretation agents, times, reinterpretations, and statement revisions. |
| `queries/cq05-coexisting-interpretations.rq` | CQ5: retrieve coexisting interpretation types, temporal orientations, and contexts by Scene. |
| `queries/cq06-interpretation-worldviews.rq` | CQ6: retrieve Worldviews recorded for InterpretationActs; absent values remain unbound. |
| `queries/cq07-relational-interpretations.rq` | CQ7: retrieve relational interpretations, the acts they relate, their agents, and statements. |

The CQ numbers refer to the seven operationalized questions in the revised paper. They do not imply exhaustive coverage of all possible ontology requirements.

## Modeling overview

- A **QualitativeChange** is associated with a Scene through `oe:occursIn`.
- A **RecognizedEvent** is linked to its individuating Agent and classified by an EventType.
- Four properties relate a RecognizedEvent to QualitativeChanges: `oe:hasFocalPart`, `oe:hasCoreContext`, `oe:hasCharacterizingContext`, and `oe:hasExternalContext`. These describe roles relative to an event, rather than fixed categories of changes.
- An **InterpretationAct** interprets a RecognizedEvent and is associated with an Agent. An InterpretationStatement is linked to the act through `prov:wasGeneratedBy`.
- A **Worldview** is recorded through `InterpretationAct -> oe:basedOn -> Worldview`. This relation is optional. Neither `orientedBy` nor `holds` is included as an OEO property in this core release. A missing Worldview link means that no Worldview was recorded, not that none exists.
- A **RelationalInterpretation** is a kind of InterpretationAct that relates other InterpretationActs through `oe:relatesInterpretations`.

The files reuse selected terms from PROV-O, HiCO, SKOS, and ORG. They include selected declarations and hierarchy axioms rather than importing these vocabularies wholesale.

## Using the files

### OWL reasoning

Load `ontology/oeo.ttl` and, when assessing populated data, the relevant instance graph into an OWL reasoner such as HermiT. Report the exact set of loaded modules and data, the tool version, consistency, and unsatisfiable named classes. Checking the ontology alone is distinct from checking the ontology together with instance data.

### SHACL validation

Use a validator supporting both SHACL Core and SHACL-SPARQL. Supply:

1. The **union of `ontology/oeo.ttl` and your instance graph** as the data graph.
2. `ontology/oeo-shapes.ttl` as the shapes graph.
3. No additional OWL/RDFS entailment for the primary validation configuration.

Including the ontology in the data graph exposes the class hierarchy used by the shapes. The core shapes do not replace the corpus-specific extension constraints used in the full Enron evaluation.

### SPARQL queries

Execute the `.rq` files against the union of the core ontology and compatible instance data using a SPARQL 1.1 processor. The queries use explicit property paths and do not require OWL entailment. Where additional vocabulary is used in the instance data, load the necessary supporting module as well.

Scene matching uses the recorded Scene IRIs. Aliases are not automatically equated through `owl:sameAs` in this non-entailing configuration. An empty result is a valid query outcome and must be interpreted in relation to the supplied data.

Python is not required. Compatible ontology editors, reasoners, SHACL validators, and SPARQL processors can use these files. Python libraries may be used to automate the same workflow.

## Interpretation of validation results

OWL consistency, SHACL conformance, and successful query execution assess different properties. None establishes that an interpretation or its Worldview annotation is semantically correct or adequately supported by a source. Such claims require source-based human assessment. This repository does not provide an independent multi-annotator evaluation or an annotation-accuracy benchmark.

## Citation and version identification

When using these artifacts, cite the accompanying paper using its final bibliographic record and identify the repository commit or release used. No DOI or final proceedings details are asserted in this README.

## Licensing

No reuse license has been specified in this package. Public availability alone should not be interpreted as an open-source or open-data license. A license selected by the rights holder should be added before licensed reuse is advertised. Referenced external vocabularies remain subject to their own applicable terms.

## Source dataset

The Enron source data were obtained from the [Enron Email Dataset on Kaggle](https://www.kaggle.com/datasets/wcukierski/enron-email-dataset), published under the dataset identifier `wcukierski/enron-email-dataset`.

The OEO annotations distributed here are a selected, structured derivative of that corpus, not the complete Kaggle dataset. Source Message-IDs and provenance information support tracing the annotations to the original messages. Consult the dataset page for access information and the applicable usage terms.

## Enron data and evaluation artifacts

| Path | Contents |
| --- | --- |
| `data/enron-annotations.ttl` | Unmodified evaluated instance graph (1,333 triples). This is the authoritative RDF representation. |
| `data/enron-annotations.json` | Flattened, readable export of the effective annotation tables: 26 acts, 17 events, and 15 changes. No imports of earlier annotation versions are required. |
| `ontology/oeo-enron-extension.ttl` | Extension vocabulary used by the Enron graph. |
| `ontology/oeo-enron-shapes.ttl` | Additional SHACL constraints used for the Enron evaluation. |
| `evaluation/results/` | Primary and supplementary query CSVs, SHACL report, HermiT report, summary, and controlled-case report. |
| `evaluation/controlled-cases.json` | Base graphs, mutations, and expected outcomes for E00–E03. All paths are relative to the repository root. |
| `evaluation/cases/` | Add/remove triple sets for the controlled cases. |
| `queries/supplementary/` | Four supplementary analyses, separate from CQ1–CQ7. |

For the Enron evaluation, combine the core ontology, Enron extension, and annotation graph. Use both shapes files for SHACL validation. Execute the queries over this combined graph without additional inference. For controlled cases, apply the specified additions/removals to the base graph, then perform validation and OWL reasoning with the listed ontology modules. E00 is the normal control; E02 uses the same base graph and confirms that an absent optional Worldview is permitted. They are not four negative tests.

The primary CQ row counts are **18, 1, 0, 26, 26, 28, 3**. The historical SHACL report records conformance, and the HermiT report records consistency and no unsatisfiable named classes. The summary's `data_triples` value **1,439** includes the extension; `closure_triples` **1,806** includes the core ontology as well. Despite that field name, the primary run has `reasoning: false`; it is not an inferred closure count.

Historical result JSON files are preserved verbatim, including their original development filenames and paths. Query result filenames now correspond to the publication query filenames. These path labels in the reports are historical provenance, not current execution paths. `evaluation/controlled-cases.json` uses the publication paths.

### Annotation export conventions

In the JSON export, `changes`, `events`, and `agents` use named fields. `acts` preserves the annotation-table fields: `ev` is the source Message-ID, `t` is the recorded time, `ctx` is the context category and description, `type` is the narration category, `ori` the temporal orientation, `crit` the interpretation criterion, `quotes` the supporting excerpts, `voice` the mediation category, and `via` the mediating agents. `interprets`, `relational`, and `reinterprets` contain referenced identifiers. `worldview` is the effective optional act-level annotation, with `null` meaning not recorded. Short category labels in JSON are mapped to ontology individuals in RDF. Legacy Agent- and Event-level Worldview fields are omitted because they are not RDF links in the evaluated graph.

### Review-status provenance

The paper reports that the authors reviewed the semantic annotations. The archived RDF still contains the earlier `pending human review` metadata. This packaging step preserves that evaluated graph and does not invent reviewer identities, dates, or annotation-level decisions. These historical labels must not be interpreted as independent multi-annotator assessment. The authors should reconcile the review metadata with their actual review record before the final public release; any graph changes require renewed checks and updated counts where applicable.

### Extension scope

The extension is preserved from the evaluated files, including historical version comments and additional declarations such as scoped non-interpretation. Their presence does not mean that every extension feature was populated or evaluated in the paper. The core model's Worldview links remain act-level `basedOn`.

### Third-party source material

Selected Enron-derived quotations and source identifiers are included in the annotation files. Any license subsequently chosen for original ontology or code contributions must distinguish these third-party materials and their applicable terms. Full source e-mails are not included.
