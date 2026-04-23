# Methodology Overview

## Experimental Design

Seven pre-trained HuggingFace models were monitored across five data streams each, producing 35 independent collection runs and 1,880 telemetry windows with 464 labelled incidents (24.7% incident rate).

The telemetry engine computes 45 statistical features per window across nine categories, all derived from prediction outputs alone.

## Methodological Challenges and Corrections

Three issues were discovered and resolved during development:

**Label circularity.** Incident labels were defined as threshold breaches on telemetry metrics — the same metrics used as training features. XGBoost reconstructed the labelling rules instead of learning predictive patterns. Fix: temporal offset — features at window *t* predict labels at window *t+k*, breaking the deterministic relationship. AUC dropped from 1.000 to 0.885.

**Cross-validation leakage.** Sequential windows from the same data stream are autocorrelated. Random fold assignment placed near-identical neighbours across train/test boundaries. Fix: GroupKFold with stream-level grouping (35 groups). AUC dropped from 0.885 to 0.794.

**Redundant evaluation.** Standalone 5-fold CV produced AUC = 1.000 even with GroupKFold, because same-model streams correlate across folds. Removed from the pipeline. Three honest evaluations remain.

## Evaluation Strategies

1. **Temporal offset analysis (RQ1):** k=0,1,2,3 with GroupKFold. Measures lead time.
2. **Leave-one-model-out (RQ2):** Train on 6 models, test on the 7th. Measures transfer.
3. **Temporal split (60/40):** Train on early windows, test on later. Validates forward prediction.

## Threshold Baseline

The D021 labelling rules applied at window *t* against labels at window *t+k* serve as the reference baseline. At k=2, the baseline achieves AUC = 0.749. The meta-model must exceed this to justify its complexity.
