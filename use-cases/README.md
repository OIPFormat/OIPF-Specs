# OIPF Use-Case Catalogue

Reference briefs for recurring operational-intelligence package types. Each is the *same*
OIPF skeleton (context → model contract → decision workflow → outcome) with different
physics, tags and models — which is the entire point of the framework.

| Use case | Typical wedge | Maturity to start |
|---|---|---|
| [Cleaning / fouling optimisation](cleaning-fouling-optimisation.md) | clean-when-needed vs. fixed schedule | L2 |
| [Energy-loss detection](energy-loss-detection.md) | abnormal consumption vs. expected curve | L1 |
| [Predictive maintenance](predictive-maintenance.md) | degradation → planned intervention | L1–L2 |
| [Quality-drift detection](quality-drift-detection.md) | early drift before spec failure | L1 |
| [Downtime root-cause analysis](downtime-root-cause.md) | event correlation → recurring-fault prevention | L0–L1 |

A brief becomes a package by filling the objects in [`../examples`](../examples) style and
binding a site overlay.
