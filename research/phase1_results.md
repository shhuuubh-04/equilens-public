# Phase 1 Results

## Status
Complete — 2026-04-04

## Primary Result (RQ1): Temporal Lead Time
XGBoost meta-model trained on output-only telemetry achieves AUC = 0.794 ± 0.120
at k=2 temporal offset, outperforming a threshold-based detection baseline (AUC = 0.749)
by +0.045. Lead time claim validated: AUC > 0.65 at k ≥ 2.

| k | XGBoost AUC | Threshold Baseline | Lead Time |
|---|-------------|-------------------|-----------|
| 0 | 0.998 ± 0.003 | 1.000 | — |
| 1 | 0.820 ± 0.109 | 0.761 | 1 window |
| 2 | 0.794 ± 0.120 | 0.749 | 2 windows |
| 3 | 0.787 ± 0.128 | 0.742 | 3 windows |

## Cross-Domain Transfer (RQ2): Leave-One-Model-Out
| Model | AUC |
|-------|-----|
| M1 (binary sentiment) | 0.997 |
| M2 (3-class sentiment) | 1.000 |
| M3 (7-class emotion) | 1.000 |
| M4 (NLI) | 1.000 |
| M5 (NLI large) | 1.000 |
| M6 (1000-class vision) | 0.626 |
| M7 (toxicity) | 1.000 |

Within-modality transfer is near-perfect. Cross-modality transfer to vision is the open problem.

## Feature Importance
Top 3 features account for 86.9% of XGBoost gain:
1. Jensen-Shannon Divergence — 0.358
2. Mean Confidence — 0.292
3. PSI — 0.219

Recursive Feature Elimination: 88% of features eliminated with no loss in predictive performance.
Optimal 5-feature subset achieves AUC = 0.810.

## Known Limitations
- Incident labels are rule-based proxies, not ground truth accuracy
- Cross-modality transfer to vision requires more vision training data
- 3 of 45 telemetry features are production-only and untested in lab conditions

## Figures
See `figures/` for visualizations from the Phase 1 training run.
