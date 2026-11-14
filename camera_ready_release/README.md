# DiagTrace Camera-Ready Data Release

This directory contains the publicly released canonical artifacts for reproducing the corrected EACL 2027 Findings camera-ready results.

It contains the canonical Setting 2 resources needed to reproduce the corrected camera-ready analyses:

- 502 canonical Setting 2 event banks (`evidence_items`), separate from the 5,911 construction-stage `evidence_events` already released in `data/diagtrace_510.jsonl`;
- 1,727 completed canonical episodes: GPT-4.1 mini 502, Claude Haiku 4.5 498, Gemini 2.5 Flash 502, and Kimi K2.5 225;
- the canonical matched-225 manifest (900 model-case rows);
- the 16 fixed-checklist episodes and manifest;
- 400 saved FVCU judgment outputs (100 per model);
- corrected expected aggregate outputs and a SHA-256 inventory.

The six specialty overrides are recorded in `manifests/canonical_specialty_overrides.json`. The staged Claude episodes use the canonical specialty versions; the six old public Claude traces are not overwritten.

## Proposed destination

If approved, add this directory to the public data repository under a new non-destructive path such as `camera_ready_release/`. Do not replace the existing `data/` or `interaction_traces/` directories; retain them as the original submission-era release and clearly label their metrics as pre-correction.

## Offline scoring

With the code repository cloned next to the data repository and this directory installed as `Diagtrace/camera_ready_release`:

```bash
cd DiagTrace-code
python evaluation/score_manifest.py \
  --manifest ../Diagtrace/camera_ready_release/manifests/matched225_manifest.jsonl \
  --artifact-root ../Diagtrace/camera_ready_release \
  --output-dir /tmp/diagtrace-matched225

python evaluation/score_manifest.py \
  --manifest ../Diagtrace/camera_ready_release/manifests/full_scale_manifest.jsonl \
  --artifact-root ../Diagtrace/camera_ready_release \
  --output-dir /tmp/diagtrace-full-scale
```

Compare the resulting deterministic metrics with `expected_results/`. Figure 2 can be regenerated from `expected_results/category_recall_corrected_canonical225.csv` using the code repository's heatmap script.

## Integrity

`SHA256SUMS.csv` records each staged file's path, type, size, and SHA-256 digest. The manifests also carry the canonical event-bank digest for every case/model row, allowing the scorer to reject cross-model snapshot mismatches.
