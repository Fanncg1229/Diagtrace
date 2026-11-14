# Public data reproducibility audit

Audit date: 2026-11-13  
Public repository: `Fanncg1229/Diagtrace` at commit `13e23ca48b775993cbbb103f3db0917c14582ebf`.

## Finding

The current public repository is **not sufficient by itself** to reproduce the corrected camera-ready Table 3, Figure 2, fixed-checklist analysis, or full-scale sensitivity analysis from real-case artifacts.

## What is currently public

- 510 unique cases and exactly 5,911 construction-stage `reference_resource.evidence_events` (mean 11.590 per case).
- Four sets of 225 matched interaction traces.
- The original matched-subset summary computed with the pre-correction request classifier.

## Critical gaps

1. The public 510-case JSONL does not contain the Setting 2 `evidence_items` banks used by the report agent and deterministic evaluator. The matched canonical bank contains 1,790 items before phase filtering and 1,439 eligible post-presentation items; event recall is defined on 224 cases.
2. The public matched traces contain old saved `trajectory_metrics`; their aggregate Tversky/LCS/pairwise values are the pre-fix values, not the corrected camera-ready values.
3. GPT, Gemini, and Kimi public episodes are sanitized-exact matches to all 225 local canonical episodes. Claude matches 219/225; the six duplicated PMCIDs use old specialty episodes.
4. The public 510-case specialty labels for those six PMCIDs are the old specialties, not the canonical evaluation identities.
5. The public repository includes only matched-225 episodes, not the 502/498/502 complete-case episodes required for full-scale sensitivity.
6. Fixed-checklist episodes and the exact 16-case manifest are absent.
7. The 400 saved FVCU judgment outputs are absent. Two Claude judgments (`PMC10254956`, `PMC4938284`) refer to stale episodes, although the camera-ready aggregate retains all 100 saved judgments and reports this explicitly.

## Six canonical specialty overrides

| PMCID | Existing public/old specialty | Canonical specialty |
|---|---|---|
| PMC10008168 | neurology | radiology |
| PMC10254956 | dermatology | neurology |
| PMC10441080 | dermatology | oncology |
| PMC11391149 | dermatology | oncology |
| PMC12255965 | dermatology | nephrology |
| PMC4938284 | internalmed | nephrology |

## Offline validation performed

- Combined the existing public matched traces with local canonical Setting 2 banks and the six canonical Claude replacements.
- Recomputed corrected Tversky, LCS, pairwise, weighted precision/recall/F1, event recall, redundancy, off-protocol, and turn metrics with the released corrected classifier.
- Every deterministic matched-225 value reproduced the camera-ready Table 3 value exactly.
- Recomputed the full-scale 502/498/502/225 metrics from saved local episodes; maximum absolute difference from `full_scale_vs_matched_metrics.csv` was `0`.
- Recomputed fixed-checklist event comparisons, bootstrap intervals, and category metrics; maximum absolute difference from the camera-ready CSVs was `0`.
- Confirmed all 16 checklist case snapshots match their canonical Setting 2 banks.

## Release recommendation

Keep the original public files unchanged for provenance. After review, add the staged artifacts under a versioned path such as `camera_ready_release/`, update the public README to distinguish construction events from Setting 2 items, and mark `data/model_comparison_225_summary.json` plus embedded `trajectory_metrics` as pre-correction outputs. The corrected classifier remains in the code repository.
