# OIPF Specification — 02 Lifecycle & Conformance

**Version 0.1.0 (draft)**

## 1. Deployment lifecycle

1. **Bind** — apply a site overlay: map site tags to the package's canonical variables,
   set constraint thresholds and parameters.
2. **Validate** — run `validation-tests.yaml` against live/historical data (tag presence,
   unit sanity, derivation checks, model back-test accuracy).
3. **Shadow** — run at L0/L1 in parallel with current operations; benchmark recommendations
   against outcomes before granting trust.
4. **Operate** — promote to the declared maturity level once shadow results clear.
5. **Feed back** — every decision and measured result is written to the outcome ledger and
   used to recalibrate the model and the savings attribution.

## 2. Deployment maturity levels

| Level | Name | Behaviour | Requires |
|---|---|---|---|
| L0 | Monitor | context + KPIs only | Core |
| L1 | Advisory | recommends; human acts | Core |
| L2 | Supervised | recommends + prepares action; human approves | constraints + workflow approver |
| L3 | Closed-loop (bounded) | acts within constraints; human on exceptions | hard constraints + signed audit |
| L4 | Autonomous (bounded) | self-optimises within envelope | proven L3 history + oversight |

A package declares the **maximum** level it supports; a deployment runs at or below it.

## 3. Conformance levels

- **Core** — valid manifest + asset-graph + tag-map + model-contract + workflow, all schema-valid.
- **Plus** — Core + `savings.yaml` + `validation-tests.yaml` + an outcome ledger.
- **Signed** — Plus + DID/VC-signed outcome and audit provenance (VeriDocs).

## 4. Validation (normative checks)

A conforming validator MUST verify: every `model-contract` input resolves to a `tag-map`
entry; every `tag-map` `asset_ref` exists in `asset-graph`; every constraint references
known variables; the manifest's declared `maturity` is supported by the present objects
(e.g. L2 requires `constraints.yaml`).
