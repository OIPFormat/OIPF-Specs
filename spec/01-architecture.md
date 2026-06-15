# OIPF Specification — 01 Architecture

**Version 0.3.0 (draft)**

## 1. Conceptual architecture

OIPF is the portable layer between an organisation's data foundation and its models +
operators. It does not own the tiers above or below it; it makes the capability that spans
them reusable.

```
Industrial / operational data sources
SCADA · DCS · PLC · historian · MES · CMMS · ERP · lab · documents
        ↓
Connector layer
OPC UA · MQTT/Sparkplug · SQL · REST/APIs · CSV · document import
        ↓
Data foundation
time-series store · lakehouse · event store · document index
        ↓
== OIPF runtime ==
plant graph · canonical semantics · packages · model contracts ·
workflows · validation/simulation · audit · outcome feedback
        ↓
Intelligence layer
ML models · physics models · rules · LLM agents · optimisation engines
        ↓
Human-in-the-loop operations
recommendations · approvals · work orders · operator actions
        ↓
Outcome feedback
actual result · savings · model improvement · audit trail
```

## 2. The ten components

| # | Component | Role | Detail |
|---|---|---|---|
| 1 | Canonical Production Semantics | shared object vocabulary that makes any site *mappable* | `02 §1` |
| 2 | Plant Graph | connects assets, tags, flows, states, events, models, outcomes | `02 §2` |
| 3 | Connector Abstraction | uniform adapters over OPC UA / historians / MQTT / MES / CMMS / ERP / docs | `02 §3` |
| 4 | Production Package Format | the deployable unit of operational intelligence | `02 §4`, `03` |
| 5 | Model Contract | declarative I/O boundary that makes models swappable & testable | `02 §5` |
| 6 | Agentic Workflow | recommend → explain → approve → act → record → feedback (UAPF DNA) | `02 §6` |
| 7 | Validation & Simulation | test a package against historical/live data before deployment | `02 §7` |
| 8 | Audit & Governance | trace every recommendation to data, model, constraint, approver, outcome | `02 §8`, `05` |
| 9 | Outcome Feedback | close the loop; attribute savings; improve the model | `02 §9` |
| 10 | Runtime Environment | execute, version, orchestrate, roll back and monitor packages | `02 §10` |

Components 1–2 give data **meaning**; 5–7 make decisions **governed and testable**; 8–9
make them **auditable and self-improving**; 3 and 10 make them **deployable**. Together
they cover the four things a model cannot carry by itself (see `CONCEPT.md §3`).
