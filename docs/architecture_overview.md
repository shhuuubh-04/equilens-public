# Architecture Overview

## Two-Stage Pipeline

EquiLens operates as a two-stage pipeline where each stage has a distinct role and no shared state.

**Stage 1 — Telemetry Engine (Stateless)**

Accepts prediction outputs from any classifier and computes a fixed-schema vector of 45 statistical features per time window. The engine is domain-agnostic by construction: it operates on probability vectors and confidence scores, which every classifier produces regardless of domain.

The 45 features span nine categories:
1. Distributional drift
2. Prediction uncertainty
3. Confidence distribution properties
4. Prediction behaviour patterns
5. Output stability
6. Behavioural divergence across subgroups
7. Temporal dynamics
8. Anomaly and data quality indicators
9. Operational signals

Every feature is derived entirely from prediction outputs. No model internals, no input data, no ground truth labels at inference time.

**Stage 2 — Reliability Engine (Learned, Stateful)**

A trained XGBoost meta-model that accepts telemetry vectors and outputs P(incident in next *k* windows). Trained on historical telemetry with temporal offset labels — features at window *t* predict incidents at window *t+k*.

## Data Flow

```
Monitored model outputs
	↓ confidence scores, class probabilities
Telemetry Engine (45 features, 9 categories)
	↓ fixed-schema telemetry vector
Storage (Apache Parquet, Hive partitioning)
	↓ historical telemetry windows
Reliability Engine (XGBoost meta-model)
	↓
P(incident in next k windows)
```

## Evaluation Architecture

Three evaluation strategies, each answering one research question:

- **Temporal offset analysis (RQ1):** Train and evaluate at k=0,1,2,3 with GroupKFold (35 stream groups). Measures predictive lead time.
- **Leave-one-model-out (RQ2):** Train on 6 models, test on the 7th. Measures cross-domain transfer.
- **Temporal split (60/40):** Train on early windows, test on later windows. Validates forward prediction.
