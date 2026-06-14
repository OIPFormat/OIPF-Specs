# Example: Heat-Exchanger Fouling / Cleaning Optimisation

**Domain:** manufacturing (process / chemicals).  **Maturity:** L2 (Supervised).  **Conformance:** Plus.

A shell-and-tube heat exchanger (`HX-101`) recovers heat from a hot process stream to
preheat a cold feed. Over time it **fouls**: deposits raise the fouling resistance `Rf`
and drop the overall heat-transfer coefficient `U`, so more downstream utility (steam) is
needed and pressure drop rises. Most plants clean on a **fixed conservative schedule** —
cleaning too early wastes labour, chemicals and downtime; too late wastes energy and
throughput.

This package turns that into a **clean-when-needed** decision: it tracks `U`/`Rf` from
existing sensors, predicts the `Rf` trajectory, and recommends the optimal cleaning date —
surfaced as a prepared CMMS work order an engineer approves.

## How it maps to OIPF

| Object | What it holds here |
|---|---|
| `asset-graph.yaml` | PLANT-A → HEAT-RECOVERY → HRS-1 → HX-101, hot & cold flows |
| `tag-map.yaml` | site tags → `T_hot_in/out`, `T_cold_in/out`, `F_hot/cold`, `dP_shell`; derived `U_overall`, `Rf` |
| `states-events.yaml` | in_service / cleaning / bypass; `cleaning_performed`, `fouling_threshold_crossed` |
| `constraints.yaml` | max `dP_shell`, max `Rf`, cleaning-window availability, isolation-before-clean |
| `model-contract.yaml` | inputs `U_overall`,`Rf` (72 h); outputs `Rf_trajectory`, `clean_by_date` + confidence |
| `workflow.yaml` | explain → engineer approve → create CMMS work order → record → feedback |
| `savings.yaml` | energy penalty from degraded `U` vs. clean baseline, net of cleaning cost |
| `validation-tests.yaml` | tag presence, `U` sanity, `Rf` monotonicity, clean-date back-test |

## Deploying to another site

Don't fork. Supply a `site.<id>.yaml` overlay that remaps tags and sets the `Rf`/`dP`
thresholds and cleaning windows for that exchanger. The base package is unchanged — that
portability is the whole point of OIPF.
