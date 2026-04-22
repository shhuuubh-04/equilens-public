# Roadmap

## Phase 1 — Complete ✅
Telemetry engine, multi-stream data collection, XGBoost baseline predictor.
45-feature telemetry vectors. 7 monitored models. 1880 windows. AUC = 0.794 at k=2 lead time.

## Phase 2 — In Progress
- Accuracy-based ground truth labels (replacing heuristic rules)
- Additional vision models for cross-modality transfer
- LSTM temporal sequence modeling
- XGBoost + LSTM ensemble

## Phase 3 — Planned
- Telemetry signatures and failure archetypes
- Explainability layer: P(incident) + reason, no model internals
- Cross-domain generalization proof
- Research paper submission
