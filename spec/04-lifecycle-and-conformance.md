# OIPF Specification — 04 Lifecycle & Conformance

**Version 0.3.0 (draft)**

## 1. Deployment lifecycle

1. **Bind** — apply a site overlay (tag mapping, thresholds, parameters).
2. **Validate** — run `validation-tests.yaml` against historical/live data.
3. **Shadow** — run at L0/L1 in parallel with current operations; benchmark before trust.
4. **Operate** — promote to the declared maturity level once shadow results clear.
5. **Feed back** — write every decision and result to the outcome ledger; recalibrate.

## 2. Deployment maturity levels

| Level | Name | Behaviour | Requires |
|---|---|---|---|
| L0 | Monitor | context + KPIs only | Core |
| L1 | Advisory | recommends; human acts | Core |
| L2 | Supervised | recommends + prepares action; human approves | constraints + approver |
| L3 | Closed-loop (bounded) | acts within constraints; human on exceptions | hard constraints + signed audit |
| L4 | Autonomous (bounded) | self-optimises within envelope | proven L3 history + oversight |

A package declares the **maximum** level it supports; a deployment runs at or below it.

## 3. Conformance levels

- **Core** — valid manifest + asset-graph + tag-map + model-contract + workflow.
- **Plus** — Core + `savings.yaml` + `validation-tests.yaml` + an outcome ledger.
- **Signed** — Plus + DID/VC-signed outcome and audit provenance (VeriDocs).
