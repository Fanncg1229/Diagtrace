# DiagTrace

This anonymous repository contains the DiagTrace benchmark data used in the submitted paper.
It releases the constructed reference resources and the matched interactive reconstruction traces; it is not intended to be a full training or evaluation pipeline release.

## Contents

- `data/diagtrace_510.jsonl`: Reference resources for 510 cases.
- `data/evaluation_subset_225.json`: Case identifiers used for the matched four-model evaluation.
- `data/taxonomy.json`: Clinical information categories and weights.
- `data/model_comparison_225_summary.json`: Aggregate metrics corresponding to the matched subset.
- `interaction_traces/`: Four-model interactive reconstruction traces on the matched 225-case subset.
- `schemas/`: JSON schema for the released records.
- `prompts/`: Prompt references used for construction, interaction, and audits.
- `examples/`: A representative benchmark instance.

## Data Format

Each case contains an initial presentation, source-grounded event bank, clinical-course information, and diagnostic references. Article order reflects the source report and should not be interpreted as an adjudicated clinical timeline.

## Source

Cases are derived from articles in the PubMed Central Open Access collection. Each record includes its PMCID and PMC URL. Original NXML/XML files, article PDFs, and figure images are not redistributed.

## Evaluation Subset

`data/evaluation_subset_225.json` identifies the shared 225-case subset used for the four-model comparison reported in the paper. The corresponding interaction traces are organized by clinician-agent model under `interaction_traces/`.

## Notes

This release does not include raw PMC NXML/XML files, article PDFs, figure images, API logs, token/cost logs, or local execution artifacts.

## License

See `LICENSE.md`.
