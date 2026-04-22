# Architecture Overview

EquiLens is a two-stage system.

## Stage 1: Telemetry Engine
Takes prediction outputs from any classifier and computes a fixed vector of
statistical features per time window. The same computation runs regardless of
model domain, architecture, or class count.

Features cover: distributional drift, prediction uncertainty, confidence stability,
behavioural divergence, temporal trends, and data quality signals.

## Stage 2: Reliability Engine
A trained meta-model that takes telemetry vectors as input and outputs
an incident probability for future windows.

```
Prediction outputs → Telemetry Engine → Feature vector → Reliability Engine → P(incident)
```

The monitored model is a black box throughout. Only its outputs are observed.
