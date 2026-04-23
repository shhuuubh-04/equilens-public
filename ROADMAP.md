# Roadmap

## Phase 1 — Complete ✅

Telemetry engine, multi-stream data collection, XGBoost baseline predictor.

- 45-feature telemetry vectors across 9 categories
- 7 monitored models (NLP + vision), 35 data streams
- 1,880 windows collected, 464 incidents labelled
- AUC = 0.794 at k=2 lead time (outperforms threshold baseline by +0.045)

## Phase 2 — In Progress

- Accuracy-based ground truth labels (replacing heuristic threshold rules)
- Additional vision models (ResNet-50, EfficientNet) for cross-modality transfer
- LSTM temporal sequence modelling over 10–20 window sequences
- XGBoost + LSTM ensemble
- Hyperparameter optimisation (deferred to accuracy-based labels)
- Research paper preparation (September 2026 target)

## Phase 3 — Planned

- Telemetry failure archetypes via unsupervised clustering (K-means, HDBSCAN)
- Explainability layer: P(incident) + likely root cause, derived from telemetry patterns
- Cross-domain generalisation proof across NLP, vision, tabular, and speech
- Production deployment architecture (push API, real-time telemetry, alerting)
- Meta-model self-monitoring (detect when the predictor itself degrades)
