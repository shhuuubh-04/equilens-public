# Methodology Overview

## The Core Idea
EquiLens applies the predictive maintenance paradigm to ML model reliability.
In industrial predictive maintenance, sensor readings from equipment are used to forecast
failure before it occurs. EquiLens treats prediction outputs as sensors and trains a
meta-model to forecast reliability incidents from those signals alone.

## Two-Stage Architecture

**Stage 1 — Telemetry Engine**
Accepts prediction outputs from any classifier. Computes a fixed-schema vector of
statistical features per time window. Stateless, domain-agnostic, privacy-preserving.
No raw predictions stored. No model internals accessed.

**Stage 2 — Reliability Engine**
An XGBoost meta-model trained on telemetry vectors. Takes features from window t
and outputs P(incident in window t+k). Forecasts before threshold-based detectors
would fire.

## What Makes This Different
Existing monitoring tools are reactive — they detect problems after they occur.
EquiLens is predictive — it forecasts problems before they become visible.
It also operates entirely on prediction outputs, requiring no model internals,
making it viable for black-box third-party model deployments.
