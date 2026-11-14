# DiagTrace data

This repository contains the public data release for **DiagTrace: An Interactive Benchmark for Clinical Decision Making**, accepted to Findings of EACL 2027.

## Authoritative camera-ready release

`camera_ready_release/` is the authoritative data version for reproducing the corrected EACL 2027 camera-ready results. It contains:

- 502 canonical Setting 2 event banks;
- 1,727 completed canonical episodes: GPT-4.1 mini 502, Claude Haiku 4.5 498, Gemini 2.5 Flash 502, and Kimi K2.5 225;
- the canonical matched-225 and full-scale manifests;
- 16 fixed-checklist episodes and their manifest;
- 400 saved FVCU judgment outputs;
- corrected expected aggregate outputs, audit documentation, and 2,663 SHA-256 checksum records.

Use the companion code repository, [Fanncg1229/DiagTrace-code](https://github.com/Fanncg1229/DiagTrace-code), for deterministic scoring and plotting.

## Original release retained for provenance

The original submission-era files remain unchanged in `data/`, `interaction_traces/`, `schemas/`, and `examples/`. They are retained for provenance and should not be used in place of `camera_ready_release/` when reproducing corrected camera-ready results.

In particular, `data/model_comparison_225_summary.json` is an **outdated pre-correction summary** produced before the request-category classifier correction. Saved `trajectory_metrics` embedded in the original interaction traces are also pre-correction values. Recompute metrics from the canonical artifacts instead.

The 5,911 `reference_resource.evidence_events` in `data/diagtrace_510.jsonl` are construction-stage events. They are not the frozen Setting 2 report-agent `evidence_items` used for camera-ready evaluation. In the matched-225 release, the Setting 2 bank contains 1,790 items before phase filtering and 1,439 eligible post-presentation items.

## Six corrected Claude snapshots

Six original Claude traces use outdated specialty snapshots. The original files are preserved, but the corrected canonical episodes under `camera_ready_release/episodes/claude_haiku_4_5/` must be used:

| PMCID | Outdated specialty | Canonical specialty |
|---|---|---|
| PMC10008168 | neurology | radiology |
| PMC10254956 | dermatology | neurology |
| PMC10441080 | dermatology | oncology |
| PMC11391149 | dermatology | oncology |
| PMC12255965 | dermatology | nephrology |
| PMC4938284 | internalmed | nephrology |

The mapping is machine-readable in `camera_ready_release/manifests/canonical_specialty_overrides.json`.

## FVCU caveat

The camera-ready FVCU aggregate retains all 100 originally saved judgments per model. Two Claude judgments, for `PMC10254956` and `PMC4938284`, were produced from older episode snapshots. They are released as retained historical judgments and were **not recomputed**. FVCU is an auxiliary LLM-judged metric; the deterministic trajectory metrics are recomputed from the canonical episodes and event banks.

## Reproduction

Clone the data and code repositories side by side:

```bash
git clone https://github.com/Fanncg1229/Diagtrace.git
git clone https://github.com/Fanncg1229/DiagTrace-code.git
cd DiagTrace-code
python -m pip install -e '.[test]'
```

Recompute matched-225 and full-scale deterministic metrics:

```bash
python evaluation/score_manifest.py \
  --manifest ../Diagtrace/camera_ready_release/manifests/matched225_manifest.jsonl \
  --artifact-root ../Diagtrace/camera_ready_release \
  --output-dir /tmp/diagtrace-matched225

python evaluation/score_manifest.py \
  --manifest ../Diagtrace/camera_ready_release/manifests/full_scale_manifest.jsonl \
  --artifact-root ../Diagtrace/camera_ready_release \
  --output-dir /tmp/diagtrace-full-scale
```

Recompute the fixed-checklist analysis and aggregate saved FVCU judgments:

```bash
python evaluation/score_checklist_manifest.py \
  --checklist-manifest ../Diagtrace/camera_ready_release/manifests/fixed_checklist_manifest.jsonl \
  --model-manifest ../Diagtrace/camera_ready_release/manifests/matched225_manifest.jsonl \
  --artifact-root ../Diagtrace/camera_ready_release \
  --output-dir /tmp/diagtrace-checklist

python evaluation/aggregate_fvcu.py \
  --root ../Diagtrace/camera_ready_release/fvcu \
  --output /tmp/diagtrace-fvcu.csv
```

Expected outputs are in `camera_ready_release/expected_results/`. See `camera_ready_release/AUDIT_REPORT.md` and `camera_ready_release/SHA256SUMS.csv` for provenance and integrity information.

## Source provenance and limitations

Cases are derived from articles in the PubMed Central Open Access collection. Records include PMCID and PMC URL provenance. Source order follows article presentation and is not an adjudicated clinical timeline. DiagTrace is a research benchmark and is not intended for clinical decision support or patient care.

Original article NXML/XML files, PDFs, and figure images are not redistributed. Some benchmark records contain source-derived textual excerpts; those excerpts remain subject to each source article's license and attribution requirements. See `LICENSE.md` for the separation between benchmark-created annotations and third-party PMC material.

## License

See `LICENSE.md`. The companion code repository is separately distributed under the MIT License.
