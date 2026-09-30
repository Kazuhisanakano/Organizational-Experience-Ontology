# Publication filename mapping

Development paths refer to the local source snapshot, not web URLs. Historical result reports retain these labels.

| Source | Publication path |
| --- | --- |
| `ontology_v3/oeo.ttl` | `ontology/oeo.ttl` |
| `ontology_v3/oeo-shapes.ttl` | `ontology/oeo-shapes.ttl` |
| `ontology_v2/oeo-ext-v2.ttl` | `ontology/oeo-enron-extension.ttl` |
| `ontology_v2/oeo-ext-shapes-v2.ttl` | `ontology/oeo-enron-shapes.ttl` |
| `enron/enron_oeo_v3.ttl` | `data/enron-annotations.ttl` |
| `results_v3/enron/cq1.csv` | `evaluation/results/cq01-event-individuation.csv` |
| `results_v3/enron/cq2.csv` | `evaluation/results/cq02-focal-core-reversal.csv` |
| `results_v3/enron/cq3.csv` | `evaluation/results/cq03-same-wording-different-interpretations.csv` |
| `results_v3/enron/cq4.csv` | `evaluation/results/cq04-provenance-and-revision.csv` |
| `results_v3/enron/cq5.csv` | `evaluation/results/cq05-coexisting-interpretations.csv` |
| `results_v3/enron/cq6.csv` | `evaluation/results/cq06-interpretation-worldviews.csv` |
| `results_v3/enron/cq7.csv` | `evaluation/results/cq07-relational-interpretations.csv` |
| `queries_v4/ext/x1_contested_changes.rq` | `queries/supplementary/x1-contested-changes.rq` |
| `results_v3/enron/x1_contested_changes.csv` | `evaluation/results/x1-contested-changes.csv` |
| `queries_v4/ext/x2_voice_mediation.rq` | `queries/supplementary/x2-voice-mediation.rq` |
| `results_v3/enron/x2_voice_mediation.csv` | `evaluation/results/x2-voice-mediation.csv` |
| `queries_v4/ext/x3_same_words_different_events.rq` | `queries/supplementary/x3-same-words-different-events.rq` |
| `results_v3/enron/x3_same_words_different_events.csv` | `evaluation/results/x3-same-words-different-events.csv` |
| `queries_v4/ext/x4_granularity.rq` | `queries/supplementary/x4-granularity.rq` |
| `results_v3/enron/x4_granularity.csv` | `evaluation/results/x4-granularity.csv` |
| `results_v3/enron/summary.json` | `evaluation/results/query-summary.json` |
| `results_v3/enron/shacl_report.json` | `evaluation/results/shacl-report.json` |
| `results_v3/hermit_enron.json` | `evaluation/results/owl-consistency.json` |
| `results_v3/tests/test_report_enron.json` | `evaluation/results/controlled-cases-report.json` |
| `tests_v3/cases/E01_kean_two_focal.ttl` | `evaluation/cases/e01-two-focal-add.ttl` |
| `tests_v3/cases/E01_kean_two_focal.remove.ttl` | `evaluation/cases/e01-two-focal-remove.ttl` |
| `tests_v3/cases/E03_shapiro_no_core.remove.ttl` | `evaluation/cases/e03-missing-core-remove.ttl` |
| `queries_v4/cq1.rq` | `queries/cq01-event-individuation.rq` |
| `queries_v4/cq2.rq` | `queries/cq02-focal-core-reversal.rq` |
| `queries_v4/cq3.rq` | `queries/cq03-same-wording-different-interpretations.rq` |
| `queries_v4/cq4.rq` | `queries/cq04-provenance-and-revision.rq` |
| `queries_v4/cq5.rq` | `queries/cq05-coexisting-interpretations.rq` |
| `queries_v4/cq6.rq` | `queries/cq06-interpretation-worldviews.rq` |
| `queries_v4/cq7.rq` | `queries/cq07-relational-interpretations.rq` |

`data/enron-annotations.json` is a flattened export of the effective `annotations_v3.py` tables, including their inherited data.
