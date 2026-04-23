# EquiLens

**Predictive reliability monitoring for deployed ML models.**

EquiLens forecasts reliability incidents before they occur — using only prediction outputs. No model weights. No training data. No internals. Just the outside.

![Architecture](research/figures/architecture.png)

---

## The Problem

91% of ML models degrade in production ([Vela et al., 2022](https://doi.org/10.1038/s41598-022-15245-z)). Current monitoring tools detect this *after* it has already happened. The alert fires, the drift is confirmed, and somewhere upstream, users have already been getting wrong answers.

EquiLens asks a different question: can the statistical telemetry that a model produces during normal operation — confidence distributions, entropy patterns, drift trajectories — predict that a failure is *about to* happen?

## The Approach

Borrowed from predictive maintenance. Turbines have vibration sensors. ML models have prediction outputs. Same paradigm, different equipment.

- **Telemetry Engine** — extracts 45 statistical features per prediction window from model outputs alone. Stateless. Domain-agnostic. Works on any classifier.
- **Reliability Engine** — a trained XGBoost meta-model that takes telemetry vectors as input and outputs P(incident in next *k* windows).

The monitored model is a black box. That's the point.

## Phase 1 Results

- **Lead time:** AUC = 0.794 at 2-window temporal offset, outperforming threshold baseline (0.749)
- **Cross-domain transfer:** AUC ≥ 0.997 within text modality (6 models → held-out 7th)
- **Feature efficiency:** 5 features carry 88% of predictive signal (42 → 5 via recursive elimination)
- **Scale:** 7 models, 35 data streams, 1,880 telemetry windows, 464 incidents

Full methodology and results: [research/phase1_results.md](research/phase1_results.md)

## Read More

- 📄 **Blog:** [Before the Alerts Fire](https://medium.com/@shhuuubh/LINK) — the full story, including what broke
- 🗺️ **Roadmap:** [ROADMAP.md](ROADMAP.md)
- 📐 **Architecture:** [docs/architecture_overview.md](docs/architecture_overview.md)
- ❓ **FAQ:** [docs/faq.md](docs/faq.md)
- 🔬 **Methodology:** [research/methodology_overview.md](research/methodology_overview.md)

## Status

Phase 1 is complete. Phase 2 is in progress. A research paper is forthcoming.

This repository contains documentation, research findings, and writing. The core implementation is maintained in a private repository under a proprietary license.

## License

Documentation and writing in this repository are licensed under [CC BY-NC 4.0](LICENSE).
The EquiLens software implementation is proprietary and not included in this repository.

## Contact

Built by [Shubhan Singh](https://linkedin.com/in/shhuuubh) — BTech Computer Engineering, NMIMS Navi Mumbai.

If you work in ML observability, production monitoring, or reliability engineering, I'd like to hear from you.
