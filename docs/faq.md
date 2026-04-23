# FAQ

**Is EquiLens open source?**
The documentation and research findings in this repository are licensed under CC BY-NC 4.0. The core software implementation is proprietary and maintained in a private repository.

**Does it require access to model internals?**
No. EquiLens operates entirely on prediction outputs — confidence scores and class probabilities. No model weights, training data, or feature pipelines are needed.

**What types of models can it monitor?**
Any classifier that produces probability outputs. Binary, multi-class, and multi-label classifiers across text, image, and tabular domains have been tested.

**How far in advance can it predict?**
Phase 1 demonstrates meaningful prediction at 2 windows of lead time (AUC = 0.794). The AUC degrades gracefully at k=3 (0.787) rather than collapsing.

**What is a "window"?**
A fixed-size batch of consecutive predictions from the monitored model. In Phase 1, each window contains 100 predictions.

**Why XGBoost?**
Strong performance on tabular data, robust to feature scale differences, native handling of missing values, and interpretable feature importance. The choice was deliberate — the contribution is the telemetry framework, not the classifier.

**What are the main limitations?**
Phase 1 uses rule-based incident labels (synthetic proxies for actual failure). Cross-modality transfer (text → vision) is limited with a single vision model. Fold variance is ±0.120. See [research/phase1_results.md](../research/phase1_results.md) for full limitations.

**Is there a paper?**
In preparation. Targeting submission September 2026.
