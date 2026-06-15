# OIPF Specification — 02 Components (detail)

**Version 0.3.0 (draft)**

## 1. Canonical Production Semantics

A shared object vocabulary so different sites become *mappable* through a common
structure (not identical). Core objects:

| Object | Description |
|---|---|
| Site / Area / Line / Unit | the facility hierarchy |
| Asset | equipment: pump, tank, reactor, filter, exchanger, compressor, oven |
| Tag | a sensor, signal, variable or historian point |
| Stream / Flow | material, energy, water, air, steam, chemical, product |
| State | running, idle, cleaning, startup, shutdown, degraded, abnormal |
| Event | alarm, cleaning, maintenance, batch start/end, quality deviation |
| Recipe / Procedure | structured production/cleaning recipe; SOP |
| Constraint | safety, quality, environmental, equipment, operating limit |
| Model | ML, physics, statistical or rule-based |
| Recommendation | suggested action with reason, confidence, expected impact |
| Outcome | accepted/rejected action, actual result, savings, deviation |

## 2. Plant Graph

Connects assets, tags, flows, states, recipes, constraints, events, models and outcomes so
AI systems know not only *what* a value is but *what it means*. Example:

```
Plant → Line → Filtration Unit
                 ├── Filter (asset)
                 ├── Inlet / Outlet pressure, Flow (tags)
                 ├── Cleaning procedure
                 ├── Fouling model
                 ├── Quality constraint
                 └── Cleaning recommendation workflow
```

## 3. Connector Abstraction

A uniform adapter interface so a package binds to a site without bespoke plumbing:
OPC UA, MQTT/Sparkplug, historian connectors, SQL, REST, CSV and document import. The
package declares the *canonical variables* it needs; the connector layer resolves them from
whatever the site actually runs. Connectors are reusable across packages and sites.

## 4. Production Package Format

The deployable unit of operational intelligence — a versioned directory with a manifest and
declarative objects. Normative structure in [`03-package-format.md`](03-package-format.md).

## 5. Model Contract

A declarative boundary that turns a model from an isolated script into a reusable
component. Defines: required input signals + asset context; time window; operating-state
assumptions; units/transformations; constraints; output format; confidence; explanation
fields; required validation tests; fallback behaviour; human-review requirement.

```
prediction: fouling_risk_high
confidence: 0.87
affected_asset: heat_exchanger_2
estimated_loss_per_hour: 420 EUR
recommended_action: inspect_or_schedule_cleaning
human_approval_required: true
```

## 6. Agentic Workflow

How a recommendation becomes a governed, auditable, human-in-the-loop action:

```
detect → check constraints → generate recommendation → explain (reason + confidence)
→ request approval → create work order/action → record decision
→ compare outcome vs prediction → update operational memory
```

This is the UAPF profile for operational technology.

## 7. Validation & Simulation

A package is testable before it touches production: schema validation; tag-mapping
validation; unit-consistency; missing-data checks; historical backtesting; model-performance
checks; constraint-compliance; recommendation simulation; approval-path testing; access &
cybersecurity checks. Equivalent to automated testing in software, adapted to operations.

## 8. Audit & Governance

Every recommendation traces to: data inputs and window, model version, constraints checked,
confidence, human decision, and outcome. At conformance **Signed**, entries carry DID/VC
signatures (VeriDocs). Governance principles are specified in
[`05-governance.md`](05-governance.md).

## 9. Outcome Feedback

Closes the loop: records disposition (accepted/rejected/modified), action taken, measured
result and attributed saving; feeds model recalibration and savings-attribution. This is
what makes the capability *compound* rather than reset each deployment.

## 10. Runtime Environment

Executes packages on-premises, at the edge, in private cloud, hybrid or containerised.
Capabilities: package deployment; version management; connector configuration; model
execution; workflow orchestration; audit logging; recommendation serving; feedback capture;
**rollback**; and monitoring. The runtime is the most likely **proprietary** component
(see `05 §2`); its *interfaces* should remain open.
