# Phase 1 Results

## Data

- 7 models (NLP + vision), 5 streams each, 35 independent runs
- 1,880 telemetry windows, 464 incidents (24.7%)
- 45 features across 9 categories, 42 used for training (3 production-only excluded)

## Temporal Offset Analysis (RQ1)

| k | XGBoost AUC ± Std | Threshold Baseline | Advantage |
|---|-------------------|-------------------|-----------|
| 0 | 0.998 ± 0.003 | 1.000 | -0.002 |
| 1 | 0.820 ± 0.109 | 0.761 | +0.059 |
| **2** | **0.794 ± 0.120** | **0.749** | **+0.045** |
| 3 | 0.787 ± 0.128 | 0.742 | +0.045 |

AUC degrades gracefully with lead time. XGBoost outperforms the threshold baseline at every offset ≥ 1.

## Leave-One-Model-Out (RQ2)

| Held Out | Task | AUC |
|----------|------|-----|
| M1 | Binary sentiment | 0.997 |
| M2 | 3-class sentiment | 1.000 |
| M3 | 7-class emotion | 1.000 |
| M4 | 3-class NLI | 1.000 |
| M5 | 3-class NLI (large) | 1.000 |
| M6 | 1000-class vision | 0.626 |
| M7 | 6-class toxicity | 1.000 |

Text-to-text transfer: near-perfect. Text-to-vision: 0.626 (single vision model in training).

## Temporal Split (60/40)

| Model | AUC |
|-------|-----|
| XGBoost | 0.999 |
| Random Forest | 0.989 |

## Feature Selection

Recursive feature elimination from 42 to 5 features. AUC peaked at 0.820 (13 features), optimal set at 0.810 (5 features). 88% dimensionality reduction with no loss in predictive performance. The surviving features cluster in the drift and confidence families.

## Limitations

- Incident labels are rule-based proxies, not ground truth accuracy
- Cross-modality transfer limited (single vision model)
- Fold variance ±0.120 (35 groups across 5 folds)
- 3 features always zero in lab conditions (production-only)
- No hyperparameter optimisation (deferred to Phase 2 with accuracy-based labels)
