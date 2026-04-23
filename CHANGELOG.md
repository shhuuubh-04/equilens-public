# Changelog

## Phase 1 — April 2026

### Architecture
- Two-stage pipeline: Telemetry Engine (stateless) + Reliability Engine (learned)
- 45-feature telemetry vector across 9 categories, computed from prediction outputs only
- Domain-agnostic by construction — same schema for binary text, 1000-class vision, multi-label toxicity

### Data Collection
- 7 HuggingFace models monitored (M1–M7): sentiment, emotion, NLI, vision, toxicity
- 5 data streams per model simulating distribution shift types
- 1,880 telemetry windows collected on Google Colab T4 GPU (~50 minutes)
- 464 incidents labelled (24.7% incident rate)

### Training & Evaluation
- XGBoost meta-model with temporal offset (k=2) and GroupKFold (35 stream groups)
- Primary result: AUC = 0.794 ± 0.120 at 2-window lead time
- Threshold baseline: AUC = 0.749 (XGBoost outperforms by +0.045)
- Leave-one-model-out: AUC ≥ 0.997 for text models, 0.626 for vision (single vision model)
- Temporal split (60/40): XGBoost AUC = 0.999, Random Forest AUC = 0.989
- Recursive feature elimination: 5 optimal features at AUC = 0.810 (88% reduction)

### Methodological Corrections
- Diagnosed and fixed label circularity (AUC 1.000 → 0.885 via temporal offset)
- Diagnosed and fixed CV leakage (AUC 0.885 → 0.794 via GroupKFold)
- Removed standalone 5-fold CV (redundant — same-model streams correlate across folds)

### Storage & Infrastructure
- Apache Parquet with Hive-style partitioning
- DuckDB for in-process analytics
- GPU/CPU device management with OOM fallback
